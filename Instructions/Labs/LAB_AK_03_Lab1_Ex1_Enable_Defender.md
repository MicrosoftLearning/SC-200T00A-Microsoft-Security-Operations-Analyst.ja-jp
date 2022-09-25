---
lab:
  title: 演習 1 - Microsoft Defender for Cloud の有効化
  module: Module 3 - Mitigate threats using Microsoft Defender for Cloud
---

# <a name="module-3---lab-1---exercise-1---enable-microsoft-defender-for-cloud"></a>モジュール 3 - ラボ 1 - 演習 1 - Microsoft Defender for Cloud の有効化

## <a name="lab-scenario"></a>ラボのシナリオ

![ラボの概要。](../Media/SC-200-Lab_Diagrams_Mod3_L1_Ex1.png)

You are a Security Operations Analyst working at a company that is implementing cloud workload protection with Microsoft Defender for Cloud.  In this lab you will enable Microsoft Defender for Cloud.


### <a name="task-1-access-the-azure-portal-and-set-up-a-subscription"></a>タスク 1:Azure portal にアクセスしてサブスクリプションを設定する

このタスクでは、このラボと今後のラボを完了するために必要なAzureサブスクリプションを設定します。

1. 管理者として **WIN1** 仮想マシンにログインします。パスワードは **Pa55w.rd** です。  

1. Microsoft Edge ブラウザーを開くか、既に開いている場合は新しいタブを開きます。

