
# Microsoft Security Operations Analyst
講師用準備ガイド

## 目的

このドキュメントは、`Defend Against Threats with Extended Detection and Response` と `Configure Security Operations Using Microsoft Sentinel` のための Microsoft セキュリティ仮想トレーニング デーを教える準備をしているプレゼンターを対象としています。 この資料は SC-200:Microsoft Security Operations Analyst 認定コースのサブセットです。

## デモの前提条件

このコースのラボでは、Microsoft 365 E5ライセンスのテナントと、Azureサブスクリプションの両方が必要です。

* ご自身のために Microsoft Learning Azure Pass を要求できます。
* デモを実行する少なくとも 2 週間前に、これらのパスを要求してください。 パスを受け取った後、そのパスを有効にする必要があります。 
* Azure Pass は、一般に公開されている Microsoft Azure 試用版サブスクリプションと同じ方法で、効果的に機能します。 これは、パスで実行できる操作には制限があることを意味します。
* ラボの手順は、[SC-200 Microsoft Learning Github](https://github.com/MicrosoftLearning/SC-200T00A-Microsoft-Security-Operations-Analyst/tree/master/Instructions/VTD_Demos/) リポジトリにあります。
* デモに使用するコンピューターに新しい Microsoft Edge ブラウザーがインストールされていることを確認してください。

## Activate Azure Pass

## Defender for Endpoint のデプロイ

### Microsoft 365 資格情報の取得

ラボを起動すると、無料のトライアル テナントを利用して Microsoft Virtual Lab 環境にアクセスできるようになります。 このテナントには自動的に一意のユーザー名とパスワードが割り当てられます。 Microsoft Virtual Lab 環境で Azure と Microsoft 365 にサインインするには、このユーザー名とパスワードを取得する必要があります。

このコースは、学習パートナーが複数の認証済みラボ ホスティング プロバイダーのいずれかを使用して実施することもあり、お使いになっているテナントに関連のあるテナント ID を取得する実際の手順はラボ ホスティング プロバイダーに応じて異なります。 このため、コース内での当該情報の取得方法については、講師が必要な指示を行います。 後ほど使用できるよう以下の情報に留意してください。

    - **テナント サフィックス ID。** この ID は、ラボ全体で Microsoft 365 にサインインする際に使用する onmicrosoft.com アカウント用です。 形式は **{username}@M365xZZZZZZ.onmicrosoft.com** です。ZZZZZZ はラボ ホスティング プロバイダーの提供した一意のテナント サフィックス ID です。 後で使用できるよう、この ZZZZZZ を記録しておきます。 ラボの手順で Microsoft 365 ポータルにサインインするよう指示されたら、ここで取得した ZZZZZZ の値を入力してください。
    - **テナント パスワード。** これは、ラボ ホスティング プロバイダーの提供する管理者アカウント向けのパスワードです。
    

### Microsoft Defender for Endpoint の初期化

このタスクでは、Microsoft Defender for Endpoint の初期化を行います。

1. 管理者として WIN1 仮想マシンにログインします。パスワードは**Pa55w.rd**。  

1. Edge ブラウザーで、 https://security.microsoft.com) の Microsoft 365 Defender ポータルに移動します。

1. **[サインイン]** ダイアログ ボックスで、ラボ ホスティング プロバイダーから提供された管理者ユーザー名のテナント電子メール アカウントをコピーして貼り付け、**[次へ]** を選択します。

1. **パスワードの入力**ダイアログ ボックスで、ラボ ホスティング プロバイダーの提供した管理者のテナント パスワードをコピーして貼り付け、**サインイン**します。

**[Microsoft 365 Defender]** ポータルのナビゲーション メニューで、左側の **[ホーム]** を選択します。

    >**Note:** You may need to scroll all the way to the menu top.

1. **[ホーム]** ポータル ページに、 **[Microsoft 365 Defender へようこそ]** が表示されます。

1. **[Microsoft 365 Defender を有効にする]** というメッセージが示された **Microsoft 365 Defender** ラベルが付いたタイルが見つかるまで、タイルを下にスクロールします。

    >**ヒント:** タイルの右下に表示されるはずです。

1. **[新しい機能を有効にする]** というボタンを選択します。

1. ページの上部に ''*読み込んで初期化しています*'' というメッセージが一時的に表示されてから、コーヒー マグの画像と ''**お待ちください。データ用の新しいスペースを準備し、それらを接続しています**'' というメッセージが表示されます。 完了するまで約 5 分かかります。 ''*ページは開いたままにしてください。これは次のラボで必要になるので、必ず完了させるようにしてください。* ''

    >**メモ:** "お待ちください。 データ用の新しいスペースを準備し、それらを接続しています。" メッセージが表示されないか、または [設定] > [Microsoft 365 Defender] > [アカウント] ページが開きますが "Failed to load data storage location (データ ストレージの場所を読み込めませんでした)" というメッセージが表示される場合、 後でもう一度お試しください。[全般] メニューから [アラート サービスの設定] を選択するか、ナビゲーション メニューに移動し、[資産] セクションまで下にスクロールして [デバイス] を選択します。

1. 新しいスペースが正常に完了すると、アカウント、電子メール通知、アラート サービス設定、アクセス許可とロールおよび Streaming API の Microsoft 365 Defender [全般] 設定が表示されます。 **[プレビュー機能]** もオンになります。

**注**:ホストされているラボ環境では、データ ストレージの場所を選択する必要があります。 また、このトレーニング テナントが管理されている場所に適した地域にある必要があります。 [データ保有期間] の長さは引き続き選択できますが、必須ではありません。

1. **[設定]** で **[エンドポイント]** を選択します。

1. デバイス管理セクションで **[オンボーディング]** を選択します。

    >**メモ:** 左側のメニュー バーの **[アセット]** セクションからデバイスのオンボードを実行することもできます。 [アセット] を展開し、[デバイス] を選択します。 [デバイス インベントリ] ページで、[コンピューター] と [モバイル] が選択された状態で、 **[デバイスのオンボード]** まで下にスクロールします。 そうすると、 **[設定] > [エンドポイント]** ページが表示されます。

1. [1. オンボード デバイス] 領域で、デプロイ方法ドロップダウンにローカル スクリプト (最大 10 デバイス) が表示されていることを確認し、**[オンボーディング パッケージのダウンロード]** ボタンを選択します。

1. ダウンロードされた zip ファイルをローカル フォルダーに抽出します (［ドキュメント］ フォルダーなど)。

1. 抽出されたファイル (WindowsDefenderATPLocalOnboardingScript.cmd) を右クリックし、**[管理者として実行]** を選択します。  Windows SmartScreen が表示されたら、[実行する] を選択します。

**注** 既定で、ファイルは [c:\users\admin\downloads] ディレクトリにあります。
    
1. スクリプトの質問に対して、**[Y]** と回答します。 完了したら、コマンド画面に "マシンが正常にオンボードされました..." のような内容のメッセージが表示されます。 

1. ポータルの [オンボーディング] ページで、検出テスト スクリプトをコピーして、オープン コマンド ウィンドウで実行します。  新しい **[管理者: コマンド プロンプト]** ウィンドウを開く必要があるかもしれません。その場合は、Windows 検索バーで「*CMD*」と入力し、**[管理者として実行]** を選択します。

1. Microsoft 365 Defender ポータル メニューで、 **[デバイス インベントリ]** を選択します。 お使いになっているデバイスがリストに表示されます。

**注** デバイスがポータルに表示されるまでに最高 5 分かかることがあります。


### ロールの構成

このタスクでは、デバイス グループで使用するロールを設定します。

1. Microsoft 365 Defender ポータルで、左側のメニュー バーから **[設定]** を選択します。 

1. **[エンドポイント]** を選択し、アクセス許可領域で **[ロール]** を選択します。

1. **[ロールをオンにする]** ボタンを選択します。

1. **[項目の追加]** を選択します。

1. ロールの追加 ダイアログで以下を入力します。

    |全般設定|値|
    |---|---|
    |ロール名|**第一層サポート**|
    |アクセス許可|ライブ応答機能 - 詳細設定|

1. **[次へ]** を選択します。

1. [割り当てられたユーザー グループ] タブで **[sg-IT]** を選択し、**[選択したグループを追加する]** を選択します。

1. **[保存]** を選択します。

### デバイス グループの構成

このタスクでは、アクセス コントロールと自動化の設定が可能なデバイス グループを構成します。

1. 左側のメニュー バーで **[設定]** を選択します。 

1. **[エンドポイント]** を選択し、アクセス許可領域で **[デバイス グループ]** を選択します。

1. **[デバイス グループの追加]** を選択します。

1. 全般 タブに次の情報を入力します。

    |全般設定|値|
    |---|---|
    |デバイス グループ名|**Regular**|
    |自動化レベル|Full - remediate threats automatically (完全 - 脅威を自動的に修復する)|

1. **[次へ]** を選択します。

1. . [デバイス] タブの OS 条件で、**[Windows 10]** を選択し、**[次へ]** を選択します。

1. [デバイスのプレビュー] タブで、**[プレビューを表示]** を選択して、WIN1 仮想マシンを表示します。 **[次へ]** を選択します。 
**ヒント:** プレビューの一覧に仮想マシンが表示されない場合は、戻って、OS 条件として *[なし]* も選択してください。 VM のデータはまだ設定されていません。

1. [ユーザー アクセス] タブで、**[sg-IT]** を選択し、**[選択したグループを追加する]** を選択します

1. **[完了]** を選択します。

1. これでデバイス グループの構成が変わりました。 **[変更を適用]** を選択して、一致を確認し、グループ化を再計算します。

1. これで、先ほど作成した "Regular" と "グループに属していないデバイス (既定)" という 2 つのデバイス グループが同じ修復レベルで表示されます。

<!--- 
## Deploy sample alerts for Demo in Module 3

In this task, you will load sample security alerts and review the alert details.

1. In the Edge browser, open the Azure portal at https://portal.azure.com.

1. In the **Sign in** dialog box, copy and paste in the **Tenant Email** account provided by your lab hosting provider and then select **Next**.

1. In the **Enter password** dialog box, copy and paste in the **Tenant Password** provided by your lab hosting provider and then select **Sign in**.

1. In the Search bar of the Azure portal, type *Defender*, then select **Microsoft Defender for Cloud**.

1. In the **Getting Started** menu the default selection is **Upgrade**, select or **Skip** for now.

1. Select **Security alerts** in the portal menu.

1. Select **Sample Alerts** from the command bar.

1. In the Create sample alerts (Preview) pane make sure your subscription is selected.  Make sure all sample alerts are selected and select **Create sample alerts**.  

**Note** This may take a few minutes to complete. --->

## モジュール 4 でデモ用の Microsoft Sentinel ワークスペースをデプロイする

このタスクでは、Microsoft Sentinel ワークスペースを作成します。

 >**注:**  次のデモでは、Azure Pass またはその他の Azure サブスクリプションがアクティブである必要があります。

1. Edge ブラウザーで、Azure portal (https://portal.azure.com ) に移動します。

1. **[サインイン]** ダイアログ ボックスで、ラボ ホスティング プロバイダーから提供された**テナントの電子メール** アカウントをコピーして貼り付け、 **[次へ]** を選択します。

1. **[パスワードの入力]** ダイアログ ボックスで、ラボ ホスティング プロバイダーから提供された**テナントのパスワード**をコピーして貼り付け、 **[サインイン]** を選択します。

1. Azure portal の検索バーに「*Sentinel*」と入力してから、**[Microsoft Sentinel]** を選択します。

1. **[+ 作成]** を選択します。

1. **[+ 新しいワークスペースの作成]** を選択します。

**注** まず、新しい Log Analytics ワークスペースを作成します。

1. 適切なサブスクリプションを選択します。

1. リソースグループの**新規作成** リンクを選択し、選択した新しいリソースグループ名を入力します。

1. 名前 フィールドの インスタンスの詳細 で、LogAnalyticsワークスペースに選択する名前を入力します。

**注:**  この名前は一意である必要があり、Microsoft Sentinel ワークスペース名でもあります。

1. 適切な領域を選択します。  適切な領域が既定になる場合や、インストラクターがどの領域を選択するかについて具体的なアドバイスをする場合があります。  

1. **[確認および作成]** を選択します。

1. **［作成］** を選択します 新しい Log Analytics ワークスペースが [Azure Sentinel をワークスペースに追加] ページのリストに表示されるのを待ちます。  これには時間がかかることがあります。

1. 新しく作成したワークスペースが表示されたら、それを選択し、**[追加]** を選択します。

## Microsoft Sentinel 用の Content Hub ソリューションとデータ コネクタをデプロイする

### タスク 1:Microsoft Sentinel ワークスペースにアクセスする

このタスクでは、Microsoft Sentinel ワークスペースにアクセスします。

1. 管理者として WIN1 仮想マシンにログインします。パスワードは**Pa55w.rd**。  

1. ブラウザを開き、新しいMicrosoft Edgeブラウザーを検索、ダウンロード、およびインストールします。 新しいMicrosoft Edge ブラウザーを起動します。

1. Edge ブラウザーで、Azure portal (https://portal.azure.com ) に移動します。

1. **[サインイン]** ダイアログ ボックスで、ラボ ホスティング プロバイダーから提供された**テナントの電子メール** アカウントをコピーして貼り付け、 **[次へ]** を選択します。

1. **[パスワードの入力]** ダイアログ ボックスで、ラボ ホスティング プロバイダーから提供された**テナントのパスワード**をコピーして貼り付け、 **[サインイン]** を選択します。

1. Azure portal の検索バーに「*Sentinel*」と入力してから、**[Microsoft Sentinel]** を選択します。

1. 前のラボで作成した Microsoft Sentinel ワークスペースを選択します。

### タスク 2:Azure Activity データ コネクタを接続する

このタスクでは、*Azure Activity* データ コネクタを接続します。

1. Microsoft Sentinel の左側のメニューで、 *[コンテンツ管理]* セクションまで下にスクロールし、 **[コンテンツ ハブ]** を選択します。

1. *[コンテンツ ハブ]* で、「**Azure Activity**」ソリューションを検索し、一覧から選択します。

1. *Microsoft Defender for Cloud* ソリューション ページで、 **[インストール]** を選択します。

1. インストールが完了したら、 **[管理]** を選択します

    >**注:** *Azure Activity* ソリューションでは、*Azure Activity* データ コネクタ、12 個の分析ルール、14 個のハンティング クエリ、1 つのブックがインストールされます。

1. *Azure Activity* データ コネクタを選択し、 **[コネクタ ページを開く]** を選択します。

1. *[構成]* 領域の *[手順]* タブで、"2. 診断設定の新しい..." まで下にスクロールし、 **[[Azure Policy の割り当て] ウィザードの起動>]** を選択します。

1. **[基本]** タブで、 **[スコープ]** の下にある省略記号ボタン [...] を選択し、ドロップダウン リストから [Azure Pass - スポンサーシップ] サブスクリプションを選択して、 **[選択]** をクリックします。

1. **[パラメーター]** タブを選び、**[プライマリ Log Analytics ワークスペース]** ドロップダウン リストから自分のワークスペースを選びます。 このアクションにより、Log Analytics ワークスペースに情報を送信するサブスクリプション構成が適用されます。

1. **[修復]** タブを選択し、 **[修復タスクの作成]** チェック ボックスをオンにします。 このアクションにより、既存の Azure リソースにポリシーが適用されます。

1. **[確認と作成]** ボタンを選択して構成を確認します。

1. **[作成]** を選択して完了します。

### タスク 3:Azure で Windows 仮想マシンを作成する

このタスクでは、Azure で Windows 仮想マシンを作成します。

1. 管理者として **WIN1** 仮想マシンにログインします。パスワードは **Pa55w.rd** です。  

1. Microsoft Edge ブラウザーで、Azure portal (https://portal.azure.com ) に移動します。

1. **サインイン** ダイアログ ボックスで、ラボ ホスティング プロバイダーから提供された**テナントの電子メール** アカウントをコピーして貼り付け、**[次へ]** を選択します。

1. **[パスワードの入力]** ダイアログ ボックスで、ラボ ホスティング プロバイダーから提供された**テナント パスワード**をコピーして貼り付け、**[サインイン]** を選択します。

1. **[+ リソースの作成]** を選択します。 **ヒント:** 既に Azure Portal にいた場合は、上部のバーから *[Microsoft Azure]* を選択してホームに移動する必要があることがあります。

1. **[サービスとマーケットプレースの検索]** ボックスに「*Windows 10*」と入力し、ドロップダウン リストから **[Microsoft Window 10]** を選択します。

1. **Microsoft Window 10** のボックスをオンにします。

1. [プラン] ドロップダウン リストを開き、 **[Windows 10 Enterprise バージョン 22H2]** を選択します。**

1. **[事前設定された構成で開始する]** を選択して続行します。

1. **[開発/テスト]** を選択してから、**[VM の作成を続行する]** を選びます。

1. [リソース グループ] で **[新規作成]** を選択し、[名前] に「`RG-AZWIN01`」と入力して **[OK]** を選択します。**

    >**注:**  これは、追跡目的の新しいリソース グループとなります。 

1. [仮想マシン名] に「`AZWIN01`」と入力します。**

1. *[リージョン]* の既定値は **[(米国) 米国東部]** のままにします。

1. 下にスクロールして、仮想マシンの [イメージ] を確認します。** 空の場合は、 **[Windows 10 Enterpriseバージョン 22H2]** を選択します。

1. 仮想マシンの [サイズ] を確認します。** 空の場合は、 **[すべてのサイズを表示]** を選択し、 *[Azure ユーザーが最もよく使用]* で最初の VM サイズを選択し、 **[選択]** を選択します。

    >**注:** 次のメッセージが表示される場合: *This image is not supported for Azure Automanage. To disable this feature,navigate to the Management tab. Otherwise, select a supported image.* (このイメージは Azure Automanage ではサポートされていません。この機能を無効にするには、[管理] タブに移動してください。それ以外の場合は、サポートされているイメージを選択してください。) [管理] タブに移動し、"Automanage" を無効にします。 その後、作成プロセスは成功するようになります。

1. 下にスクロールし、選んだ [ユーザー名] を入力します。** **ヒント:** admin や root のような予約語は避けてください。

1. 任意の ''*パスワード*'' を入力します。 **ヒント:** テナント パスワードを再利用する方が簡単な場合があります。 これはリソース タブにあります。

1. ページの下部まで下にスクロールし、*[ライセンス]* の下にあるチェックボックスをオンにして、対象ライセンスがあることを確認します。

1. **[確認と作成]** を選択し、検証に合格するまで待ちます。

    >**注:** "ネットワーク" 検証エラーがある場合は、そのタブを選び、その内容を確認してから、 **[確認と作成]** をもう一度選びます。**

1. **［作成］** を選択します リソースが作成されるのを待ちますこれには数分かかることがあります。

### タスク 4:Azure Windows 仮想マシンを接続する

このタスクでは、Azure Windows 仮想マシンを Microsoft Sentinel に接続します。

1. Azure portal の検索バーに「*Sentinel*」と入力してから、**[Microsoft Sentinel]** を選択します。

1. 先ほど作成した Microsoft Sentinel ワークスペースを選択します。

1. 1. Microsoft Sentinel の左側のメニューで、 *[コンテンツ管理]* セクションまで下にスクロールし、 **[コンテンツ ハブ]** を選択します。

1. *[コンテンツ ハブ]* で、「**Windows セキュリティ イベント**」ソリューションを検索し、一覧から選択します。

1. "Windows セキュリティ イベント" のソリューション ページで、 **[インストール]** を選択します。**

1. インストールが完了したら、 **[管理]** を選択します

    >**注:** "Windows セキュリティ イベント" ソリューションでは、"AMA を使用した Windows セキュリティ イベント" と "レガシ エージェントを使用したセキュリティ イベント" データ コネクタの両方がインストールされます。** ** ** さらに、2 つのブック、20 個の分析ルール、43 個のハンティング クエリがインストールされます。

1. "AMA を使用した Windows セキュリティ イベント" データ コネクタを選択し、コネクタ情報ブレードの **[コネクタ ページを開く]** を選択します。**

1. *[構成]* セクションの *[手順]* タブで、 **[データ収集ルールの作成]** を選択します。

1. ルール名に「**AZWINDCR**」と入力して、 **[次へ: リソース]** を選択します。

1. **[+ リソースの追加]** を選択し、作成した仮想マシンを選択します。

1. **RG-AZWIN01** を展開し、**AZWIN01** を選択します。

1. **[適用]** を選んでから、 **[次へ: 収集]** を選びます。

1. 別のセキュリティ イベント コレクション オプションを確認します。 [すべてのセキュリティ イベント] のままにして、 **[次へ: 確認と作成]** を選びます。**

1. **[作成]** を選んで、データ収集ルールを保存します。

1. 少し待ってから **[更新]** を選択すると、新しいデータ収集規則が一覧表示されます。

### タスク 5:Azure Arc をインストールしてオンプレミス サーバーに接続する

このタスクでは、オンボードを簡単にするために、オンプレミスのサーバーに Azure Arc をインストールします。

>**重要:** 次の手順は、以前に作業していたものとは異なるマシンで行います。 仮想マシン名の参照を探します。

1. 管理者として **WINServer** 仮想マシンにログインします。パスワードは **Passw0rd!** です。 です (必要な場合)。  

1. Microsoft Edge ブラウザーを開き、Azure portal (https://portal.azure.com ) に移動します。

1. **サインイン** ダイアログ ボックスで、ラボ ホスティング プロバイダーから提供された**テナントの電子メール** アカウントをコピーして貼り付け、**[次へ]** を選択します。

1. **[パスワードの入力]** ダイアログ ボックスで、ラボ ホスティング プロバイダーから提供された**テナントのパスワード**をコピーして貼り付け、 **[サインイン]** を選択します。

1. Azure portal の検索バーに「*Arc*」と入力し、**[Azure Arc]** を選択します。

1. ナビゲーション ウィンドウの **[インフラストラクチャ]** の下にある **[マシン]** を選択します

1. **[+ Add/Create] (+ 追加/作成)** を選択し、 **[Add a machine] (マシンの追加)** を選択します。

1. [単一サーバーの追加] セクションから **[スクリプトの生成]** を選択します。

1. *[前提条件]* タブに目を通してから、 **[次へ]** を選択して続行します。

1. *[Azure Arc を使用してサーバーを追加する]* ページで、 *[プロジェクトの詳細]* で先ほど作成したリソース グループを選択します。 **ヒント:** *RG-Defender*

    >**注:**  リソース グループをまだ作成していない場合は、別のタブを開き、リソース グループを作成して最初からやり直します。

1. *[サーバーの詳細]* と *[接続方法]* のオプションを確認します。 既定値のままにして **[次へ]** を選択し、[タグ] タブに移動します。

1. 使用可能な既定のタグを確認します。 **[次へ]** を選択して、[スクリプトのダウンロードと実行] タブに移動します。

1. 下にスクロールし、 **[ダウンロード]** ボタンを選択します。 **ヒント:** ブラウザーでダウンロードがブロックされた場合は、ブラウザーでダウンロードを許可するように対処してください。 Edge ブラウザーで、必要に応じて省略記号ボタン ([...]) を選択し、**[保存]** を選択します。

1. Windows の [スタート] ボタンを右クリックし、**[Windows PowerShell (管理者)]** を選択します。

1. UAC プロンプトが表示された場合は、「*Administrator*」を "ユーザー名" として、「*Passw0rd!*」を "パスワード" として入力します。

1. 「cd C:\Users\Administrator\Downloads」と入力します。

    >**重要:** このディレクトリがない場合は、ほとんどの場合、間違ったマシンを使用していることを意味します。 タスク 4 の先頭に戻り、WINServer に変更してやり直します。

1. *Set-ExecutionPolicy -ExecutionPolicy Unrestricted* を入力しEnterキーを押します。

1. [すべてにはい] の場合は「**A**」を入力し、Enter キーを押します。

1. 「*.\OnboardingScript.ps1*」と入力し、Enter キーを押します。  

    >**重要:** *用語 .\OnboardingScript.ps1 が認識されません...* というエラーが表示された場合は、タスク 4 を WINServer 仮想マシンで行っていることを確認してください。 他の問題として、複数回ダウンロードしたためにファイルの名前が変更された可能性があります。実行中のディレクトリで *".\OnboardingScript (1).ps1"* またはその他のファイル番号を検索してください。

1. **R** を入力して 1 回実行し、Enter キーを押します (これには数分かかる場合があります)。

1. セットアップ プロセスにより、Azure Arc エージェントを認証するための新しい Edge ブラウザー タブが開きます。 ご自分の管理者アカウントを選択し、"認証が完了しました" というメッセージが表示されるまで待ってから、Windows PowerShell ウィンドウに戻ります。

1. インストールが完了したら、スクリプトをダウンロードした Azure portal ページに戻り、 **[閉じる]** を選択します。 **[Azure Arc を使用してサーバーを追加]** を閉じて、Azure Arc の **[マシン]** ページに戻ります。

1. WINServer サーバー名が表示され、[状態] が *[接続済み]* になるまで **[更新]** を選択します。

    >**注:** これには数分かかることがあります。


### タスク 6:オンプレミスのサーバーを保護する

このタスクでは、Azure Arc に接続された非 Azure Windows 仮想マシンを、Microsoft Sentinel に追加します。  

   >**注:** "AMA を使用した Windows セキュリティ イベント" データ コネクタには非 Azure デバイス用の Azure Arc が必要です。**

1. Microsoft Sentinel ワークスペースの "AMA を使用した Windows セキュリティ イベント" データ コネクタの構成にいることを確認します。**

1. **[手順]** タブの *[構成]* セクションで、"鉛筆" アイコンを選択して **AZWINDCR** の "データ収集ルール" を編集します。** **

1. **[次へ: リソース]** 、 **[+ リソースの追加]** の順に選択します。

1. 作成したリソース グループを展開して、**WINServer** を選びます。

    >**重要:** WINServer が表示されない場合は、このサーバーに Azure Arc をインストールしたラーニング パス 3、演習 1、タスク 4 を参照してください。

1. **[適用]** を選択します。

1. **[次へ: 収集]** 、 **[次へ: 確認と作成]** の順に選択します。

1. *[検証に成功しました]* が表示されたら、 **[作成]** を選択します。


<!--- ### Task 4: Connect the Microsoft Defender for Cloud connector.

In this task, you will connect the Microsoft Defender for Cloud connector.

1. From the Data Connectors tab, select the **Microsoft Defender for Cloud** connector from the list.

1. Select **Open connector page** on the connector information blade.

1. Review the Connecting Options. Don't connect. This is for informational purposes only.

### Task 5: Connect the Microsoft Defender for Cloud Apps connector.

In this task, you will connect theMicrosoft Defender for Cloud Apps connector.

1. From the Data Connectors Tab, select the **Microsoft Defender for Cloud Apps** connector from the list.

1. Select **Open connector page** on the connector information blade.

1. In the **Instructions** tab in the **Configuration** section, select **Alerts** and then select **Apply Changes**.

### Task 6: Connect the Microsoft Defender for Office 365 connector.

In this task, you will connect the Microsoft Defender for Office 365 connector.

1. From the Data Connectors tab, select the **Microsoft Defender for Office 365** connector from the list.

1. Select **Open connector page** on the connector information blade.

1. Select **Connect**.

### Task 7: Connect the Microsoft Defender for Identity connector.

In this task, you will connect the Microsoft Defender for Identity connector.

1. From the Data Connectors Tab, select the **Microsoft Defender for Identity** connector from the list.

1. Select **Open connector page** on the connector information blade.

1. Review the Connecting Options. Don't connect. This is for informational purposes only.

### Task 8: Connect the Microsoft Defender for Endpoint connector.

In this task, you will connect the Microsoft Defender for Endpoint connector.

1. From the Data Connectors Tab, select the **Microsoft Defender for Endpoint** connector from the list.

1. Select Open connector page on the connector information blade.

1. Select **Connect**.

### Task 9: Connect the Microsoft 365 Defender connector.

In this task, you will connect the Microsoft 365 Defender connector.

1. From the Data Connectors Tab, select the **Microsoft 365 Defender** connector from the list.

1. Select **Open connector page** on the connector information blade.

1. Select all the checkboxes for Microsoft Defender for Endpoint.

1. Select **Apply Changes**. 

### Task 3: Connect a non-Azure Windows Machine.

In this task, you will connect a non-Azure Windows virtual machine to Microsoft Sentinel.

1. Login to WIN2 virtual machine as Admin with the password: **Pa55w.rd**.  

1. Open the browser, search for, download, and install the new Microsoft Edge browser. Start the new Edge browser.

1. Open a browser and log into the Azure Portal at https://portal.azure.com with your credentials.

1. In the Search bar of the Azure Portal, type *Sentinel*, then select **Microsoft Sentinel**.

1. Select your Microsoft Sentinel Workspace.

1. From the Data Connectors tab, select the **Security Events via Legacy Agent** connector from the list.

1. Select **Open connector page** on the connector information blade.

1. In the Select which events to stream area, select **All Events**, then select **Apply Changes**.

1. Select the **Install agent on a non-Azure Windows  Machine**.

**Note:** The instructions for Install agent on a Windows Virtual Machine and Install agent on a non-Azure Windows Machine may be reversed. The links take you to the proper location even with the reversed text.

1. Select **Download & install agent for non-Azure Windows machines**. 

1. Select the link for **Download Windows Agent (64 bit)**.

1. Run the .exe file that is downloaded and confirm and User Account Control prompt that may appear.

1. Select **Next** on the Welcome dialog.

1. Select **I Agree** on the Microsoft Software License Terms page.  On the Destination prompt select **Next**.

1. On the Agent Setup Options prompt, select **Connect the agent to Azure Log Analytics (OMS)** option, then select **Next**.

1. In the browser, copy the **Workspace ID** from the Agents Management page and paste into the Workspace ID in the dialog. 

1. In the browser, copy the **Primary key** from the Agents Management page and paste into the Primary key in the dialog. 

1. Select **Next**.

1. Select **Next** on the Microsoft Update page.

2. Then select **Install**.

### Task 4: Install and collect Sysmon logs.

In this task, you will install and collect Sysmon logs.

You should still be connected to the WIN2 virtual machine.  The following instructions will install Sysmon with the default configuration.  You should research community based configurations for Sysmon to be used on production machines.

1. In the browser, go to https://docs.microsoft.com/sysinternals/downloads/sysmon

1. Download Sysmon from the page by select **Download Sysmon**.

1. Open the downloaded file and extract the files to a new directory c:\sysmon

1. In the Windows Taskbar for WIN2 search box, enter *command*.  The search results will show command prompt app.  Right-click on the command prompt app and select **Run as Administrator**.  Confirm any User Account Control prompts that appear.

1. Enter *cd \sysmon*

1. type *notepad sysmon.xml* to create a new file.

1. Open a tab in the browser and navigate to: https://github.com/SwiftOnSecurity/sysmon-config/blob/master/sysmonconfig-export.xml

1. Copy the contents of that file from Github to the sysmon.xml notepad file you just created and save the file.

1. In the command prompt type the following and press enter:
    sysmon.exe -accepteula -i sysmon.xml

1. In the browser, navigate to the Azure portal at https://portal.azure.com 

1. In the Search bar of the Azure portal, type *Sentinel*, then select **Microsoft Sentinel**.

1. In Microsoft Sentinel, select **Settings** from the Configuration area and then select **Workspace settings** tab.

1. Make sure your Microsoft Sentinel Workspace is selected.

1. Select **Agents configuration** in Settings.

1. Select the **Windows Event logs** tab.

1. Select **Add windows event log** button.

1. Enter **Microsoft-Windows-Sysmon/Operational** in the Log name field.

1. Select **Apply**. --->

## 攻撃を実施する

### タスク 1:Defender for Endpoint で構成された Windows を攻撃する

このタスクでは、Microsoft Defender for Endpoint が構成されているホストに対して攻撃を実行します。

1. 管理者として、次のパスワードを使用して `WIN1` 仮想マシンにログインします: **Pa55w.rd**。  

1. タスク バーの検索で、*Command* と入力します。  検索結果にコマンド プロンプトが表示されます。  コマンド プロンプトを右クリックして、 **[管理者として実行]** を選択します。 表示されるユーザー アカウント制御のプロンプトを確認します。

1. コマンドプロンプトで、各行の後に Enter キーを押して、各行にコマンドを入力します。
```
cd \
mkdir temp
cd temp
```

1. 次のコマンドをコピーして実行します。

```
REG ADD "HKCU\SOFTWARE\Microsoft\Windows\CurrentVersion\Run" /V "SOC Test" /t REG_SZ /F /D "C:\temp\startup.bat"
```

### タスク 2:C2 (コマンドと制御) 攻撃を作成する

1. 管理者として、次のパスワードを使用して `WIN1` 仮想マシンにログインします: **Pa55w.rd**。  

1. タスク バーの検索で、*Command* と入力します。  検索結果にコマンド プロンプトが表示されます。  コマンド プロンプトを右クリックして、 **[管理者として実行]** を選択します。 表示されるユーザー アカウント制御のプロンプトを確認します。
1. 
1. 
1. 攻撃 2 - 次のコマンドをコピーして実行します。

```
notepad c2.ps1
```
**[はい]** を選択して新しいファイルを作成し、以下の PowerShell スクリプトを c2.ps1 にコピーして **[保存]** を選択します。

**注** 仮想マシンへの貼り付けには長さの制限がある場合があります。  これを 3 つのセクションに貼り付けて、すべてのスクリプトが仮想マシンに貼り付けられるようにします。  スクリプトがメモ帳c2.ps1ファイル内のこれらの手順のように見えることを確認してください。

```


param(
    [string]$Domain = "microsoft.com",
    [string]$Subdomain = "subdomain",
    [string]$Sub2domain = "sub2domain",
    [string]$Sub3domain = "sub3domain",
    [string]$QueryType = "TXT",
        [int]$C2Interval = 8,
        [int]$C2Jitter = 20,
        [int]$RunTime = 240
)


$RunStart = Get-Date
$RunEnd = $RunStart.addminutes($RunTime)

$x2 = 1
$x3 = 1 
Do {
    $TimeNow = Get-Date
    Resolve-DnsName -type $QueryType $Subdomain".$(Get-Random -Minimum 1 -Maximum 999999)."$Domain -QuickTimeout

    if ($x2 -eq 3 )
    {
        Resolve-DnsName -type $QueryType $Sub2domain".$(Get-Random -Minimum 1 -Maximum 999999)."$Domain -QuickTimeout
        
        $x2 = 1

    }
    else
    {
        $x2 = $x2 + 1
    }
    
    if ($x3 -eq 7 )
    {

        Resolve-DnsName -type $QueryType $Sub3domain".$(Get-Random -Minimum 1 -Maximum 999999)."$Domain -QuickTimeout

        $x3 = 1
        
    }
    else
    {
        $x3 = $x3 + 1
    }


    $Jitter = ((Get-Random -Minimum -$C2Jitter -Maximum $C2Jitter) / 100 + 1) +$C2Interval
    Start-Sleep -Seconds $Jitter
}
Until ($TimeNow -ge $RunEnd)

```

コマンドプロンプトで、次のように入力し、各行の後に Enter キーを押して各行にコマンドを入力します。
```
powershell
.\c2.ps1
```
**注:**  解決エラーが表示されます。 これは通常の動作で、エラーではありません。
このコマンド/パワーシェルスクリプトをバックグラウンドで実行します。 ウィンドウを閉じないでください。  コマンドは、数時間ログエントリを生成する必要があります。  このスクリプトの実行中に次のタスクや次の演習に進むことができます。  このタスクで作成したデータは、後で脅威の捜索ラボで使用します。  このプロセスでは、大量のデータや処理を作成することはありません。

### タスク 2:Azure Monitor エージェント (AMA) で構成された攻撃ウィンドウ

このタスクでは、セキュリティ イベント コネクタが構成され、Sysmon が構成されているホストに対して攻撃を実行します。

1. 前に作成した `AZWIN01` 仮想マシンを選択します。  

1. 左側のメニューで **[操作]** まで下にスクロールし、**[コマンドの実行]** を選択します

1. **[コマンドの実行]** ペインで、**[RunPowerShellScript]** を選択します

1. 以下のコマンドをコピーして、`PowerShell Script` フォームへの管理アカウントの作成をシミュレートし、**[実行]** を選択します

    ```CommandPrompt
    net user theusernametoadd /add
    net user theusernametoadd ThePassword1!
    net localgroup administrators theusernametoadd /add
    ```

>**注**: 1 行にコマンドが 1 つだけあることを確認してください。ユーザー名を変更するとコマンドを再実行できます。

1. `Output` ウィンドウに `The command completed successfully` が 3 回表示されます
