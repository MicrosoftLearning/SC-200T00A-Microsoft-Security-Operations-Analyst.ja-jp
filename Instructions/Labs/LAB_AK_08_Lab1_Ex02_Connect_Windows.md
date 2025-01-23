---
lab:
  title: 演習 2 - データ コネクタを使用して Microsoft Sentinel に Windows デバイスを接続する
  module: Learning Path 8 - Connect logs to Microsoft Sentinel
---

# ラーニング パス 8: ラボ 1: 演習 2: データ コネクタを使用して Microsoft Sentinel に Windows デバイスを接続する

## ラボのシナリオ

![ラボの概要。](../Media/SC-200-Lab_Diagrams_Mod6_L1_Ex2.png)

あなたは Microsoft Sentinel を実装した企業で働いているセキュリティ運用アナリストです。 組織内の多くのデータ ソースからのログ データを接続する方法について学習する必要があります。 データの次のソースは、オンプレミス環境や他のパブリック クラウドなど、Azure の内部および外部にある Windows 仮想マシンです。

>**重要:** ラーニング パス #8 のラボ演習は、*スタンドアロン*環境にあります。 ラボを完了せずに終了する場合は、構成を再実行する必要があります。

### このラボの推定所要時間: 30 分

### タスク 1:Azure で Windows 仮想マシンを作成する

このタスクでは、Azure で Windows 仮想マシンを作成します。

1. 管理者として **WIN1** 仮想マシンにログインします。パスワードは **Pa55w.rd** です。  

