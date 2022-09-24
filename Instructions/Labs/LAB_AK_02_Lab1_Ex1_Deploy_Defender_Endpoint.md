---
lab:
  title: 演習 1 - Microsoft Defender for Endpoint のデプロイ
  module: Module 2 - Mitigate threats using Microsoft Defender for Endpoint
---

# <a name="module-2---lab-1---exercise-1---deploy-microsoft-defender-for-endpoint"></a>モジュール 2 - ラボ 1 - 演習 1 - Microsoft Defender for Endpoint のデプロイ

## <a name="lab-scenario"></a>ラボのシナリオ

![ラボの概要。](../Media/SC-200-Lab_Diagrams_Mod2_L1_Ex1.png)

You are a Security Operations Analyst working at a company that is implementing Microsoft Defender for Endpoint. Your manager plans to onboard a few devices to provide insight into required changes to the Security Operations (SecOps) team response procedures.

You start by initializing the Defender for Endpoint environment. Next, you onboard the initial devices for your deployment by running the onboarding script on the devices. You configure security for the environment. Lastly, you create Device groups and assign the appropriate devices.

><bpt id="p1">**</bpt>Important:<ept id="p1">**</ept>  The lab Virtual Machines are used through different modules. SAVE your virtual machines. If you exit the lab without saving, you will be required to re-run some configurations again.

>**注:**  前のモジュールのタスク 3 の手順が正常に完了していることを確認します。


### <a name="task-1-initialize-microsoft-defender-for-endpoint"></a>タスク 1:Microsoft Defender for Endpoint の初期化

このタスクでは、Microsoft Defender for Endpoint ポータルの初期化を行います。

1. 管理者として **WIN1** 仮想マシンにログインします。パスワードは **Pa55w.rd** です。  

1. Microsoft 365 Defender ポータルにまだ登録していない場合は、Microsoft Edge ブラウザーを起動します。

1. Edge ブラウザーで、 https://security.microsoft.com) の Microsoft 365 Defender ポータルに移動します。

1. **サインイン** ダイアログ ボックスで、ラボ ホスティング プロバイダーの提供した管理者ユーザー名のテナント電子メール アカウントをコピーして貼り付け、**[次へ]** を選択します。

1. **パスワードの入力**ダイアログ ボックスで、ラボ ホスティング プロバイダーの提供した管理者のテナント パスワードをコピーして貼り付け、**サインイン**します。

1. **[Microsoft 365 Defender]** ポータルのナビゲーション メニューで、左側の **[設定]** を選択します。

1. **[設定]** ページで、 **[デバイス検出]** を選択します。 

    ><bpt id="p1">**</bpt>Note:<ept id="p1">**</ept> If you do not see the <bpt id="p2">**</bpt>Device discovery<ept id="p2">**</ept> option under <bpt id="p3">**</bpt>Settings<ept id="p3">**</ept>, logout by selecting the top-right circle with your account initials and select <bpt id="p4">**</bpt>Sign out<ept id="p4">**</ept>. Other options that you might want to try is to refresh the page with Ctrl+F5 or open the page InPrivate. Login again with the <bpt id="p1">**</bpt>Tenant Email<ept id="p1">**</ept> credentials.

1. In Discovery setup make sure <bpt id="p1">**</bpt>Standard discovery (recommended)<ept id="p1">**</ept> is selected. <bpt id="p1">**</bpt>Hint:<ept id="p1">**</ept> If you do not see the option, refresh the page.


### <a name="task-2-onboard-a-device"></a>タスク 2:デバイスのオンボード

このタスクでは、オンボード スクリプトを使用してデバイスを Microsoft Defender for Endpoint にオンボードします。

