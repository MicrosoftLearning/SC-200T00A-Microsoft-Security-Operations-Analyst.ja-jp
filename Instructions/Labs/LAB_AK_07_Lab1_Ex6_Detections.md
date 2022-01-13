---
lab:
    title: '演習 6 - 検出を作成する'
    module: 'モジュール 7 – Microsoft Sentinel を使用して脅威を検出し、調査を実行する'
---

# モジュール 7 - ラボ 1 - 演習 6 - 検出を作成する


### タスク 1: Sysmon による攻撃 1 の検出

このタスクでは、セキュリティ イベント コネクタと Sysmon がインストールされているホストで**攻撃 1** の検出を作成します。

1. 管理者として WIN1 仮想マシンにログインします。パスワードは**Pa55w.rd** です。  

2. Microsoft Edge ブラウザーで Azure portal (https://portal.azure.com) に移動します。

3. **サインイン**ダイアログ ボックスで、ラボのホスティングプロバイダーから提供された管理者用の**テナント電子メール**アカウントをコピーして貼り付け、**次へ**を選択します。

4. **パスワードの入力**ダイアログ ボックスで、ラボ ホスティング プロバイダーから提供された管理者用の**テナントパスワード**をコピーして貼り付け、「**サインイン**」 を選択します。

5. Azure portal の検索バーに「*Sentinel*」と入力し、「**Microsoft Sentinel**」を選択します。

6. 先ほど作成した Microsoft Sentinel ワークスペースを選択します。

7. 全般 セクションから**ログ**を選択します。

8. まず、データが保存されている場所を確認する必要があります。攻撃を行ったばかりなので  ログの時間範囲を**過去24時間**に設定します。

9. 次のKQLステートメントを実行します

```KQL
search "temp\\startup.bat"
```

10. 結果は、次の 3 つの異なるテーブルのデータを表示します。
    - DeviceProcessEvents
    - DeviceRegistryEvents
    - Event

    *Device* テーブルは、Defender for Endpoint コネクタに由来します。**Event** テーブルのデータは、エージェント構成を通して接続された Sysmon/Operational Windows Event Logs から入力されます。

    Sysmon と Defender for Endpoint の 2 つの異なるソースからデータを受信しているため、後で結合できる 2 つの KQL ステートメントを作成する必要があります。最初の調査では、それぞれを個別に確認していきます。

    >**注:** まれに、データの読み込みプロセスに通常よりも時間がかかる場合があります。その場合、テーブルがクエリに数時間表示されないことがあります。「*イベント*」テーブルを表示させるだけなら、そのまま続行することができます。

11. 最初のデータソースは、WindowsホストからのSysmonです。以下のKQLステートメントを実行します。

```KQL
search in (Event) "temp\\startup.bat"
```

結果は、イベントテーブルに対してのみ表示されるようになりました。  

12. 行を展開して、レコードに関連するすべての列を表示します。  EventDataやParameterXmlなどのいくつかのフィールドには、構造化データとして保存された複数のデータ項目があります。これにより、特定のフィールドでのクエリが困難になります。  

13. 次に、各行のデータを解析するKQLステートメントを作成して、意味のあるフィールドを作成する必要があります。GitHubの Microsoft Sentinel コミュニティでは、ParsersフォルダーにParsersの例が多数あります。  ブラウザーで新しいタブを開き、以下に移動します**https://github.com/Azure/Azure-Sentinel**

14. **Parsers**フォルダーを選択し、次に**Sysmon**フォルダーを選択します。

15. Sysmon-v12.0.txtファイルを選択し確認します。

    ファイルの先頭に、Eventテーブルをクエリし、EventDataという名前の変数に格納するLetステートメントが表示されます。
    >**ヒント:** 以下のコード スニペットは、手順 16 のクエリをより良く理解するためのもので、コピーしたり実行するものではありません。

```
let EventData = Event
| where Source == "Microsoft-Windows-Sysmon"
| extend RenderedDescription = tostring(split(RenderedDescription, ":")[0])
| project TimeGenerated, Source, EventID, Computer, UserName, EventData, RenderedDescription
| extend EvData = parse_xml(EventData)
| extend EventDetail = EvData.DataItem.EventData.Data
| project-away EventData, EvData  ;
```

ファイルのさらに下に、EventID == 13を調べ、EventData変数を入力として使用している別のletステートメントがあります。
>**ヒント:** 以下のコード スニペットは、手順 16 のクエリをより良く理解するためのもので、コピーしたり実行するものではありません。

```
let SYSMON_REG_SETVALUE_13=()
{
    let processEvents = EventData
    | where EventID == 13
    | extend RuleName = EventDetail.[0].["#text"], EventType = EventDetail.[1].["#text"], UtcTime = EventDetail.[2].["#text"], ProcessGuid = EventDetail.[3].["#text"], 
    ProcessId = EventDetail.[4].["#text"], Image = EventDetail.[5].["#text"], TargetObject = EventDetail.[6].["#text"], Details = EventDetail.[7].["#text"]
    | project-away EventDetail  ;
    processEvents;
    
};
```

16. これは良いスタートのように見えます。上の 2 つのステートメントによって、自分自身の KQL を作成し、イベント テーブル内の Sysmon を使用してすべてのレジストリ キー設定値行を表示させます。次の KQL クエリを実行します。

    >**重要:** どんな間違いも避けるために、どの KQL クエリも最初に*メモ帳*に貼り付け、次に、そこから *New Query 1* ログ ウィンドウにコピーしてください。

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

   ![スクリーンショット](../Media/SC200_sysmon_query1.png)

17. ここから引き続き検出ルールを作成できますが、このKQLステートメントは、他の検出ルールのKQLステートメントで再利用できるように見えます。  「ログ」ウィンドウで、「**保存**」、「**関数として保存**」の順に選択します。[保存] フライアウトで、次のように入力して関数を保存します。

    |設定|値|
    |---|---|
    |関数名|**Event_Reg_SetValue**|
    |カテゴリ|Sysmon|

18. 「**保存**」を選択し、「**+**」記号を選択することにより新しい「ログ クエリ」タブを開きます。そして、以下の KQL ステートメントを実行します:

```KQL
Event_Reg_SetValue
```

19. 現在のデータ収集によっては、多くの行を受け取る可能性があります。これは予測されている結果です。次のタスクは、特定のシナリオにフィルターをかけることです次の KQLステートメントを実行し、特定のレコードを返させ、確認して行を識別するために何を変更できるかを調べることができます。

```KQL
Event_Reg_SetValue | search "startup.bat"
```

20. 脅威インテリジェンスから、脅威アクターがreg.exeを使用してレジストリキーを追加していることがわかります。  ディレクトリはc：\ tempです。startup.batは別の名前にすることができます。次のスクリプトを実行します。

```KQL
Event_Reg_SetValue 
| where Image contains "reg.exe"
```

21. これは良いスタートです  次に、c：\ tempディレクトリの結果のみを返す必要があります。続いて、以下のKQLステートメントを実行します:

```KQL
Event_Reg_SetValue 
| where Image contains "reg.exe"
| where Details startswith "C:\\TEMP"
```

22. アラートについてできるだけ多くのコンテキストを提供することにより、セキュリティ運用アナリストを支援することが重要です。これには、調査グラフで使用するエンティティの投影が含まれます。  次のクエリを実行します。

```KQL
Event_Reg_SetValue 
| where Image contains "reg.exe"
| where Details startswith "C:\\TEMP"
| extend timestamp = TimeGenerated, HostCustomEntity = Computer, AccountCustomEntity = UserName

```

23. 適切な検出ルールができたので、クエリのあるログウィンドウで、コマンド バーの **[新しいアラート ルール]** を選択し、**[Azure Sentinel アラートの作成]** を選択します。

24. これにより、分析ルール　ウィザードが起動します。全般タブに次のように入力します

    |設定|値|
    |---|---|
    |名前|**Sysmon Startup RegKey**|
    |説明|**C:\temp の Sysmon Startup Regkey**|
    |戦術|**永続化**|
    |重要度|**高**|

25. 「**次へ:**」を選択します。**ルール ロジックの設定 >**」を選択します。[**ルール ロジックの設定**] タブで、**ルール クエリ**が既に入力されているはずです。「**-> 現状のデータを使用してテスト**」を選択し、現状の構成で 1 日当たり受信することができるアラートの数を確認します。

26. クエリスケジューリングの場合、次のように設定します。

    |設定|値|
    |---|---|
    |クエリを|5 分|
    |データを最後の|1 日|

    >**注:** 同じデータに対して意図的に多くのインシデントを生成しています。これにより、ラボはこれらのアラートを使用できるようになります。この構成変更により、受信するアラートの数は変わるかも知れません。  「**-> 現状のデータを使用してテスト**」を選択し、変更された構成で 1 日当たり受診することができるアラートの数を確認します。

27. 残りのオプションは既定値のままにします。  「**次へ:**」を選択します。**インシデント設定 >**」ボタンを選択します。

28. 「*インシデントの設定 (プレビュー)*」タブには、これら構成が以下のように設定されていることを確認してください。 

    |設定|値|
    |---|---|
    |インシデントの設定|有効化|
    |アラート グループ|無効化|

29. 「**次へ: 自動応答 >**」ボタンを選択します。「自動応答」タブには、「*Alert automation*」の下の「*PostMessageTeams-OnAlert*」を選択して「**次へ：**」を選択します。「**レビュー**」ボタンを選択します。

30. レビュータブで、**作成**を選択します。


### タスク 2: エンドポイントのDefenderによる攻撃1の検出

このタスクでは、Microsoft Defender for Endpoint が構成されたホストで「**攻撃1**」の検出を作成します。

1. Microsoft Sentinel ポータルで、全般セクションから「**ログ**」を選択します。

2. まず、データが保存されている場所を確認する必要があります。攻撃を実行したばかりなので、ログを「**時間の範囲：過去 24 時間**に設定します。

3. 以下の　KQL　ステートメントを実行します。

```KQL
search "temp\\startup.bat"
```

4. 結果は、次の 3 つの異なるテーブルのデータを示します。
    - DeviceProcessEvents
    - DeviceRegistryEvents
    - Event

    「*デバイス*」テーブルは Defender for Endpoint コネクタからであり、「*エベント*」テーブルは、「エージェント」構成を通して接続される Sysmon/Operational Windows Event ログからのデータを読み込みます。

    SysmonとDefenderforEndpointの2つの異なるソースからデータを受信しているため、  後で結合できる2つのKQLステートメントを作成する必要があります。しかし、最初の調査では、それぞれを個別に確認していきます。

    >**注:** まれに、データの読み込みプロセスに通常よりも時間がかかる場合があります。その場合、テーブルがクエリに数時間表示されないことがあります。タスク 3 を実行し、結果にこの「*デバイス*」テーブルが表示されない場合は、後でこのポイントまで戻ります。

5. この検出は、Defender forEndpointからのデータに焦点を当てます。  以下の　KQL　ステートメントを実行します。

```KQL
search in (Device*) "temp\\startup.bat"
```

6. テーブル--DeviceRegistryEventsは、データがすでに正規化されており、クエリが簡単にできるように見えます。  行を展開して、レコードに関連するすべての列を表示します。

7. 脅威インテリジェンスから、脅威アクターがreg.exeを使用してレジストリキーを追加していることがわかります。  ディレクトリはc：\ tempです。startup.batは別の名前にすることができます。  このKQLステートメントを入力します。

```KQL
DeviceRegistryEvents
| where ActionType == "RegistryValueSet"
| where InitiatingProcessFileName == "reg.exe"
| where RegistryValueData startswith "c:\\temp"
```

8. アラートについてできるだけ多くのコンテキストを提供することにより、セキュリティオペレーションセンターアナリストを支援することが重要です。これには、調査グラフで使用するエンティティの投影が含まれます。次のクエリを実行します。

```KQL
DeviceRegistryEvents
| where ActionType == "RegistryValueSet"
| where InitiatingProcessFileName == "reg.exe"
| where RegistryValueData startswith "c:\\temp"
| extend timestamp = TimeGenerated, HostCustomEntity = DeviceName, AccountCustomEntity = InitiatingProcessAccountName
```

   ![スクリーンショット](../Media/SC200_sysmon_query2.png)

9.  適切な検出ルールができたので、クエリのあるログ ウィンドウで、コマンド バーの **[新しいアラート ルール]** を選択します。  次に、**[Azure Sentinel アラートの作成]** を選択します。

10. これにより、分析ルール　ウィザードが起動します。全般タブに次のように入力します

    |設定|値|
    |---|---|
    |名前|**MDE Startup RegKey**|
    |説明|**C:\temp の MDE Startup Regkey**|
    |戦術|**永続化**|
    |重要度|**高**|

11. 「**次へ:**」を選択します。**ルール ロジックを設定　>**」ボタンを選択します。

12. [ルール ロジックの設定] タブで、**ルール クエリ**が既に入力されているはずです。

13. クエリスケジューリングの場合、次のように設定します。

    |設定|値|
    |---|---|
    |クエリを|5 分|
    |データを最後の|1 日|

    >**注:** 同じデータに対して意図的に多くのインシデントを生成しています。  これにより、ラボはこれらのアラートを使用できるようになります。

14. 残りのオプションは既定値のままにします。  「**次へ:**」を選択します。**インシデントの設定 >**」を選択します。

15. 「*インシデント設定 (プレビュー)*」には、以下を設定します。 

    |設定|値|
    |---|---|
    |インシデントの設定|有効化|
    |アラート グループ|無効化|

16. 「**次へ: 「自動応答 >**」を選択します。「自動応答」タブには、「*Alert automation*」の下の「*PostMessageTeams-OnAlert*」を選択して「**次へ：**」を選択します。「**レビュー**」ボタンを選択します。

17. 確認および作成 タブで、**作成** を選択します。


### タスク 3: SecurityEventによる攻撃2の検出

このタスクでは、セキュリティ イベント コネクタと Sysmon がインストールされているホストで*攻撃 2* の検出を作成します。

1. Microsoft Sentinel ポータルの「全般」セクションで「**ログ**」を選択します。

2. まず、データが保存されている場所を確認する必要があります。攻撃を行ったばかりなので  

    ログの時間範囲を過去24時間に設定します。

3. 以下の　KQL　ステートメントを実行します。

```KQL
search "administrators"
```

4. 結果は次の表を示します。
    - Event
    - SecurityEvent

5. 最初のデータソースはSecurityEventです。特権グループへのメンバーの追加を識別するためにWindowsが使用するイベントIDを調査するときが来ました。私たちが探している EventID およびイベントは、「4732- メンバーはセキュリティが有効なローカル グループに追加されました」です。次のスクリプトを実行して確認します。

```KQL
SecurityEvent
| where EventID == "4732"
| where TargetAccount == "Builtin\\Administrators"
```

6. 行を展開して、レコードに関連するすべての列を表示します。  探しているユーザー名は表示されません。  問題は、ユーザー名を保存する代わりに、セキュリティ識別子 (SID) が保存されるということです。  次のKQLは、SIDを照合して、Administratorsグループに追加されたTargetUserNameにデータを入力しようとします。

```KQL
SecurityEvent
| where EventID == "4732"
| where TargetAccount == "Builtin\\Administrators"
| extend Acct = MemberSid, MachId = SourceComputerId 
| join kind=leftouter (
     SecurityEvent 
     | summarize count() by TargetSid, SourceComputerId, TargetUserName
     | project Acct1 = TargetSid, MachId1 = SourceComputerId, UserName1 = TargetUserName
) on $left.MachId == $right.MachId1, $left.Acct == $right.Acct1 
```

   ![スクリーンショット](../Media/SC200_sysmon_attack3.png)

>**注:** ラボで使用されるデータセットが小さいため、このKQLは期待される結果を返さない場合があります。

7. アラートについてできるだけ多くのコンテキストを提供することにより、セキュリティ運用アナリストを支援することが重要です。これには、調査グラフで使用するエンティティの投影が含まれます。  次のクエリを実行します。

```KQL
SecurityEvent
| where EventID == "4732"
| where TargetAccount == "Builtin\\Administrators"
| extend Acct = MemberSid, MachId = SourceComputerId 
| join kind=leftouter (
     SecurityEvent 
     | summarize count() by TargetSid, SourceComputerId, TargetUserName
     | project Acct1 = TargetSid, MachId1 = SourceComputerId, UserName1 = TargetUserName
) on $left.MachId == $right.MachId1, $left.Acct == $right.Acct1 
| extend timestamp = TimeGenerated, HostCustomEntity = Computer, AccountCustomEntity = UserName1
```

8. 適切な検出ルールができたので、クエリのあるログ ウィンドウで、コマンド バーの **[新しいアラート ルール]** を選択し、**[Azure Sentinel アラートの作成]** を選択します。

9. これにより、分析ルール　ウィザードが起動します。全般タブに次のように入力します

    |設定|値|
    |---|---|
    |名前|**SecurityEvents Local Administrators User Add**|
    |説明|**ユーザーはローカル管理者グループに追加されました**|
    |戦術|**特権エスカレーション**|
    |重要度|**高**|

10. 「**次へ:**」を選択します。**ルール ロジックを設定　>**」ボタンを選択します。ルールロジックの設定タブで、ルールクエリエンティティとマップエンティティが既に入力されている必要があります。

11. クエリスケジューリングの場合、次のように設定します。

    |設定|値|
    |---|---|
    |クエリを|5 分|
    |データを最後の|1 日|

    >**注:** 同じデータに対して意図的に多くのインシデントを生成しています。  これにより、ラボはこれらのアラートを使用できるようになります。

12. 残りのオプションは既定値のままにします。  「**次へ:**」を選択します。**インシデントの設定 >**」を選択します。

13. 「*インシデント設定 (プレビュー)*」には、以下を設定します。

    |設定|値|
    |---|---|
    |インシデントの設定|有効化|
    |アラート グループ|無効化|

14. 「**次へ: 「自動応答 >**」を選択します。「自動応答」タブには、「*Alert automation*」の下の「*PostMessageTeams-OnAlert*」を選択して「**次へ：**」を選択します。「**レビュー**」ボタンを選択します。

15. レビュー タブで、**作成**を選択します。

## 演習 7 に進みます。
