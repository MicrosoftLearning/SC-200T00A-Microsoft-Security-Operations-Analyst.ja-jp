---
lab:
  title: 演習 11 - Microsoft Sentinel でリポジトリを使用する
  module: Module 7 - Create detections and perform investigations using Microsoft Sentinel
---

# <a name="module-7---lab-1---exercise-11---use-repositories-in-microsoft-sentinel"></a>モジュール 7 - ラボ 1 - 演習 11 - Microsoft Sentinel でリポジトリを使用する

## <a name="lab-scenario"></a>ラボのシナリオ

You are a Security Operations Analyst working at a company that implemented Microsoft Sentinel. You already created Scheduled and Microsoft Security Analytics rules.  You need to centralize analytical rules in an Azure DevOps repository.  Then connect Sentinel to the Azure DevOps repository and import the content. 


### <a name="task-1-create-and-export-an-analytical-rule"></a>タスク 1:分析ルールを作成してエクスポートする

このタスクでは、Microsoft Sentinel でエンティティ行動分析を有効にします。

1. 管理者として WIN1 仮想マシンにログインします。パスワードは**Pa55w.rd**。  

1. **[サインイン]** ダイアログ ボックスで、ラボ ホスティング プロバイダーから提供された**テナントの電子メール** アカウントをコピーして貼り付け、 **[次へ]** を選択します。

1. **[パスワードの入力]** ダイアログ ボックスで、ラボ ホスティング プロバイダーから提供された**テナントのパスワード**をコピーして貼り付け、 **[サインイン]** を選択します。

1. Azure portal の検索バーに「*Sentinel*」と入力し、**[Microsoft Sentinel]** を選択します。

1. Microsoft Sentinel ワークスペースを選択します。

1. 構成領域から **[分析]** を選択します。

1. **[+ 作成]** ボタンを選択してから、 **[スケジュールされたクエリ ルール]** を選びます。

1. 分析ルール ウィザードの [全般] タブで、「**Rule from Azure DevOps**」という名前を入力します。

1. [戦術] では、 **[永続化]** を選択します。

1. [重要度] では、 **[低]** を選択します。

1. **[次へ: ルール ロジックを設定 >]** ボタンを選択します。

1. ルールクエリの場合は、次のKQLステートメントを貼り付けます。

    ><bpt id="p1">**</bpt>Warning:<ept id="p1">**</ept> When using the Paste function to the virtual machine extra (pipe) characters could be added. Make sure you use Notepad first to paste the following query.

    ```KQL
    SecurityEvent | where EventID == 4732
    ```

1. Select <bpt id="p1">**</bpt>View query results<ept id="p1">**</ept>. You should not receive any results nor any errors. If you receive an error, please review that the query appears just like the previous KQL statement. Close the <bpt id="p1">*</bpt>Logs<ept id="p1">*</ept> window by selecting the upper right <bpt id="p2">**</bpt>X<ept id="p2">**</ept> and select <bpt id="p3">**</bpt>OK<ept id="p3">**</ept> to discard to save changes to go back to the wizard.


1. 下にスクロールし、 *[クエリのスケジュール設定]* で次のように設定します。

    |設定|値|
    |---|---|
    |クエリの実行間隔|5 分|
    |過去のデータを見る|1 日|

    ><bpt id="p1">**</bpt>Note:<ept id="p1">**</ept> We are purposely generating many incidents for the same data. This enables the Lab to use these alerts.

1. *[アラートのしきい値]* 領域では、アラートですべてのイベントを登録するため、値はそのままにしておきます。

1. *[イベントのグループ化]* 領域では、 **[すべてのイベントを単一のアラートにグループ化する]** オプションを選択したままにしておきます。これは、クエリから、上記の指定されたアラートのしきい値よりも多くの結果が返される場合に限り、実行するたびに単一のアラートを生成する必要があるためです。

1. 下部にある **[次: インシデント設定 >]** ボタンを選択します。 

1. 下部にある **[次: 自動応答 >]** ボタンを選択します。

1. 下部にある **[次: 確認 >]** ボタンを選択します。
 
