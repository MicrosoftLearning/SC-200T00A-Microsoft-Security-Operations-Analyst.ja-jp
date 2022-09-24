---
lab:
  title: 演習 7 - 検出を作成する
  module: Module 7 - Create detections and perform investigations using Microsoft Sentinel
---

# <a name="module-7---lab-1---exercise-7---create-detections"></a>モジュール 7 - ラボ 1 - 演習 7 - 検出を作成する

## <a name="lab-scenario"></a>ラボのシナリオ


You are a Security Operations Analyst working at a company that implemented Microsoft Sentinel. You are going to work with Log Analytics KQL queries and from there, you will create custom analytics rules to help discover threats and anomalous behaviors in your environment.

分析ルールでは、環境全体にわたる特定のイベントまたは一連のイベントを検索したり、特定のイベントしきい値または条件に達したときはユーザーに警告したり、SOC でトリアージと調査を行うためのインシデントを生成したり、自動化された追跡および修復プロセスを使用して脅威に対応したりします。


### <a name="task-1-attack-1-detection-with-defender-for-endpoint"></a>タスク 1: Defender for Endpoint を使用した攻撃 1 の検出

このタスクでは、Microsoft Defender for Endpoint が構成されたホストで**攻撃 1** の検出を作成します。

1. Microsoft Sentinel ポータルで、[全般] セクションから **[ログ]** を選択します (このページから移動した場合)。

1. 次の KQL ステートメントをもう一度**実行**して、このデータがあるテーブルを呼び出します。

    ```KQL
    search "temp\\startup.bat"
    ```

1. This detection will focus on data from Defender for Endpoint. <bpt id="p1">**</bpt>Run<ept id="p1">**</ept> the following KQL Statement:

    ```KQL
    search in (Device*) "temp\\startup.bat"
    ```

1. The table <bpt id="p1">*</bpt>DeviceRegistryEvents<ept id="p1">*</ept> looks to have the data already normalized and easy for us to query. Expand the row to see all the columns related to the record.

    ><bpt id="p1">**</bpt>Important:<ept id="p1">**</ept> If you do not see the <bpt id="p2">*</bpt>DeviceRegistryEvents<ept id="p2">*</ept> table in the results, an alternative for the following queries is to use the <bpt id="p3">*</bpt>DeviceProcessEvents<ept id="p3">*</ept> table as replacement. Being that said, use one of the two provided examples below.

1. 結果から、脅威アクターが reg.exe を使用してレジストリ キーにキーを追加し、プログラムが C:\temp にあることがわかりました。次のステートメントを**実行**し、クエリの *search* 演算子を *where* 演算子に置き換えます。

    ```KQL
    DeviceRegistryEvents | where ActionType == "RegistryValueSet"
    | where InitiatingProcessFileName == "reg.exe"
    | where RegistryValueData startswith "c:\\temp"
    ```

1. または、*DeviceProcessEvents* テーブルを使用して、次の KQL クエリを**実行**することもできます。

    ```KQL
    DeviceProcessEvents | where ActionType == "ProcessCreated"
    | where FileName == "reg.exe"
    | where ProcessCommandLine contains "c:\\temp"
    ```

1. あなたは、Microsoft Sentinel を実装した会社で働いているセキュリティ運用アナリストです。

    ```KQL
    DeviceRegistryEvents
    | where ActionType == "RegistryValueSet"
    | where InitiatingProcessFileName == "reg.exe"
    | where RegistryValueData startswith "c:\\temp"
    | extend timestamp = TimeGenerated, HostCustomEntity = DeviceName, AccountCustomEntity = InitiatingProcessAccountName
    ```

   ![Screenshot](../Media/SC200_sysmon_query2.png)

1. または、*DeviceProcessEvents* テーブルを使用して、次の KQL クエリを**実行**することもできます。

    ```KQL
    DeviceProcessEvents | where ActionType == "ProcessCreated"
    | where FileName == "reg.exe"
    | where ProcessCommandLine contains "c:\\temp"
    | extend timestamp = TimeGenerated, HostCustomEntity = DeviceName, AccountCustomEntity = InitiatingProcessAccountName
    ```

1. Log Analytics KQL クエリを使用し、そこから、環境内の脅威や異常な動作を検出するのに役立つカスタム分析ルールを作成します。

1. This starts the "Analytics rule wizard". For the <bpt id="p1">*</bpt>General<ept id="p1">*</ept> tab type:

    |設定|[値]|
    |---|---|
    |名前|**MDE Startup RegKey**|
    |説明|**c:\temp の MDE Startup Regkey**|
    |方針|**永続化**|
    |Severity|**高**|

1. **[次へ: ルール ロジックを設定]** ボタンを選択します。

1. *[ルール ロジックの設定]* タブの *[ルール クエリ]* には、 *[アラート エンリッチメント - エンティティ マッピング]* の下のエンティティだけでなく、KQL クエリが既に設定されているはずです。

1. *[クエリのスケジュール設定]* では、次のように設定します。

    |設定|値|
    |---|---|
    |クエリの実行間隔|5 分|
    |過去のデータを見る|1 日|

    ><bpt id="p1">**</bpt>Note:<ept id="p1">**</ept> We are purposely generating many incidents for the same data. This enables the Lab to use these alerts.

