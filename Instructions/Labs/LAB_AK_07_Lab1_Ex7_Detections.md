---
lab:
  title: 演習 7 - 検出を作成する
  module: Module 7 - Create detections and perform investigations using Microsoft Sentinel
---

# <a name="module-7---lab-1---exercise-7---create-detections"></a>モジュール 7 - ラボ 1 - 演習 7 - 検出を作成する

## <a name="lab-scenario"></a>ラボのシナリオ


あなたは、Microsoft Sentinel を実装した会社で働いているセキュリティ運用アナリストです。 Log Analytics KQL クエリを使用し、そこから、環境内の脅威や異常な動作を検出するのに役立つカスタム分析ルールを作成します。

分析ルールでは、環境全体にわたる特定のイベントまたは一連のイベントを検索したり、特定のイベントしきい値または条件に達したときはユーザーに警告したり、SOC でトリアージと調査を行うためのインシデントを生成したり、自動化された追跡および修復プロセスを使用して脅威に対応したりします。


### <a name="task-1-attack-1-detection-with-defender-for-endpoint"></a>タスク 1: Defender for Endpoint を使用した攻撃 1 の検出

このタスクでは、Microsoft Defender for Endpoint が構成されたホスト (Win1) で**攻撃 1** の検出を作成します。

1. Microsoft Sentinel ポータルで、[全般] セクションから **[ログ]** を選択します (このページから移動した場合)。

1. 次の KQL ステートメントをもう一度**実行**して、このデータがあるテーブルを呼び出します。

    ```KQL
    search "temp\\startup.bat"
    ```

1. この検出は、Defender forEndpointからのデータに焦点を当てます。 以下の KQL ステートメントを**実行**します。

    ```KQL
    search in (Device*) "temp\\startup.bat"
    ```

1. テーブル *DeviceRegistryEvents* は、データが既に正規化されており、簡単にクエリを実行できるように見えます。 行を展開して、レコードに関連するすべての列を表示します。

    >**重要:** 結果に *DeviceRegistryEvents* テーブルが表示されない場合は、次の 2 つのクエリの代替手段として、*DeviceProcessEvents* テーブルを代わりに使用します。 つまり、前のクエリに表示されたテーブルに応じて、次に示す 2 つの例のいずれかを使用します。

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

1. アラートについてできるだけ多くのコンテキストを提供することにより、セキュリティオペレーションセンターアナリストを支援することが重要です。 これには、調査グラフで使用するエンティティの投影が含まれます。 次のクエリを**実行**します。

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

1. 適切な検出ルールができたので、[ログ] ウィンドウで、コマンド バーの **[+ 新しいアラート ルール]** を選んでから、 **[Microsoft Sentinel アラートの作成]** を選びます。 これにより、新しいスケジュールされたルールが作成されます。

1. **ヒント:** コマンド バーの省略記号 (...) ボタンを選択する必要がある場合があります。 これで [分析ルール ウィザード] が起動します。

    |*[全般]* タブで、次のように入力します。|設定|
    |---|---|
    |値|名前|
    |**MDE Startup RegKey**|説明|
    |**c:\temp の MDE Startup Regkey**|方針|
    |**永続化**|Severity|

1. **高**

1. **[次へ: ルール ロジックを設定]** ボタンを選択します。

1. *[ルール ロジックの設定]* タブの *[ルール クエリ]* には、 *[アラート エンリッチメント - エンティティ マッピング]* の下のエンティティだけでなく、KQL クエリが既に設定されているはずです。

    |*[クエリのスケジュール設定]* では、次のように設定します。|設定|
    |---|---|
    |値|クエリの実行間隔|
    |5 分|過去のデータを見る|

    >1 日 **注:**  同じデータに対して意図的に多くのインシデントを生成しています。

1. これにより、ラボはこれらのアラートを使用できるようになります。 残りのオプションは既定値のままにします。

1. **[次へ: インシデント設定>]** ボタンを選択します。

1. *[インシデント設定]* タブについては、既定値のままにし、 **[次へ: 自動応答 >]** ボタンを選択します。

1. *[自動応答]* タブでは、 **[アラートのオートメーション (クラシック)]** で *[PostMessageTeams-OnAlert]* を選んでから、 **[次へ: 確認]** をクリックします。