1. Edge ブラウザーで、Azure portal (https://portal.azure.com) ) に移動します。

1. **サインイン** ダイアログ ボックスで、ラボ ホスティング プロバイダーの提供した管理者ユーザー名のテナント電子メール アカウントをコピーして貼り付け、**[次へ]** を選択します。

1. **パスワードの入力**ダイアログ ボックスで、ラボ ホスティング プロバイダーの提供した管理者のテナント パスワードをコピーして貼り付け、**サインイン**します。

1. Azureポータルの検索バーに「*サブスクリプション*」を入力し「**サブスクリプション**」を選択します。 

1. If the <bpt id="p1">*</bpt>"Azure Pass - Sponsorship"<ept id="p1">*</ept> subscription is shown (or equivalent name in your selected language), proceed to Task #2. Otherwise, ask your instructor on how to create the Azure subscription with your tenant admin user credentials. <bpt id="p1">**</bpt>Note:<ept id="p1">**</ept> The subscription creation process could take up to 10 minutes. 

    >**重要:** これらのラボは、クラス中に 10 米ドル未満の Azure サービスを使用するように設計されています。


### <a name="task-2-create-a-log-analytics-workspace"></a>タスク 2:Log Analytics ワークスペースを作成する

このタスクでは、Microsoft Defender for Cloud で使用する Log Analytics ワークスペースを作成します。

1. Azure portal の検索バーに「*Log Analytics* ワークスペース」を入力し、同じサービス名を選択します。

1. コマンド バーから [**+ 作成**] を選択します。

1. リソース グループの **[新規作成]** を選択します。

1. 「*RG-Defender*」と入力し、**[OK]** を選択します。

1. 名前には、*uniquenameDefender* のように一意の名前を入力します。

1. **[確認および作成]** を選択します。

1. Once the workspace validation has passed, select <bpt id="p1">**</bpt>Create<ept id="p1">**</ept>. Wait for the new workspace to be provisioned, this may take a few minutes.


### <a name="task-3-enable-microsoft-defender-for-cloud"></a>タスク 3:Microsoft Defender for Cloud を有効にする

このタスクでは、Microsoft Defender for Cloud を有効にして構成します。

1. Azure portal の検索バーに「*Defender*」と入力し、**[Microsoft Defender for Cloud]** を選択します。

1. On the <bpt id="p1">**</bpt>Getting started<ept id="p1">**</ept> page, under the <bpt id="p2">**</bpt>Upgrade<ept id="p2">**</ept> tab, make sure your subscription is selected, and then select the <bpt id="p3">**</bpt>Upgrade<ept id="p3">**</ept> button at the bottom of the page. Wait for the <bpt id="p1">*</bpt>Trial started<ept id="p1">*</ept> notification to appear, it takes about 2 minutes. <bpt id="p1">**</bpt>Hint:<ept id="p1">**</ept> You can click the bell button on the top bar to review your Azure portal notifications.

1. The next page shows the option to install the agent on virtual machines already in the subscription. Select <bpt id="p1">**</bpt>Continue without installing agents<ept id="p1">**</ept> or <bpt id="p2">**</bpt>Do nothing here<ept id="p2">**</ept>.

1. ポータル メニューの管理領域で **[環境設定]** を選択します。

1. **"Azure Pass - スポンサー"** サブスクリプション (または、お使いの言語の同等の名前) を選択します。 

1. *[すべての Microsoft Defender for Cloud プランの有効化]* で有効化されている機能と、 *[Microsoft Defender for]* 列で保護されている Azure リソースを確認します。

1. 設定領域から **[自動プロビジョニング]** を選択します。

1. あなたは、Microsoft Defender for Cloud を使用してクラウド ワークロード保護を実装している企業に勤務するセキュリティ運用アナリストです。

1. ページの右上にある [x] を選択して [設定] ページを閉じ、 **[環境設定]** に戻って、サブスクリプションの左側にある [>] を選択します。

1. このラボでは、Microsoft Defender for Cloud を有効にします。

    >**注:**  そのページが表示されない場合は、Edge ブラウザーを最新の情報に更新して、もう一度やり直してください。


### <a name="task-4-install-azure-arc-on-an-on-premises-server"></a>タスク 4:オンプレミスのサーバーに Azure Arc をインストールする

このタスクでは、オンボードを簡単にするために、オンプレミスのサーバーに Azure Arc をインストールします。

><bpt id="p1">**</bpt>Important:<ept id="p1">**</ept> The next steps are done in a different machine than the one you were previously working. Look for the Virtual Machine name references.

1. Log in to <bpt id="p1">**</bpt>WINServer<ept id="p1">**</ept> virtual machine as Administrator with the password: <bpt id="p2">**</bpt>Passw0rd!<ept id="p2">**</ept> if required.  

1. Microsoft Edge ブラウザーを開き、Azure portal (https://portal.azure.com ) に移動します。

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

1. **[登録]** を選択します (手順 "1. ** サブスクリプションを登録")。

    >**注:**  処理のために少なくとも 3 分待ちます。

1. Scroll down and select the <bpt id="p1">**</bpt>Download<ept id="p1">**</ept> button. <bpt id="p1">**</bpt>Hint:<ept id="p1">**</ept> if your browser blocks the download, take action in the browser to allow it. In Edge Browser, select the ellipsis button (...) if needed and then select <bpt id="p1">**</bpt>Keep<ept id="p1">**</ept>. 

1. Windows の [スタート] ボタンを右クリックし、**[Windows PowerShell (管理者)]** を選択します。

1. Enter <bpt id="p1">*</bpt>Administrator<ept id="p1">*</ept> for "Username" and <bpt id="p2">*</bpt>Passw0rd!<ept id="p2">*</ept> for "Password" if you get a UAC prompt.

1. 「cd C:\Users\Administrator\Downloads」と入力します。

1. *Set-ExecutionPolicy -ExecutionPolicy Unrestricted* を入力しEnterキーを押します。

1. [すべてにはい] の場合は「**A**」を入力し、Enter キーを押します。

1. 「*.\OnboardingScript.ps1*」と入力し、Enter キーを押します。  

    ><bpt id="p1">**</bpt>Important:<ept id="p1">**</ept> If you get the error <bpt id="p2">*</bpt>"The term .\OnboardingScript.ps1 is not recognized..."<ept id="p2">*</ept>, make sure you are doing the steps for Task 4 in the WINServer virtual machine. Other issue might be that the name of the file changed due to multiple downloads, search for <bpt id="p1">*</bpt>".\OnboardingScript (1).ps1"<ept id="p1">*</ept> or other file numbers in the running directory.

1. **R** を入力して 1 回実行し、Enter キーを押します (これには数分かかる場合があります)。

1. Edge ブラウザーに戻って新しいタブを開き、アドレス バーに「https://microsoft.com/devicelogin」と入力します。

1. [Windows PowerShell] ウィンドウに戻り、スクリプトの最後の行で "... コードの入力" の後に表示されている、エージェントを認証するためのコードをコピーします。**

1. Go back to the Edge browser and paste it in the <bpt id="p1">**</bpt>Code<ept id="p1">**</ept> box and select <bpt id="p2">**</bpt>Next<ept id="p2">**</ept>. Select your tenant admin account and select <bpt id="p1">**</bpt>Continue<ept id="p1">**</ept> in the <bpt id="p2">*</bpt>Are you trying to sign in to Azure Connected Machine Agent?<ept id="p2">*</ept> window. 

1. Go back to the Windows PowerShell window and wait for the message <bpt id="p1">*</bpt>"Successfully Onboarded Resource to Azure"<ept id="p1">*</ept>. <bpt id="p1">**</bpt>Note:<ept id="p1">**</ept> If you see a message line with a new authentication code, you need to repeat the last 3 steps again.

1. *Azure Pass - スポンサー* サブスクリプション (または、選択した言語で同等の名前) が表示されている場合は、タスク #2 に進みます。

1. WINServer サーバー名が表示されるまで **[更新]** を選択します。

    >**注:**  この処理には数分かかります。


### <a name="task-5-protect-an-on-premises-server"></a>タスク 5:オンプレミスのサーバーを保護する

このタスクでは、必要なエージェントを **WINServer** 仮想マシンに手動でインストールします。

1. **[Microsoft Defender for Cloud]** にアクセスし、 **[作業の開始]** ページを選択します。

1. **[作業の開始]** タブを選択します。

1. *[非 Azure サーバーの追加]* セクションで **[構成]** を選択します。

1. それ以外の場合は、テナント管理者のユーザー資格情報を使用して Azure サブスクリプションを作成する方法について、インストラクターに確認してください。

1. 前に作成したワークスペースの横にある **[+ サーバー追加]** を選択します。

1. **[Download Windows Agent (64 bit)]** を選択します。

1. **[ファイルを開く]** を選択し、ダウンロードした *MMASetup-AMD64.exe* ファイルを実行します。

1. ウィザードの **[エージェントのセットアップ オプション]** ページが表示されるまで **[次へ]** を選択し、 **[Connect the Agent to Azure Log Analytics (OMS)]\(エージェントを Azure Log Analytics (OMS) に接続する\)** を選択して、 **[次へ]** を選択します。

1. 必要に応じて、Azure portal から **[ワークスペース キー]** テキスト ボックスの**ワークスペース ID** と**主キー**の値をコピーし、ウィザード ページのフィールドに貼り付け、 **[次へ]** を選択します。

1. **注:**  サブスクリプションの作成プロセスは最大 10 分かかることがあります。

1. "Microsoft Defender for Cloud" のポータルにアクセスして、 **[インベントリ]** を選択します。

1. The <bpt id="p1">**</bpt>WINServer<ept id="p1">**</ept> virtual machine will appear after at least 5 minutes. You may have to select <bpt id="p1">**</bpt>Refresh<ept id="p1">**</ept> to see it. <bpt id="p1">**</bpt>Hint:<ept id="p1">**</ept> If you see the number 1 under <bpt id="p2">*</bpt>Total resources<ept id="p2">*</ept> remove the filter to show the <bpt id="p3">*</bpt>WINServer<ept id="p3">*</ept> virtual machine.

1. 次のラボに進み、後から戻って **Microsoft Defender for Cloud** の **[インベントリ]** セクションを確認することができます。

## <a name="proceed-to-exercise-2"></a>演習 2 に進みます。