1. Leave the rest of the options with the defaults. Select <bpt id="p1">**</bpt>Next: Incident settings&gt;<ept id="p1">**</ept> button.

1. *[インシデント設定]* タブについては、既定値のままにし、 **[次へ: 自動応答 >]** ボタンを選択します。

1. *[自動応答]* タブでは、 *[アラートの自動化]* で **[PostMessageTeams-OnAlert]** を選んでから、 **[次へ: Review]\(次へ: 確認\)** をクリックします。

1. *[確認]* タブで、 **[作成]** ボタンを選択して新しいスケジュール化された分析ルールを作成します。


### <a name="task-2-attack-2-detection-with-securityevent"></a>タスク 2: SecurityEvent を使用した攻撃 2 の検出

このタスクでは、セキュリティ イベント コネクタがインストールされているホストで**攻撃 2** の検出を作成します。

1. Microsoft Sentinel ポータルで、[全般] セクションから **[ログ]** を選択します (このページから移動した場合)。

1. 次の KQL ステートメントを**実行**して、管理者を指すエントリを特定します。

    ```KQL
    search "administrators" | summarize count() by $table
    ```

1. The result might show events from different tables, but in our case, we want to investigate the SecurityEvent table. The EventID and Event that we are looking is "4732 - A member was added to a security-enabled local group". With this, we will identify adding a member to a privileged group. <bpt id="p1">**</bpt>Run<ept id="p1">**</ept> the following KQL query to confirm:

    ```KQL
    SecurityEvent | where EventID == 4732
    | where TargetAccount == "Builtin\\Administrators"
    ```

1. Expand the row to see all the columns related to the record. The username of the account added as Administrator does not show. The issue is that instead of storing the username, we have the Security IDentifier (SID). <bpt id="p1">**</bpt>Run<ept id="p1">**</ept> the following KQL to match the SID to the username that was added to the Administrators group:

    ```KQL
    SecurityEvent | where EventID == 4732
    | where TargetAccount == "Builtin\\Administrators"
    | extend Acct = MemberSid, MachId = SourceComputerId  
    | join kind=leftouter (
        SecurityEvent 
        | summarize count() by TargetSid, SourceComputerId, TargetUserName 
        | project Acct1 = TargetSid, MachId1 = SourceComputerId, UserName1 = TargetUserName) on $left.MachId == $right.MachId1, $left.Acct == $right.Acct1
    ```

   ![Screenshot](../Media/SC200_sysmon_attack3.png)

    >**注:**  ラボで使用されるデータセットが小さいため、このKQLは期待される結果を返さない場合があります。

1. Extend the row to show the resulting columns, in the last one, we see the name of the added user under the <bpt id="p1">*</bpt>UserName1<ept id="p1">*</ept> column we <bpt id="p2">*</bpt>project<ept id="p2">*</ept> within the KQL query. It is important to help the Security Operations Analyst by providing as much context about the alert as you can. This includes projecting Entities for use in the investigation graph. <bpt id="p1">**</bpt>Run<ept id="p1">**</ept> the following query:

    ```KQL
    SecurityEvent | where EventID == 4732
    | where TargetAccount == "Builtin\\Administrators"
    | extend Acct = MemberSid, MachId = SourceComputerId  
    | join kind=leftouter (
        SecurityEvent 
        | summarize count() by TargetSid, SourceComputerId, TargetUserName 
        | project Acct1 = TargetSid, MachId1 = SourceComputerId, UserName1 = TargetUserName) on $left.MachId == $right.MachId1, $left.Acct == $right.Acct1
    | extend timestamp = TimeGenerated, HostCustomEntity = Computer, AccountCustomEntity = UserName1
    ```

1. 適切な検出ルールができたので、[ログ] ウィンドウで、コマンド バーの **[+ 新しいアラート ルール]** を選んでから、 **[Microsoft Sentinel アラートの作成]** を選びます。

1. この検出は、Defender forEndpointからのデータに焦点を当てます。

    |設定|[値]|
    |---|---|
    |名前|**SecurityEvent Local Administrators User Add**|
    |説明|**ローカル管理者グループに追加されたユーザー**|
    |方針|**特権エスカレーション**|
    |Severity|**高**|

1. **[次へ: ルール ロジックを設定]** ボタンを選択します。 

1. *[ルール ロジックの設定]* タブの *[ルール クエリ]* には、 *[アラート エンリッチメント - エンティティ マッピング]* の下のエンティティだけでなく、KQL クエリが既に設定されているはずです。

1. *[クエリのスケジュール設定]* では、次のように設定します。

    |設定|値|
    |---|---|
    |クエリの実行間隔|5 分|
    |過去のデータを見る|1 日|

    >以下の KQL ステートメントを**実行**します。

1. Leave the rest of the options with the defaults. Select <bpt id="p1">**</bpt>Next: Incident settings&gt;<ept id="p1">**</ept> button.

1. *[インシデント設定]* タブについては、既定値のままにし、 **[次へ: 自動応答 >]** ボタンを選択します。

1. *[自動応答]* タブでは、 *[アラートの自動化]* で **[PostMessageTeams-OnAlert]** を選んでから、 **[次へ: Review]\(次へ: 確認\)** をクリックします。

1. *[確認]* タブで、 **[作成]** ボタンを選択して新しいスケジュール化された分析ルールを作成します。

## <a name="proceed-to-exercise-8"></a>演習 8 に進む
