---
lab:
  title: 演習 9 - ASIM パーサーを作成する
  module: Module 7 - Create detections and perform investigations using Microsoft Sentinel
---

# <a name="module-7---lab-1---exercise-9---create-asim-parsers"></a>モジュール 7 - ラボ 1 - 演習 9 - ASIM パーサーを作成する

## <a name="lab-scenario"></a>ラボのシナリオ

あなたは、Microsoft Sentinel を実装した会社で働いているセキュリティ運用アナリストです。 特定の Windows レジストリ イベントに対して ASIM パーサーをモデル化する必要があります。  これらの簡素化されたパーサーは、後で ASIM パーサー レジストリ イベント正規化標準 (https://docs.microsoft.com/en-us/azure/sentinel/registry-event-normalization-schema) に従って最終処理されます。

>**重要:** このラボでは、長い KQL ASIM パーサー スクリプトを Microsoft Sentinel に入力する必要があります。 これらのスクリプトは、このラボの最初でダウンロードしたファイルで提供されたものです。 また、 https://github.com/MicrosoftLearning/SC-200T00A-Microsoft-Security-Operations-Analyst/tree/master/Allfiles からダウンロードすることもできます。

### <a name="task-1-develop-kql-function-for-microsoft-365-defender-registry-event"></a>タスク 1: Microsoft 365 Defender レジストリ イベント用の KQL 関数を開発する 

このタスクでは、DeviceRegistryEvents のワークスペース パーサーである関数を作成します。 

1. 管理者として WIN1 仮想マシンにログインします。パスワードは**Pa55w.rd**。  

1. Edge ブラウザーで、Azure portal (https://portal.azure.com ) に移動します。

1. **[サインイン]** ダイアログ ボックスで、ラボ ホスティング プロバイダーから提供された**テナントの電子メール** アカウントをコピーして貼り付け、 **[次へ]** を選択します。

1. **[パスワードの入力]** ダイアログ ボックスで、ラボ ホスティング プロバイダーから提供された**テナントのパスワード**をコピーして貼り付け、 **[サインイン]** を選択します。

1. Azure portal の検索バーに「*Sentinel*」と入力し、**[Microsoft Sentinel]** を選択します。

1. 先ほど作成した Microsoft Sentinel ワークスペースを選択します。

1. **[ログ]** ページを選択します。

1. ダウンロードした **SC200_module7_ASIM_Parser_scripts.txt** を開き、*Task 1 Script* の KQL ステートメントをコピーして新しいクエリ タブに貼り付けます。

    >**注:** 以下のスクリプトは参考用としてのみ示されています。KQL クエリの確認のために時間を取ってください。

    ```KQL
    let RegistryType = datatable (TypeCode: string, TypeName: string) [
    "None", "Reg_None",
    "String", "Reg_Sz",
    "ExpandString", "Reg_Expand_Sz",
    "Binary", "Reg_Binary",
    "Dword", "Reg_DWord",
    "MultiString", "Reg_Multi_Sz",
    "QWord", "Reg_QWord"
    ];
    let RegistryEvents_M365D=() {
    DeviceRegistryEvents
    | extend
        // Event
        EventOriginalUid = tostring(ReportId),
        EventCount = int(1), 
        EventProduct = 'M365 Defender for Endpoint',
        EventVendor = 'Microsoft', 
        EventSchemaVersion = '0.1.0', 
        EventStartTime = TimeGenerated, 
        EventEndTime = TimeGenerated, 
        EventType = ActionType,
        // Registry
        RegistryKey = iff (ActionType in ("RegistryKeyDeleted", "RegistryValueDeleted"), PreviousRegistryKey, RegistryKey),
        RegistryValue = iff (ActionType == "RegistryValueDeleted", PreviousRegistryValueName, RegistryValueName),
        // RegistryValueType -- original name is fine
        // RegistryValueData -- original name is fine
        RegistryKeyModified = iff (ActionType == "RegistryKeyRenamed", PreviousRegistryKey, ""),
        RegistryValueModified = iff (ActionType == "RegistryValueSet", PreviousRegistryValueName, ""),
        // RegistryValueTypeModified -- Not provided by Defender
        RegistryValueDataModified = PreviousRegistryValueData
    | lookup RegistryType on $left.RegistryValueType == $right.TypeCode
    | extend RegistryValueType = TypeName
    | project-away
        TypeName,
        PreviousRegistryKey,
        PreviousRegistryValueName,
        PreviousRegistryValueData
    // Device
    | extend
        DvcHostname = DeviceName,
        DvcId = DeviceId,
        Dvc = DeviceName
    // Users
    | extend
        ActorUsername = iff (InitiatingProcessAccountDomain == '', InitiatingProcessAccountName, strcat(InitiatingProcessAccountDomain, '\\', InitiatingProcessAccountName)), 
        ActorUsernameType = iff(InitiatingProcessAccountDomain == '', 'Simple', 'Windows'), 
        ActorUserIdType = 'SID'
    | project-away InitiatingProcessAccountDomain, InitiatingProcessAccountName
    | project-rename
    ActorUserId = InitiatingProcessAccountSid, 
    ActorUserAadId = InitiatingProcessAccountObjectId, 
    ActorUserUpn = InitiatingProcessAccountUpn
    // Processes
    | extend
    ActingProcessId = tostring(InitiatingProcessId), 
    ParentProcessId = tostring(InitiatingProcessParentId) 
    | project-away InitiatingProcessId, InitiatingProcessParentId
    | project-rename
    ParentProcessName = InitiatingProcessParentFileName, 
    ParentProcessCreationTime = InitiatingProcessParentCreationTime, 
    ActingProcessName = InitiatingProcessFolderPath, 
    ActingProcessFileName = InitiatingProcessFileName,
    ActingProcessCommandLine = InitiatingProcessCommandLine, 
    ActingProcessMD5 = InitiatingProcessMD5, 
    ActingProcessSHA1 = InitiatingProcessSHA1, //OK
    ActingProcessSHA256 = InitiatingProcessSHA256, 
    ActingProcessIntegrityLevel = InitiatingProcessIntegrityLevel, 
    ActingProcessTokenElevation = InitiatingProcessTokenElevation, 
    ActingProcessCreationTime = InitiatingProcessCreationTime 
    // -- aliases
    | extend 
    Username = ActorUsername,
    UserId = ActorUserId,
    UserIdType = ActorUserIdType,
    User = ActorUsername,
    CommandLine = ActingProcessCommandLine,
    Process = ActingProcessName
    };
    RegistryEvents_M365D
    ```

1. **[実行]** を選択して、KQL が有効であることを確認します。

1. **[保存]** を選択してから、 **[関数として保存]** を選択します。

1. *[関数として保存]* で、次のように設定します。

    |設定|値|
    |---|---|
    |関数名|vimRegEvtM365D|
    |レガシ カテゴリ|MyASIM|

1. 次に、 **[保存]** を選択します。

1. 新しいクエリ タブで、「**vimRegEvtM365D**」と入力して **[実行]** を選択します。


### <a name="task-2-develop-kql-function-for-securityevent-table"></a>タスク 2: SecurityEvent テーブル用の KQL 関数を開発する。 

このタスクでは、SecurityEvent のワークスペース パーサーである関数を作成します。

1. 新しいクエリ タブを作成します。

1. ダウンロードした **SC200_module7_ASIM_Parser_scripts.txt** に戻り、*Task 2 Script* の KQL ステートメントをコピーして新しいクエリ タブに貼り付けます。

    >**注:** 以下のスクリプトは参考用としてのみ示されています。KQL クエリの確認のために時間を取ってください。

    ```KQL
    let RegistryType = datatable (TypeCode: string, TypeName: string) [
    "%%1872", "Reg_None",
    "%%1873", "Reg_Sz",
    "%%1874", "Reg_Expand_Sz",
    "%%1875", "Reg_Binary",
    "%%1876", "Reg_DWord",
    "%%1879", "Reg_Multi_Sz",
    "%%1883", "Reg_QWord"
    ];
    let RegistryAction = datatable (EventOriginalSubType: string, EventType: string) [
        "%%1904", "RegistryValueSet",
        "%%1905", "RegistryValueSet",      
        "%%1906", "RegistryValueDeleted"             
    ];
    let Hives = datatable (KeyPrefix: string, Hive: string) [
        "MACHINE", "HKEY_LOCAL_MACHINE",
        "USER", "HKEY_USERS",   
    ];
    let RegistryEvents=() {
        SecurityEvent
        // -- Filter
        | where EventID == 4657          
        // Event
        | extend
            EventCount = int(1), 
            EventVendor = 'Microsoft', 
            EventProduct = 'Security Events', 
            EventSchemaVersion = '0.1.0', 
            EventStartTime = todatetime(TimeGenerated), 
            EventEndTime = todatetime(TimeGenerated),
            EventOriginalType = tostring(EventID) 
        | project-rename
            EventOriginalSubType = OperationType,
            EventOriginalUid = EventOriginId
        | lookup RegistryAction on EventOriginalSubType
        // Registry
        // Normalize key hive
        | parse ObjectName with "\\REGISTRY\\" KeyPrefix "\\" Key
        | lookup Hives on KeyPrefix
        | extend RegistryKey = strcat (Hive, "\\", Key)
        | project-away Hive, Key, KeyPrefix, ObjectName
        | project-rename
            RegistryValue = ObjectValueName
        | extend
            RegistryValueData = iff (EventOriginalSubType == "%%1906", OldValue, NewValue), 
            RegistryKeyModified = iff (EventOriginalSubType == "%%1905", RegistryKey, ""),
            RegistryValueModified = iff (EventOriginalSubType == "%%1905", RegistryValue, ""),
            RegistryValueDataModified = iff (EventOriginalSubType == "%%1905", OldValue, "")
        | lookup RegistryType on $left.NewValueType == $right.TypeCode
        | project-rename RegistryValueType = TypeName
        | lookup RegistryType on $left.OldValueType == $right.TypeCode
        | project-rename RegistryValueTypeModified = TypeName
        | project-away OldValue, NewValue, OldValueType, NewValueType
        // Device
        | extend
            DvcId = SourceComputerId,
            DvcHostname = Computer,
            DvcOs = 'Windows'
        // User
        | project-rename
            ActorUserId = SubjectUserSid, 
            ActorSessionId = SubjectLogonId, 
            ActorDomainName = SubjectDomainName
        | extend
            ActorUserIdType = 'SID',
            ActorUsername = iff (ActorDomainName == '-', SubjectUserName, SubjectAccount), 
            ActorUsernameType = iff(ActorDomainName == '-', 'Simple', 'Windows'),
            ActingProcessId = tostring(toint(ProcessId)) 
        // Process 
        | project-rename
            ActingProcessName = ProcessName
        // -- Aliases
        | extend
            User = ActorUsername,
            UserId = ActorUserId,
            Dvc = DvcHostname,
            Process = ActingProcessName
        // -- Remove potentially confusing
        | project-away 
            SubjectUserName,
            SubjectAccount
    };
    RegistryEvents
    ```

1. **[実行]** を選択して、KQL が有効であることを確認します。

1. **[保存]** を選択してから、 **[関数として保存]** を選択します。

1. *[関数として保存]* で、次のように設定します。

    |設定|値|
    |---|---|
    |関数名|vimRegEvtSecurityEvent|
    |レガシ カテゴリ|MyASIM|

1. 次に、 **[保存]** を選択します。

1. 新しいクエリ タブで、「**vimRegEvtSecurityEvent**」と入力して **[実行]** を選択します。


### <a name="task-3-create-a-unifying-workspace-parser"></a>タスク 3: 統一ワークスペース パーサーを作成する。 

このタスクでは、前の 2 つの関数を組み合わせた統一パーサー関数を作成します。  

1. 新しいクエリ タブを作成します。

1. 新しいクエリ タブに、次の KQL ステートメントを入力します。

    ```KQL
    union isfuzzy=true
    vimRegEvtM365D,
    vimRegEvtSecurityEvent
    ```

1. **[実行]** を選択して、KQL が有効であることを確認します。

1. **[保存]** を選択してから、 **[関数として保存]** を選択します。

1. *[関数として保存]* で、次のように設定します。

    |設定|値|
    |---|---|
    |関数名|imRegEvt|
    |レガシ カテゴリ|MyASIM|

1. 次に、 **[保存]** を選択します。

1. 新しいクエリ タブで、「**imRegEvt**」と入力して **[実行]** を選択します。

1. クエリを以下に更新して **[実行]** を選択します。

    ```KQL
    imRegEvt
    | where ActionType == 'RegistryValueSet'
    ```

## <a name="proceed-to-exercise-10"></a>演習 10 に進む

