---
lab:
  title: 演習 2 - データ コネクタを使用して Microsoft Sentinel に Windows デバイスを接続する
  module: Module 6 - Connect logs to Microsoft Sentinel
---

# <a name="module-6---lab-1---exercise-2---connect-windows-devices-to-microsoft-sentinel-using-data-connectors"></a>モジュール 6 - ラボ 1 - 演習 2 - データ コネクタを使用して Microsoft Sentinel に Windows デバイスを接続する

## <a name="lab-scenario"></a>ラボのシナリオ

![ラボの概要。](../Media/SC-200-Lab_Diagrams_Mod6_L1_Ex2.png)

You are a Security Operations Analyst working at a company that implemented Microsoft Sentinel. You must learn how to connect log data from the many data sources in your organization. The next source of data are Windows virtual machines inside and outside of Azure, like On-Premises environments or other Public Clouds.


### <a name="task-1-create-a-windows-virtual-machine-in-azure"></a>タスク 1:Azure で Windows 仮想マシンを作成する

このタスクでは、Azure で Windows 仮想マシンを作成します。

1. 管理者として **WIN1** 仮想マシンにログインします。パスワードは **Pa55w.rd** です。  

1. Edge ブラウザーで、Azure portal (https://portal.azure.com ) に移動します。

1. **サインイン** ダイアログ ボックスで、ラボ ホスティング プロバイダーから提供された**テナントの電子メール** アカウントをコピーして貼り付け、**[次へ]** を選択します。

1. **[パスワードの入力]** ダイアログ ボックスで、ラボ ホスティング プロバイダーから提供された**テナント パスワード**をコピーして貼り付け、**[サインイン]** を選択します。

1. Select <bpt id="p1">**</bpt>+ Create a Resource<ept id="p1">**</ept>. <bpt id="p1">**</bpt>Hint:<ept id="p1">**</ept> If you were already in the Azure Portal, you might need to select <bpt id="p2">*</bpt>Microsoft Azure<ept id="p2">*</ept> from the top bar to go Home.

1. **[サービスとマーケットプレースの検索]** ボックスに「*Windows 10*」と入力し、ドロップダウン リストから **[Microsoft Window 10]** を選択します。

1. Open the <bpt id="p1">*</bpt>Plan<ept id="p1">*</ept> drop-down list and select <bpt id="p2">**</bpt>Windows 10 Enterprise, version 21H2<ept id="p2">**</ept>. Select <bpt id="p1">**</bpt>Start with a pre-set configuration<ept id="p1">**</ept> to continue.

1. **[開発/テスト]** を選択してから、**[VM の作成を続行する]** を選びます。

1. *[リソース グループ]* で **[新規作成]** を選択し、[名前] に「RG-AZWIN01」と入力して **[OK]** を選択します。

    >**注:**  これは、追跡目的の新しいリソース グループとなります。 

1. *[仮想マシン名]* に、「AZWIN01」と入力します。

1. *[リージョン]* の既定値は **[(米国) 米国東部]** のままにします。

1. Scroll down and review the <bpt id="p1">*</bpt>Size<ept id="p1">*</ept> for the virtual machine. If it appears empty, select <bpt id="p1">**</bpt>See all sizes<ept id="p1">**</ept>, choose one of the VM sizes under <bpt id="p2">*</bpt>Most used by Azure users<ept id="p2">*</ept> and click <bpt id="p3">**</bpt>Select<ept id="p3">**</ept>.

1. Enter a <bpt id="p1">*</bpt>Username<ept id="p1">*</ept> of your choosing. <bpt id="p1">**</bpt>Hint:<ept id="p1">**</ept> Avoid reserved words like admin or root.

1. あなたは、Microsoft Sentinel を実装した会社で働いているセキュリティ運用アナリストです。

1. ページの下部まで下にスクロールし、*[ライセンス]* の下にあるチェックボックスをオンにして、対象ライセンスがあることを確認します。

1. **[確認と作成]** を選択し、検証に合格するまで待ちます。

1. 組織内の多くのデータ ソースからのログ データを接続する方法について学習する必要があります。


### <a name="task-2-connect-an-azure-windows-virtual-machine"></a>タスク 2:Azure Windows 仮想マシンを接続する

このタスクでは、Azure Windows 仮想マシンを Microsoft Sentinel に接続します。

1. Azure portal の検索バーに「*Sentinel*」と入力してから、**[Microsoft Sentinel]** を選択します。

1. 先ほど作成した Microsoft Sentinel ワークスペースを選択します。

1. [データ コネクタ] タブで、 **[AMA 使用した Windows セキュリティ イベント]** コネクタを検索し、リストからそれを選択します。

1. [コネクタ情報] ブレードで **[コネクタ ページを開く]** を選択します。

1. *[構成]* セクションで、 **[データ収集の作成]** 規則を選択します。
1. ルール名に「**AZWIN01DCR**」と入力して、 **[次へ:リソース]** を選択します。
1. **[リソースの追加]** を選択します。
1. **rg-azwin01** を展開し、**AZWIN01** を選択します。
1. **[適用]** を選択します。
1. **[次へ: 収集]** 、 **[次へ:確認と作成]** の順に選択します。
1. **[作成] をクリックします**
1. 数分待ってから **[更新]** を選択すると、新しいデータ収集規則が一覧表示されます。


### <a name="task-3-connect-a-non-azure-windows-machine"></a>タスク 3:非 Azure Windows マシンを接続する

このタスクでは、Azure Arc をインストールし、非 Azure Windows 仮想マシンを Microsoft Sentinel に接続します。  

>データの次のソースは、オンプレミス環境や他のパブリック クラウドなど、Azure の内部および外部にある Windows 仮想マシンです。

>**重要:** *AMA を使用した Windows セキュリティ イベント* データ コネクタには非 Azure デバイス用の Azure Arc が必要です。 

1. 管理者として、**WIN2** 仮想マシンにログインします:。パスワードは **Pa55w.rd** です。  

1. Microsoft Edge ブラウザーを開きます。

1. ブラウザーを開き、前のラボで使っていた資格情報を使用して、Azure Portal (https://portal.azure.com ) にログインします。


1. **サインイン** ダイアログ ボックスで、ラボ ホスティング プロバイダーから提供された**テナントの電子メール** アカウントをコピーして貼り付け、**[次へ]** を選択します。

1. **[パスワードの入力]** ダイアログ ボックスで、ラボ ホスティング プロバイダーから提供された**テナントのパスワード**をコピーして貼り付け、 **[サインイン]** を選択します。

1. Azure portal の検索バーに「*Arc*」と入力し、**[Azure Arc]** を選択します。

1. ナビゲーション ウィンドウの **[インフラストラクチャ]** の下にある **[サーバー]** を選択します。

1. **[+ 追加]** を選択します。

1. 単一サーバーの追加セクションで **[スクリプトの生成]** を選択します。

1. **[次へ]** を選択して [リソースの詳細] タブに移動します。

1. Select the Resource group you created earlier. <bpt id="p1">**</bpt>Hint:<ept id="p1">**</ept> <bpt id="p2">*</bpt>RG-Defender<ept id="p2">*</ept>

    >**注:**  リソース グループをまだ作成していない場合は、別のタブを開き、リソース グループを作成して最初からやり直します。

1. Review the <bpt id="p1">*</bpt>Server details<ept id="p1">*</ept> and <bpt id="p2">*</bpt>Connectivity method<ept id="p2">*</ept> options. Keep the default values and select <bpt id="p1">**</bpt>Next<ept id="p1">**</ept> to get to the Tags tab.

1. **[次へ]** を選択して、[スクリプトのダウンロードと実行] タブに移動します。

1. **[登録]** オプションが利用できる場合は、 **[登録]** を選択します (ステップ *[1. サブスクリプションを登録]* の下)。

    >**注:**  処理のために少なくとも 3 分待ちます。

1. Scroll down and select the <bpt id="p1">**</bpt>Download<ept id="p1">**</ept> button. <bpt id="p1">**</bpt>Hint:<ept id="p1">**</ept> if your browser blocks the download, take action in the browser to allow it. In Edge Browser, select the ellipsis button (...) if needed and then select <bpt id="p1">**</bpt>Keep<ept id="p1">**</ept>. 

1. Windows の [スタート] ボタンを右クリックし、**[Windows PowerShell (管理者)]** を選択します。

1. In case you get a UAC prompt, enter <bpt id="p1">*</bpt>Administrator<ept id="p1">*</ept> for "Username" and <bpt id="p2">*</bpt>Passw0rd!<ept id="p2">*</ept> for "Password", else skip to next step.

1. 「cd C:\Users\Admin\Downloads」と入力します。

1. *Set-ExecutionPolicy -ExecutionPolicy Unrestricted* を入力しEnterキーを押します。

1. [すべてにはい] の場合は「**A**」を入力し、Enter キーを押します。

1. 「*.\OnboardingScript.ps1*」と入力し、Enter キーを押します。  

    ><bpt id="p1">**</bpt>Important:<ept id="p1">**</ept> If you get the error <bpt id="p2">*</bpt>"The term .\OnboardingScript.ps1 is not recognized..."<ept id="p2">*</ept>, make sure you are doing the steps for Task 4 in the WINServer virtual machine. Other issue might be that the name of the file changed due to multiple downloads, search for <bpt id="p1">*</bpt>".\OnboardingScript (1).ps1"<ept id="p1">*</ept> or other file numbers in the running directory.

1. **R** を入力して 1 回実行し、Enter キーを押します (これには数分かかる場合があります)。

1. Edge ブラウザーに戻って新しいタブを開き、アドレス バーに「https://microsoft.com/devicelogin」と入力します。

1. [Windows PowerShell] ウィンドウに戻り、スクリプトの最後の行で "... コードの入力" の後に表示されている、エージェントを認証するためのコードをコピーします。**

1. Go back to the Edge browser and paste it in the <bpt id="p1">**</bpt>Code<ept id="p1">**</ept> box and select <bpt id="p2">**</bpt>Next<ept id="p2">**</ept>. Select your tenant admin account and select <bpt id="p1">**</bpt>Continue<ept id="p1">**</ept> in the <bpt id="p2">*</bpt>Are you trying to sign in to Azure Connected Machine Agent?<ept id="p2">*</ept> window. 

1. Go back to the Windows PowerShell window and wait for the message <bpt id="p1">*</bpt>"Successfully Onboarded Resource to Azure"<ept id="p1">*</ept>. <bpt id="p1">**</bpt>Note:<ept id="p1">**</ept> If you see a message line with a new authentication code, you need to repeat the last 3 steps again.

1. **[+ リソースの作成]** を選択します。

1. **WIN2** の名前が表示されるまで、 **[更新]** を選択します。

    >**注:**  この処理には数分かかります。



1. Azure portal の検索バーに「*Sentinel*」と入力し、**[Microsoft Sentinel]** を選択します。

1. 先ほど作成した Microsoft Sentinel ワークスペースを選択します。

1. [データ コネクタ] タブで、 **[AMA 使用した Windows セキュリティ イベント]** コネクタを検索し、リストからそれを選択します。

1. [コネクタ情報] ブレードで **[コネクタ ページを開く]** を選択します。

1. *[構成]* セクションで、 **[データ収集の作成]** 規則を選択します。
1. ルール名に「**WIN2**」と入力し、 **[次へ:リソース]** を選択します。
1. **[リソースの追加]** を選択します。
1. **rg-defender** (または作成したリソース グループ) を展開し、**WIN2** を選択します。
1. **[適用]** を選択します。
1. **[次へ: 収集]** 、 **[次へ:確認と作成]** の順に選択します。
1. **[作成] をクリックします**
1. 数分待ってから **[更新]** を選択すると、新しいデータ収集規則が一覧表示されます。



### <a name="task-4-onboard-microsoft-defender-for-endpoint-device"></a>タスク 4:Microsoft Defender for Endpoint デバイスをオンボードする

このタスクでは、デバイスを Microsoft Defender for Endpoint にオンボードします。

>**ヒント:** 既に Azure Portal にいた場合は、上部のバーから *[Microsoft Azure]* を選択してホームに移動する必要があることがあります。

><bpt id="p1">**</bpt>Important:<ept id="p1">**</ept> The next steps are done in a different machine than the one you were previously working. Look for the Virtual Machine name references.

1. 管理者として WIN1 仮想マシンにログインします。パスワードは**Pa55w.rd**。  

1. Edge ブラウザーで、Microsoft 365 Defender ポータル (https://security.microsoft.com) ) に移動し、現在ポータルにいない場合は、**テナントの電子メール**資格情報を使用してログインします。

1. 左側のメニュー バーから **[設定]** を選択し、設定 ページから **[エンドポイント]** を選択します。

1. デバイス管理セクションで **[オンボーディング]** を選択します。

1. **[オンボーディング パッケージのダウンロード]** を選択します。

1. ダウンロードした.zipファイルを解凍します。

1. **管理者**としてWindowsコマンドプロンプトを実行し、表示されるユーザーアカウント制御プロンプトに同意します。

1. Run the WindowsDefenderATPLocalOnboardingScript.cmd file that you just extracted as administrator. <bpt id="p1">**</bpt>Note:<ept id="p1">**</ept> By default the file should be in the c:\users\admin\downloads directory. Answer Y to questions presented by the script. 

1. *[プラン]* ドロップダウン リストを開き、**[Windows 10 Enterprise バージョン 21H2]** を選択します。

1. **[事前設定された構成で開始する]** を選択して続行します。

## <a name="proceed-to-exercise-3"></a>演習 3 に進む