1. Microsoft Edge ブラウザーで、Azure portal (<https://portal.azure.com> ) に移動します。

1. **サインイン** ダイアログ ボックスで、ラボ ホスティング プロバイダーから提供された**テナントの電子メール** アカウントをコピーして貼り付け、**[次へ]** を選択します。

1. **[パスワードの入力]** ダイアログ ボックスで、ラボ ホスティング プロバイダーから提供された**テナント パスワード**をコピーして貼り付け、**[サインイン]** を選択します。

1. **[+ リソースの作成]** を選択します。 **ヒント:** 既に Azure Portal にいた場合は、上部のバーから *[Microsoft Azure]* を選択してホームに移動する必要があることがあります。

1. **[サービスとマーケットプレースの検索]** ボックスに「*Windows 10*」と入力し、ドロップダウン リストから **[Microsoft Window 10]** を選択します。

1. **Microsoft Window 10** のボックスをオンにします。

1. [プラン] ドロップダウン リストを開き、 **[Windows 10 Enterprise バージョン 22H2]** を選択します。**

1. **[事前設定された構成で開始する]** を選択して続行します。

1. **[開発/テスト]** を選択してから、**[VM の作成を続行する]** を選びます。

1. *[リソース グループ]* で **[新規作成]** を選択し、[名前] に「RG-AZWIN01」と入力して **[OK]** を選択します。

    >**注:**  これは、追跡目的の新しいリソース グループとなります。 

1. *[仮想マシン名]* に、「AZWIN01」と入力します。

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

<!--- ### Task 2: Install Azure Arc on an On-Premises Server

In this task, you install Azure Arc on an on-premises server to make onboarding easier.

>**Important:** The next steps are done in a different machine than the one you were previously working. Look for the Virtual Machine name references.

1. Log in to **WINServer** virtual machine as Administrator with the password: **Passw0rd!** if necessary.  

1. Open the Microsoft Edge browser and navigate to the Azure portal at <https://portal.azure.com>.

1. In the **Sign in** dialog box, copy, and paste in the **Tenant Email** account provided by your lab hosting provider and then select **Next**.

1. In the **Enter password** dialog box, copy, and paste in the **Tenant Password** provided by your lab hosting provider and then select **Sign in**.

1. In the Search bar of the Azure portal, type *Arc*, then select **Azure Arc**.

1. In the navigation pane under **Azure Arc resources** select **Machines**

1. Select **+ Add/Create**, then select **Add a machine**.

1. Select **Generate script** from the "Add a single server" section.

1. In the *Add a server with Azure Arc* page, select the Resource group you created earlier under *Project details*. **Hint:** *RG-Defender*

    >**Note:** If you haven't already created a resource group, open another tab and create the resource group and start over.

1. For *Region*, select **(US) East Us** from the drop-down list.

1. Review the *Server details* and *Connectivity method* options. Keep the default values and select **Next** to get to the Tags tab.

1. Review the default available tags. Select **Next** to get to the Download and run script tab.

1. Scroll down and select the **Download** button. **Hint:** if your browser blocks the download, take action in the browser to allow it. In Microsoft Edge Browser, select the ellipsis button (...) if needed and then select **Keep**.

1. Right-click the Windows Start button and select **Windows PowerShell (Admin)**.

1. Enter *Administrator* for "Username" and *Passw0rd!* for "Password" if you get a UAC prompt.

1. Enter: cd C:\Users\Administrator\Downloads

    >**Important:** If you do not have this directory, most likely means that you are in the wrong machine. Go back to the beginning of Task 4 and change to WINServer and start over.

1. Type *Set-ExecutionPolicy -ExecutionPolicy Unrestricted* and press enter.

1. Enter **A** for Yes to All and press enter.

1. Type *.\OnboardingScript.ps1* and press enter.  

    >**Important:** If you get the error *"The term .\OnboardingScript.ps1 is not recognized..."*, make sure you are doing the steps for Task 4 in the WINServer virtual machine. Other issue might be that the name of the file changed due to multiple downloads, search for *".\OnboardingScript (1).ps1"* or other file numbers in the running directory.

1. Enter **R** to Run once and press enter (this may take a couple minutes).

1. The setup process opens a new Microsoft Edge browser tab to authenticate the Azure Arc agent. Select your admin account, wait for the message "Authentication complete" and then go back to the Windows PowerShell window.

1. When the installation finishes, go back to the Azure portal page where you downloaded the script and select **Close**. Close the **Add servers with Azure Arc** to go back to the Azure Arc **Machines** page.

1. Select **Refresh** until WINServer server name appears and the Status is *Connected*.

    >**Note:** This could take a couple of minutes. --->

### タスク 2:Azure Windows 仮想マシンを接続する

このタスクでは、Azure Windows 仮想マシンを Microsoft Sentinel に接続します。

>**注:** Microsoft Sentinel は、**defenderWorkspace** という名前で Azure サブスクリプションに事前にデプロイされており、必要な*コンテンツ ハブ* ソリューションがインストールされています。

1. Azure portal の検索バーに「*Sentinel*」と入力してから、**[Microsoft Sentinel]** を選択します。

1. Microsoft Sentinel **defenderWorkspace** を選択します。

1. Microsoft Sentinel の左側ナビゲーション メニューで、*[コンテンツ管理]* セクションまで下にスクロールし、**[コンテンツ ハブ]** を選択します。

1. *[コンテンツ ハブ]* で、「**Windows セキュリティ イベント**」ソリューションを検索し、一覧から選択します。

1. *Windows セキュリティ イベント* のソリューション ページで、**[管理]** を選択します。

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

### タスク 4: 非 Azure Windows マシンを接続する

このタスクでは、Azure Arc に接続された非 Azure Windows 仮想マシンを、Microsoft Sentinel に追加します。  

   >**注:** "AMA を使用した Windows セキュリティ イベント" データ コネクタには非 Azure デバイス用の Azure Arc が必要です。**

1. Microsoft Sentinel ワークスペースの "AMA を使用した Windows セキュリティ イベント" データ コネクタの構成にいることを確認します。**

1. **[手順]** タブの *[構成]* セクションで、"鉛筆" アイコンを選択して **AZWINDCR** の "データ収集ルール" を編集します。** **

1. **[次へ: リソース]** を選択し、*[リソース]* タブの *[スコープ]* の下の *[サブスクリプション]* を展開します。

    >**ヒント:***[スコープ]* 列の前にある ">" を選択することで、*[スコープ]* 階層全体を展開できます。

1. **RG-Defender** (または作成したリソース グループ) を展開して、**WINServer** を選びます。

    >**重要:** WINServer が表示されない場合は、このサーバーに Azure Arc をインストールしたラーニング パス 3、演習 1、タスク 4 を参照してください。

1. **[適用]** を選択します。

1. **[次へ: 収集]** 、 **[次へ: 確認と作成]** の順に選択します。

1. *[検証に成功しました]* が表示されたら、 **[作成]** を選択します。

## 演習 3 に進む
