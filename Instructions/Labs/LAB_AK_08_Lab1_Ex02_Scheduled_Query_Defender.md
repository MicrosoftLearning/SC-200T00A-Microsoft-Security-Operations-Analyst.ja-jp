---
lab:
  title: 演習 2 - テンプレートからスケジュールされたクエリを作成する
  module: Learning Path 8 - Create detections and perform investigations using Microsoft Sentinel
  description: このタスクでは、Azure Activity データ コネクタを接続し、スケジュールされたクエリをテンプレートから作成します。
  duration: 45 minutes
  level: 200
  islab: true
  primarytopics:
    - Azure
    - Microsoft Sentinel
---

# ラーニング パス 8 - ラボ 1 - 演習 2 - テンプレートからスケジュールされたクエリを作成する

## ラボのシナリオ

あなたは Microsoft Sentinel を実装した企業で働いているセキュリティ運用アナリストです。 Azure Sentinel を使って脅威を検出および軽減する方法を学習する必要があります。 データ ソースを Microsoft Sentinel に接続した後、環境内の脅威や異常な動作を検出するのに役立つカスタム分析ルールを作成します。

分析ルールでは、環境全体にわたる特定のイベントまたは一連のイベントを検索したり、特定のイベントしきい値または条件に達したときはユーザーに警告したり、SOC でトリアージと調査を行うためのインシデントを生成したり、自動化された追跡および修復プロセスを使用して脅威に対応したりします。

>**重要:** ラーニング パス #8 のラボ演習は、*スタンドアロン*環境にあります。 ラボを完了せずに終了する場合は、構成を再実行する必要があります。

### このラボの推定所要時間: 45 分

>**注:** Microsoft Sentinel は既に、あなたの Azure サブスクリプション内に **sentinelworkspace-01** という名前で事前デプロイされており、*Azure Activity* ソリューションとデータ コネクタのインストールと接続が完了しています。

<!--- To successfully complete this task you will need to complete the following prerequisite tasks.

### Prerequisite task: Connect the Azure Activity data connector

In this task, you will connect the *Azure Activity* data connector.

1. In the Microsoft Sentinel navigation menu, scroll down to the *Content management* section and select **Content Hub**.

1. In the *Content hub*, search for the **Azure Activity** solution and select it from the list.

1. On the *Azure Activity* solution details page select **Manage**.

1. Select the *Azure Activity* Data connector and select **Open connector page**.

1. In the *Configuration* area under the *Instructions* tab, scroll down to "2. Connect your subscriptions...", and select **Launch Azure Policy Assignment Wizard>**.

1. In the **Basics** tab, select the ellipsis button (...) under **Scope** and select your *MOC Subscription-XXXXXXXXXXX* subscription from the drop-down list and click **Select**.

    >**Note:** *Do not* select an optional Resource Group.

1. Select the **Parameters** tab, choose your *sentinelworkspace-01* workspace from the **Primary Log Analytics workspace** drop-down list. This action will apply the subscription configuration to send the information to the Log Analytics workspace.

1. Select the **Remediation** tab and select the **Create a remediation task** checkbox. This action will apply the policy to existing Azure resources.

1. Select the **Review + Create** button to review the configuration.

1. Select **Create** to finish.

1. Please wait for the *Azure Activity* data connector to display a *Connected* status before proceeding. --->

### タスク 1: スケジュールされたクエリ ルールを作成する

このタスクでは、*Microsoft Sentinel 分析のスケジュールされたクエリ ルール*を作成します。

1. 管理者として WIN1 仮想マシンにログインします。パスワードは**Pa55w.rd**。  

1. Microsoft Edge ブラウザーを開きます。

1. Edge ブラウザーで、Defender XDR (`https://security.microsoft.com`) に移動します。

1. **[サインイン]** ダイアログ ボックスで、ラボ ホスティング プロバイダーから提供された**テナントの電子メール** アカウントをコピーして貼り付け、**[次へ]** を選択します。

1. **[パスワードの入力]** ダイアログ ボックスで、ラボ ホスティング プロバイダーから提供された**テナントパスワード**をコピーして貼り付け、**[サインイン]** を選択します。

    >**注:**  パスワードの代わりに "一時アクセス パス" (TAP) を入力するように求められる場合があります。** これはリソース タブにも表示されます。TAP を入力する画面が表示された場合は、値をコピーして貼り付けて **[サインイン]** を選択してください。

1. Microsoft Defender のナビゲーション メニューで、下スクロールして **[Microsoft Sentinel]** セクションを展開します。

1. **[構成]** セクションを展開して **[分析]** を選択します。

1. コマンド バーの [規則のテンプレート] タブにいることを確認し、 **[New CloudShell User] (新しい CloudShell ユーザー)** 規則を検索します。**

1. ルールの概要ブレードで、 *[データ ソース: Azure アクティビティ]* の下にある緑色のアイコンを調べて、データを受信していることを確認します。

    >**注:** 接続状態として表示されておらず、上記の*前提条件タスク*を実行した場合は、プロセスが完了するまで長く待つ必要がある場合があります。

1. **[ルールの作成]** を選んで続けます。

1. 分析ルール ウィザードの [全般] タブで、[重大度] を **[中]** に変更します。** **

1. **[次へ: ルール ロジックを設定 >]** ボタンを選択します。

1. ルール クエリで、 **[クエリ結果の表示]** を選びます。 結果やエラーは表示されないはずです。

1. 右上の **[X]** を選択して *[ログ]* ウィンドウを閉じ、 **[OK]** を選択して変更を破棄して保存し、ウィザードに戻ります。