1. ブラウザーに Microsoft 365 Defender ポータルが表示されていない場合は、Microsoft Edge ブラウザーを起動し、(https://security.microsoft.com) にアクセスして、**テナントの電子メール**の資格情報でログインします。

1. 左側のメニュー バーから **[設定]** を選択し、設定 ページから **[エンドポイント]** を選択します。

1. デバイス管理セクションで **[オンボーディング]** を選択します。

1. あなたは Microsoft Defender for Endpoint を実装している企業で働いているセキュリティ運用アナリストです。

1. ダウンロードした zip ファイルを右クリックし、 **[すべて展開]** を選択し、 *[完了時に展開されたファイルを表示する]* チェックボックスがオンになっていることを確認し、 **[抽出]** を選択します。

1. あなたの上司は、いくつかのデバイスをオンボードして、セキュリティ オペレーション (SecOps) チームの応答手順で必要な変更に関する情報を提供しようとしています。

1. Right-click on the extracted file "WindowsDefenderATPLocalOnboardingScript.cmd" again and choose <bpt id="p1">**</bpt>Run as Administrator<ept id="p1">**</ept>.  <bpt id="p1">**</bpt>Hint:<ept id="p1">**</ept> If you encounter the Windows SmartScreen window, select on <bpt id="p2">**</bpt>More info<ept id="p2">**</ept>, and choose <bpt id="p3">**</bpt>Run anyway<ept id="p3">**</ept>. 
    
1. 最初に、Defender for Endpoint 環境を初期化します。

1. 次に、デバイスでオンボード スクリプトを実行し、デプロイ対象の初期デバイスをオンボードします。

1. 環境のセキュリティを構成します。  

1. WIN1 仮想マシンの Windows 検索バーで「**CMD**」と入力し、コマンド プロンプト アプリの右側のペインで **[管理者として実行]** を選択します。 

1. [ユーザー アカウント制御] ウィンドウが表示されたら **[はい]** を選択し、アプリの実行を許可します。 

1. 最後に、デバイス グループを作成し、適切なデバイスを割り当てます。

1. In the Microsoft 365 Defender portal, in the left-hand menu, under the <bpt id="p1">**</bpt>Assets<ept id="p1">**</ept> area, select <bpt id="p2">**</bpt>Devices<ept id="p2">**</ept>. If the device is not shown, complete the next task and come back to check it back later. It can take up to 60 minutes for the first device to be displayed in the portal.

    >**注:**  オンボード プロセスを完了してから 1 時間経ってもデバイス一覧にデバイスが表示されない場合は、オンボードまたは接続に問題があるおそれがあります。


### <a name="task-3-configure-roles"></a>タスク 3:ロールの構成

このタスクでは、デバイス グループで使用するロールを設定します。

1. Microsoft 365 Defender ポータルで、左側のメニューバーから **[設定]** を選択し、 **[エンドポイント]** を選択します。 

1. [アクセス許可] 領域で、**[ロール]** を選択します。

1. **[ロールをオンにする]** ボタンを選択します。

1. **[+ 項目の追加]** を選択します。

1. ロールの追加 ダイアログで以下を入力します。

    |全般設定|値|
    |---|---|
    |ロール名|**第一層サポート**|
    |アクセス許可|ライブ応答機能 - 詳細設定|

1. **重要:** ラボの Virtual Machines は、さまざまなモジュールで使用されます。

1. **[保存]** を選択します。


### <a name="task-4-configure-device-groups"></a>タスク 4:デバイス グループの構成

このタスクでは、アクセス コントロールと自動化の設定が可能なデバイス グループを構成します。

1. Microsoft 365 Defender ポータルで、左側のメニューバーから **[設定]** を選択し、 **[エンドポイント]** を選択します。 

1. アクセス許可領域で **[デバイス グループ]** を選択します。

1. **[デバイス グループの追加]** アイコンを選択します。

1. 全般 タブに次の情報を入力します。

    |全般設定|値|
    |---|---|
    |デバイス グループ名|**Regular**|
    |自動化レベル|Full - remediate threats automatically (完全 - 脅威を自動的に修復する)|

1. **[次へ]** を選択します。

1. [デバイス] タブの OS 条件で、**[Windows 10]** を選択し、**[次へ]** を選択します。

1. 仮想マシンを保存します。

1. 保存せずにラボを終了する場合は、構成を再実行する必要があります。

1. **[完了]** を選択します。

1. Device group configuration has changed. Select <bpt id="p1">**</bpt>Apply changes<ept id="p1">**</ept> to check matches and recalculate groupings.

1. これで、先ほど作成した "Regular" と "グループに属していないデバイス (既定)" という 2 つのデバイス グループが同じ修復レベルで表示されます。

## <a name="proceed-to-exercise-2"></a>演習 2 に進みます。