1. **［作成］** を選択します

1. 作成したルールを選択し、ツール バーから **[エクスポート]** を選択します。

1. 作成したルールを選択し、 **[削除]** を選択します

### <a name="task-2-create-our-azure-devops-environment"></a>タスク 2:Azure DevOps 環境を作成する

このタスクでは、Azure DevOps リポジトリの作成と設定をテストします。

1. ブラウザーで別のタブを開きます
1. https://devops.azure.com に移動します
1. **[Azure DevOps へのサインイン]** リンクを選択します
1. *[We need a few more details]\(詳細情報をいくつか入力する必要があります\)* ページで、 **[続行]** を選びます。
1. *[Azure DevOps の使用を開始する]* ページで、**[続行]** を選択します。
1. あなたは、Microsoft Sentinel を実装した会社で働いているセキュリティ運用アナリストです。  

1. *"表示される文字を入力し"* 、 **[続行]** します。
1. あなたはスケジュール済みおよび Microsoft セキュリティ分析ルールを既に作成しています。
1. **[リポジトリ]** に移動します。
1. ページの下部にある *[Initialize main branch with a README or gitignore]\(README または gitignore を使用してメイン ブランチを初期化する\)* 領域で、 **[初期化]** を選択します。
1. Azure DevOps リポジトリで分析ルールを一元化する必要があります。
1. 次に、Sentinel を Azure DevOps リポジトリに接続し、コンテンツをインポートします。
1. **[ファイルのアップロード]** を選択します
1. **[参照]** を選択し、 *"ダウンロード"* ディレクトリからファイル **Azure_Sentinel_analytic_rule.json** を選択します。
1. **[コミット]** を選択します。
1. 
1. Select <bpt id="p1">**</bpt>Azure DevOps<ept id="p1">**</ept> on the top left corner of the page.  This display your organization and projects.
1. ページの左下にある **[組織の設定]** を選択します。
1. *[セキュリティ]* 領域で **[ポリシー]** を選択します。
1. *[アプリケーション接続ポリシー]* 領域で *[OAuth を使用したサード パーティ アプリケーションのアクセス]* を **[オン]** にします。


### <a name="task-3-connect-sentinel-to-azure-devops"></a>タスク 3:Sentinel を Azure DevOps に接続する。

1. ブラウザーで *[Azure portal]* / *[Microsoft Sentinel]* タブを選択します。
1. Microsoft Sentinel で、 *[コンテンツ管理]* セクションの **[リポジトリ]** を選択します。
1. ツール バーから **[Add mew]\(mew の追加\)** を選択します。
1. 名前に「**My Content**」と入力します。
1. ソース管理に対して、 **[Azure DevOps]** を選択します。
1. Select <bpt id="p1">**</bpt>Authorize<ept id="p1">**</ept>.  Then <bpt id="p1">**</bpt>Accept<ept id="p1">**</ept>.
1. 先ほど作成した組織を選択します。
1. 先ほど作成したプロジェクトを選択します。
1. 先ほど作成したリポジトリを選択します。
1. **main** ブランチを選択します。
1. すべてのコンテンツ タイプを選択します。
1. **[作成]** を選択します。


1. On the Repositories page, select <bpt id="p1">**</bpt>Refresh<ept id="p1">**</ept>.  Wait until <bpt id="p1">*</bpt>Last deployment status<ept id="p1">*</ept> is <bpt id="p2">*</bpt>Failed<ept id="p2">*</ept>.  

><bpt id="p1">**</bpt>Important:<ept id="p1">**</ept> The <bpt id="p2">*</bpt>Failed<ept id="p2">*</ept> status is due to limitations in the hosted lab environment. You would normally see <bpt id="p1">*</bpt>Succeeded<ept id="p1">*</ept>. Then you can see in the <bpt id="p1">*</bpt>Analytics<ept id="p1">*</ept> the imported rule <bpt id="p2">*</bpt>Rule from Azure DevOps<ept id="p2">*</ept>.


## <a name="you-have-completed-the-lab"></a>これでラボは完了です。