1. 下にスクロールし、 *[クエリのスケジュール設定]* で次のように設定します。

    |設定|値|
    |---|---|
    |クエリの実行間隔|5 分|
    |次の時間分の過去のデータを参照します|1 日|

    >**注:**  同じデータに対して意図的に多くのインシデントを生成しています。 これにより、ラボはこれらのアラートを使用できるようになります。

1. *[アラートのしきい値]* 領域では、アラートですべてのイベントを登録するため、値はそのままにしておきます。

1. *[イベントのグループ化]* 領域では、 **[すべてのイベントを単一のアラートにグループ化する]** オプションを選択したままにしておきます。これは、クエリから、上記の指定されたアラートのしきい値よりも多くの結果が返される場合に限り、実行するたびに単一のアラートを生成する必要があるためです。

1. 下部にある **[次: インシデント設定 >]** ボタンを選択します。

1. *[インシデント設定]* タブで、既定のオプションを確認します。

1. 下部にある **[次: 自動応答 >]** ボタンを選択します。

1. **[次へ: 確認と作成 >]** ボタンを選択します。
  
1. **[保存]** を選択します。

### タスク 2: 新しいルールを編集する

1. Microsoft Defender のナビゲーション メニューで、下スクロールして **[Microsoft Sentinel]** セクションを展開します。

1. **[構成]** セクションを展開して **[分析]** を選択します。

1. コマンド バーの *[アクティブな規則]* タブにいることを確認したうえで、**[新しい CloudShell ユーザー]** 規則を選択します。

1. この規則を右クリックし、*ポップアップ* メニューから **[編集]** を選択します。

1. **[次へ: ルール ロジックを設定 >]** ボタンを選択します。

1. 下部にある **[次: インシデント設定 >]** ボタンを選択します。

1. 下部にある **[次: 自動応答 >]** ボタンを選択します。

1. *[オートメーション ルール]* の下の *[自動応答]* タブで、**[新規追加]** を選択します。

1. *[Automation ルール名]* に「**Tier 2**」と入力します。

1. *[アクション]* で、 **[所有者の割り当て]** を選択します。

1. 次に、 **[自分に割り当てる]** を選択します。

1. **[適用]** を選択します

1. **[次へ: 確認と作成 >]** ボタンを選択します。
  
1. **[保存]** を選択します。

### タスク 3: 新しいルールをテストする

このタスクでは、新しくスケジュールされたクエリ ルールをテストします。 まず、Azure portal で *Cloud Shell* を有効にします。これで、前のタスクで作成したルールがトリガーされてインシデントが生成されます。

1. Microsoft Edge ブラウザーで、Azure portal (`https://portal.azure.com` ) に移動します。

1. **サインイン** ダイアログ ボックスで、ラボ ホスティング プロバイダーから提供された**テナントの電子メール** アカウントをコピーして貼り付け、**[次へ]** を選択します。

1. **[パスワードの入力]** ダイアログ ボックスで、ラボ ホスティング プロバイダーから提供された**テナントパスワード**をコピーして貼り付け、**[サインイン]** を選択します。

    >**注:**  パスワードの代わりに "一時アクセス パス" (TAP) を入力するように求められる場合があります。** これはリソース タブにも表示されます。TAP を入力する画面が表示された場合は、値をコピーして貼り付けて **[サインイン]** を選択してください。

1. Azure portal のメニュー バーで、*Cloud Shell* に対応するアイコン **>_** を選びます。 ディスプレイの解像度が低すぎる場合は、最初に省略記号アイコン **[...]** の選択が必要な場合があります。

1. *[Azure Cloud Shell へようこそ]* ウィンドウで **[PowerShell]** を選択します。

1. [作業の開始] ページで、**[ストレージ アカウントをマウントする]** を選択し、自分の **_XXXXXXXXX-MicrosoftSentinelLabs** をストレージ アカウント サブスクリプションのドロップダウン メニュー項目から選択して **[適用]** ボタンを選択します。****

    >**重要:***[ストレージ アカウントは必要ありません]* オプション ボタンのオプションは選択しないでください。 これは、インシデントの作成が失敗する原因になります。

1. *[ストレージ アカウントのマウント]* ページで、**[自動でストレージ アカウントを作成します]** を選択した後、**[次へ]** を選択します。

1. Cloud Shell がプロビジョニングされるまで待った後、Azure Cloud Shell ウィンドウを閉じます。

1. Azure portal の検索バーに「アクティビティ」と入力し、 **[アクティビティ ログ]** を選びます。**

1. [操作名] の項目に **[ストレージ アカウント キーの一覧表示]** と **[Update Storage Account Create] (ストレージ アカウントの作成の更新)** が表示されていることを確認します。** これらは、前に確認した KQL クエリがアラートを生成するために一致する操作です。 **ヒント:** **[最新の情報に更新]** を選んで一覧を更新することが必要な場合があります。

1. Defender XDR (`https://security.microsoft.com`) に戻ります。

1. Microsoft Defender ナビゲーション メニューで、下にスクロールし、*[調査と対応]* セクションを展開します。 次に、[インシデントとアラート] セクションを展開して **[インシデント]** を選択します。**

1. 新しく作成したインシデントが表示されます。

    >**注:** インシデントをトリガーするイベントは、処理に 5 分以上かかることがあります。 次の演習に進んでください。このビューには後で戻ります。

1. インシデントを選択し、右側のブレードの情報を確認します。

## 演習 3 に進む
