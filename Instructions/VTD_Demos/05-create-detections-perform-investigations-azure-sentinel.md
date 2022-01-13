﻿# モジュール 5 Azure Sentinel を使用して検出を作成し、調査を実行する

**注**: このデモを正常に完了するには、[前提条件ドキュメント](00-prerequisites.md)のすべての手順を完了する必要があります。 

## Sysmonによる攻撃1の検出

このタスクでは、セキュリティイベントコネクタと Sysmon がインストールされているホストで攻撃1の検出を作成します。

この攻撃により、起動時に実行されるレジストリキーが作成されます。  
```Command
REG ADD "HKCU\SOFTWARE\Microsoft\Windows\CurrentVersion\Run" /V "SOC Test" /t REG_SZ /F /D "C:\temp\startup.bat"
```

1. 管理者として WIN1 仮想マシンにログインします。パスワードは **Pa55w.rd**。  

2. Edge　ブラウザーで Azure portal (https://portal.azure.com) に移動します。

3. **サインイン**ダイアログ ボックスで、ラボのホスティングプロバイダーから提供された管理者用の**テナント電子メール**アカウントをコピーして貼り付け、**次へ**を選択します。

4. **パスワードの入力**ダイアログ ボックスで、ラボ ホスティング プロバイダーから提供された管理者用の**テナントパスワード** をコピーして貼り付け、**サインイン**を選択します。

5. Azure ポータルの検索バーに「*Sentinel*」と入力し、「**Azure Sentinel**」を選択します。

6. 先ほど作成した Azure Sentinel ワークスペースを選択します。

7. 一般セクションから **Log** を選択します。

8. まず、データが保存されている場所を確認する必要があります。攻撃を行ったばかりなので  ログの時間範囲を**過去 24 時間**に設定します。

9. 次の KQL ステートメントを実行します

```KQL
search "temp\\startup.bat"
```

10. 結果は、3 つの異なるテーブルについて示しています。
    DeviceProcessEvents
    DeviceRegistryEvents
    Event

    デバイス*テーブルは、Defender for Endpoint （データコネクタ - Microsoft 365 Defender）からのものです。  イベントは、データコネクタのセキュリティイベントからのものです。 

    Sysmon と Defender for Endpoint の 2 つの異なるソースからデータを受信しているため、後で結合できる 2 つの KQL ステートメントを作成する必要があります。  最初の調査では、それぞれを個別に確認していきます。

11. 最初のデータソースは、Windows ホストからの Sysmon です。  以下の KQL ステートメントを実行します。

```KQL
search in (Event) "temp\\startup.bat"
```
結果は、イベントテーブルに対してのみ表示されるようになりました。  

16. 独自の KQL ステートメントを作成し、すべてのレジストリ キー セット値の行を表示します。  次の KQL クエリを実行します。

```KQL

Event
| where Source == "Microsoft-Windows-Sysmon"
| where EventID == 13
| extend RenderedDescription = tostring(split(RenderedDescription, ":")[0])
| project TimeGenerated, Source, EventID, Computer, UserName, EventData, RenderedDescription
| extend EvData = parse_xml(EventData)
| extend EventDetail = EvData.DataItem.EventData.Data
| project-away EventData, EvData  
| extend RuleName = EventDetail.[0].["#text"], EventType = EventDetail.[1].["#text"], UtcTime = EventDetail.[2].["#text"], ProcessGuid = EventDetail.[3].["#text"], 
    ProcessId = EventDetail.[4].["#text"], Image = EventDetail.[5].["#text"], TargetObject = EventDetail.[6].["#text"], Details = EventDetail.[7].["#text"]
    | project-away EventDetail 


```

17.  ここから引き続き検出ルールを作成できますが、この KQL ステートメントは、他の検出ルールの KQL ステートメントで再利用できるように見えます。  
    
    「ログ」ウィンドウで、「**保存**」、「**関数として保存**」の順に選択します。
    保存フライアウトで、次のように入力します。

    名前: Event_Reg_SetValue
    名前を付けて保存: 機能
    関数のエイリアス: Event_Reg_SetValue
    カテゴリ: Sysmon

18. 新しいクエリ タブを開きます。そして、以下の KQL ステートメントを実行します:

```KQL

Event_Reg_SetValue

```
在のデータ収集によっては、多くの行を受け取る可能性があります。  これは予測されている結果です。  次のタスクは、特定のシナリオにフィルターをかけることです

19. 以下の KQL ステートメントを実行します:

```KQL

Event_Reg_SetValue | search "startup.bat"

```

22. アラートについてできるだけ多くのコンテキストを提供することにより、セキュリティ運用アナリストを支援することが重要です。これには、調査グラフで使用するエンティティの投影が含まれます。  次のクエリを実行します。

```KQL
Event_Reg_SetValue 
| where Image contains "reg.exe"
| where Details startswith "C:\\TEMP"
| extend timestamp = TimeGenerated, HostCustomEntity = Computer, AccountCustomEntity = UserName

```

## デモが完了しました。