### <a name="task-2-attack-2-detection-with-securityevent"></a>*[確認]* タブで、 **[作成]** ボタンを選択して新しいスケジュール化された分析ルールを作成します。

タスク 2: SecurityEvent を使用した攻撃 2 の検出

1. このタスクでは、セキュリティ イベント コネクタがインストールされているホスト (Win2) で**攻撃 2** の検出を作成します。

1. Microsoft Sentinel ポータルで、[全般] セクションから **[ログ]** を選択します (このページから移動した場合)。

    ```KQL
    search "administrators" | summarize count() by $table
    ```

1. 次の KQL ステートメントを**実行**して、管理者を指すエントリを特定します。 結果には異なるテーブルからのイベントが表示される場合がありますが、ここでは、SecurityEvent テーブルを調査する必要があります。 目的の EventID および Event は "4732 - セキュリティが有効なローカル グループにメンバーが追加されました" です。 これを使用して、特権グループへのメンバーの追加を特定します。

    ```KQL
    SecurityEvent | where EventID == 4732
    | where TargetAccount == "Builtin\\Administrators"
    ```

1. 次の KQL クエリを**実行**して確認します。 行を展開して、レコードに関連するすべての列を表示します。 Administrator として追加されたアカウントのユーザー名は表示されません。 問題は、ユーザー名ではなく、セキュリティ識別子 (SID) が格納されることです。

    ```KQL
    SecurityEvent | where EventID == 4732
    | where TargetAccount == "Builtin\\Administrators"
    | extend Acct = MemberSid, MachId = SourceComputerId  
    | join kind=leftouter (
        SecurityEvent 
        | summarize count() by TargetSid, SourceComputerId, TargetUserName 
        | project Acct1 = TargetSid, MachId1 = SourceComputerId, UserName1 = TargetUserName) on $left.MachId == $right.MachId1, $left.Acct == $right.Acct1
    ```

   ![次の KQL を**実行**して、SID と、Administrators グループに追加されたユーザー名を照合します。](../Media/SC200_sysmon_attack3.png)

    >Screenshot

1. **注:**  ラボで使用されるデータセットが小さいため、このKQLは期待される結果を返さない場合があります。 行を拡張して、結果の列を表示します。最後のものには、KQL クエリ内で ''*投影*'' する *UserName1* 列の下に追加されたユーザーの名前が示されます。 アラートについてできるだけ多くのコンテキストを提供することにより、セキュリティ運用アナリストを支援することが重要です。 これには、調査グラフで使用するエンティティの投影が含まれます。

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

1. 次のクエリを**実行**します。

1. 適切な検出ルールができたので、[ログ] ウィンドウで、コマンド バーの **[+ 新しいアラート ルール]** を選んでから、 **[Microsoft Sentinel アラートの作成]** を選びます。 **ヒント:** コマンド バーの省略記号 (...) ボタンを選択する必要がある場合があります。

    |これで [分析ルール ウィザード] が起動します。|*[全般]* タブで、次のように入力します。|
    |---|---|
    |設定|値|
    |名前|**SecurityEvent Local Administrators User Add**|
    |説明|**ローカル管理者グループに追加されたユーザー**|
    |方針|**特権エスカレーション**|

1. Severity 

1. **高**

1. **[次へ: ルール ロジックを設定]** ボタンを選択します。

    |*[ルール ロジックの設定]* タブの *[ルール クエリ]* には、 *[アラート エンリッチメント - エンティティ マッピング]* の下のエンティティだけでなく、KQL クエリが既に設定されているはずです。|*[クエリのスケジュール設定]* では、次のように設定します。|
    |---|---|
    |設定|値|
    |クエリの実行間隔|5 分|

    >過去のデータを見る 1 日

1. **注:**  同じデータに対して意図的に多くのインシデントを生成しています。 これにより、ラボはこれらのアラートを使用できるようになります。

1. 残りのオプションは既定値のままにします。

1. **[次へ: インシデント設定>]** ボタンを選択します。

1. *[インシデント設定]* タブについては、既定値のままにし、 **[次へ: 自動応答 >]** ボタンを選択します。

## <a name="proceed-to-exercise-8"></a>*[自動応答]* タブでは、 **[アラートのオートメーション (クラシック)]** で *[PostMessageTeams-OnAlert]* を選んでから、 **[次へ: 確認]** をクリックします。
