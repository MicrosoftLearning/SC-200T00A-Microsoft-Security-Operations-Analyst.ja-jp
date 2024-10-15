# モジュール 6 Microsoft Sentinel を使用して検出を作成し、調査を実行する

**注**: このデモを正常に完了するには、[前提条件ドキュメント](00-prerequisites.md)のすべての手順を完了する必要があります。

**重要:** VTD-5002-FY25 では、このデモは必要ありません。

## NRT クエリ ルールを作成する

このタスクでは、NRT (ほぼリアルタイム) 分析クエリ ルールを作成します。

1. Microsoft Sentinel で *[構成]* の **[分析]** ページを選択します。

1. **[作成]** タブを選択し、**[NRT クエリ ルール]** を選択します。

1. これで [分析ルール ウィザード] が起動します。 *[全般]* タブで、次のように入力します。

    |設定|値|
    |---|---|
    |名前|**NRT PowerShell ハント**|
    |説明|**NRT PowerShell ハント**|
    |戦術と手法|**コマンドとコントロール**|
    |Severity|**高**|

1. **[次へ: ルール ロジックを設定]** ボタンを選択します。 

1. *[ルール クエリ]* に次の KQL ステートメントを入力します。

    ```KQL
    let lookback = 2d; 
    SecurityEvent 
    | where TimeGenerated >= ago(lookback) 
    | where EventID == 4688 and Process =~ "powershell.exe"
    | extend PwshParam = trim(@"[^/\\]*powershell(.exe)+" , CommandLine) 
    | project TimeGenerated, Computer, SubjectUserName, PwshParam 
    | summarize min(TimeGenerated), count() by Computer, SubjectUserName, PwshParam
    ```

1. **[クエリ結果の表示 >]** を選択して、クエリにエラーがないことを確認します。

1. ウィンドウの右上にある **[X]** を選択して *[ログ]* ウィンドウを閉じ、 **[OK]** を選択して変更を破棄します。 

1. *[結果のシミュレーション]* の **[現在のデータでテストする]** を選択します。 *[1 日あたりのアラート]* の予想される数に注目してください。

1. *[エンティティ マッピング]* で、次のように選択します。

    - *[エンティティの種類]* ドロップダウン リストで、**[ホスト]** を選択します。
    - *[識別子]* ドロップダウン リストで、**[HostName]** を選択します。
    - *[値]* ドロップダウン リストで、 **[コンピューター]** を選択します。

1. 下にスクロールし、 **[次へ: インシデント設定>]** ボタンを選択します。

1. *[インシデント設定]* タブについては、既定値のままにし、**[次へ: 自動応答 >]** ボタンを選択します。

1. **[次へ: 確認と作成 >]** を選択します。

1. *[確認と作成]* タブで、 **[保存]** ボタンを選択して、新しいスケジュール化された分析ルールを作成して保存します。

## Azure Monitor エージェント (AMA) で構成された攻撃の検出 Windows

このタスクでは、作成した `NRT` ルールから作成されたインシデントを調査します。

1. 管理者として WIN1 仮想マシンにログインします。パスワードは**Pa55w.rd**。  

1. Edge ブラウザーで、Azure portal (https://portal.azure.com ) に移動します。

1. **サインイン** ダイアログ ボックスで、ラボのホスティングプロバイダーから提供された管理者用の**テナント電子メール** アカウントをコピーして貼り付け、 **[次へ]** を選択します。

1. **パスワードの入力**ダイアログ ボックスで、ラボ ホスティング プロバイダーから提供された管理者用の**テナントパスワード**をコピーして貼り付け、 **[サインイン]** を選択します。

1. Azure portal の検索バーに「*Sentinel*」と入力してから、**[Microsoft Sentinel]** を選択します。

1. 先ほど作成した Microsoft Sentinel ワークスペースを選択します。

1. `Microsoft Sentinel` で、`Threat management` メニュー セクションに移動し、**[インシデント]** を選択します

**注** `Incident` が表示されるまで、数分かかることがあります。

1. 作成した `NRT` ルールで構成した `Severity` と `Title` に一致するインシデントが表示されます

1. `Incident` を選択すると、`detail` ウィンドウが開きます

1. **[詳細の表示]** を選択し、**[調査]** ボタンを選択します。

1. その後のインシデントとの `Entities` 関連性 `NRT PowerShell Hunt` を探る。

1. ウインドウの右上隅の **[X]** を選択して、`Investigation` ウィンドウを閉じます。

1. `Logs` タブを選択し、次の KQL ステートメントを入力します。

    ```KQL
    let lookback = 2d; 
    SecurityEvent 
    | where TimeGenerated >= ago(lookback) 
    | where EventID == 4688 and Process =~ "powershell.exe"
    | extend PwshParam = trim(@"[^/\\]*powershell(.exe)+" , CommandLine) 
    | project TimeGenerated, Computer, SubjectUserName, PwshParam 
    | summarize min(TimeGenerated), count() by Computer, SubjectUserName, PwshParam
    ```

**注** このクエリは `Queries History` にあるので、そこから**実行**できます。

1. **[完了]** ボタンを選択して `Logs` ウィンドウを閉じます。

1. ウインドウの右上隅で **[X]** を選択して、`Incident` ウィンドウを閉じます。

## デモが完了しました
