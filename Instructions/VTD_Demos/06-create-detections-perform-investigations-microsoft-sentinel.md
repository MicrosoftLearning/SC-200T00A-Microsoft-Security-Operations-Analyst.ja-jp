# <a name="module-6-create-detections-and-perform-investigations-with-microsoft-sentinel"></a>モジュール 6 Microsoft Sentinel を使用して検出を作成し、調査を実行する

**注**: このデモを正常に完了するには、[前提条件ドキュメント](00-prerequisites.md)のすべての手順を完了する必要があります。 

## <a name="attack-1-detection-with-sysmon"></a>Sysmon による攻撃 1 の検出

このタスクでは、セキュリティ イベント コネクタと Sysmon がインストールされているホストで攻撃 1 の検出を作成します。

この攻撃により、起動時に実行されるレジストリ キーが作成されます。  
```Command
REG ADD "HKCU\SOFTWARE\Microsoft\Windows\CurrentVersion\Run" /V "SOC Test" /t REG_SZ /F /D "C:\temp\startup.bat"
```

1. 管理者として WIN1 仮想マシンにログインします。パスワードは**Pa55w.rd**。  

2. Edge ブラウザーで、Azure portal (https://portal.azure.com ) に移動します。

3. **サインイン** ダイアログ ボックスで、ラボのホスティングプロバイダーから提供された管理者用の**テナント電子メール** アカウントをコピーして貼り付け、 **[次へ]** を選択します。

4. **パスワードの入力**ダイアログ ボックスで、ラボ ホスティング プロバイダーから提供された管理者用の**テナントパスワード**をコピーして貼り付け、 **[サインイン]** を選択します。

5. Azure portal の検索バーに「*Sentinel*」と入力してから、**[Microsoft Sentinel]** を選択します。

6. 先ほど作成した Microsoft Sentinel ワークスペースを選択します。

7. 一般セクションから**Log**を選択します。

8. First, you need to see where the data is stored. Since you just performed the attacks.  Set the Log Time Range to <bpt id="p1">**</bpt>Last 24 hours<ept id="p1">**</ept>.

9. 次のKQLステートメントを実行します

```KQL
search "temp\\startup.bat"
```

10. 結果は、3つの異なるテーブルについて示しています。DeviceProcessEvents DeviceRegistryEvents Event

    The Device* tables are from Defender for Endpoint (Data Connector - Microsoft 365 Defender).  Event is from our Data Connector Security Events. 

    Since we are receiving data from two different sources - Sysmon and Defender for Endpoint,  we will need to build two KQL statements that could be unioned later.  In our initial investigation, you will look at each separately.

11. Our first data source is Sysmon from Windows hosts.  Run the following KQL Statement.

```KQL
search in (Event) "temp\\startup.bat"
```
結果は、イベントテーブルに対してのみ表示されるようになりました。  

16. Create your own KQL statement to display all Registry Key Set Value rows.  Run the following KQL query:

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

17.  ここから引き続き検出ルールを作成できますが、このKQLステートメントは、他の検出ルールのKQLステートメントで再利用できるように見えます。  
    
    In the Log window, select <bpt id="p1">**</bpt>Save<ept id="p1">**</ept>, then <bpt id="p2">**</bpt>Save as function<ept id="p2">**</ept>.
    In the Save flyout, enter the following:

    名前: Event_Reg_SetValue [名前を付けて保存]:Function [関数のエイリアス]:Event_Reg_SetValue [カテゴリ]:Sysmon

18. 新しいクエリ タブを開きます。そして、以下の KQL ステートメントを実行します:

```KQL

Event_Reg_SetValue

```
Depending on the current data collection, you could receive many rows.  This is expected.  Our next task is to filter to our specific scenario.

19. 以下の　KQL　ステートメントを実行します:

```KQL

Event_Reg_SetValue | search "startup.bat"

```

22. It is important to help the Security Operations Analyst by providing as much context about the alert as you can. This includes projecting Entities for use in the investigation graph.  Run the following query:

```KQL
Event_Reg_SetValue 
| where Image contains "reg.exe"
| where Details startswith "C:\\TEMP"
| extend timestamp = TimeGenerated, HostCustomEntity = Computer, AccountCustomEntity = UserName

```

## <a name="you-have-completed-the-demo"></a>デモが完了しました。