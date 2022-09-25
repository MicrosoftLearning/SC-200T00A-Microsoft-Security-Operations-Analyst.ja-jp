---
lab:
  title: 演習 1 - データ コネクタを使用して Microsoft Sentinel にデータを接続する
  module: Module 6 - Connect logs to Microsoft Sentinel
---

# <a name="module-6---lab-1---exercise-1---connect-data-to-microsoft-sentinel-using-data-connectors"></a>モジュール 6 - ラボ 1 - 演習 1 - データ コネクタを使用して Microsoft Sentinel にデータを接続する

## <a name="lab-scenario"></a>ラボのシナリオ

![ラボの概要。](../Media/SC-200-Lab_Diagrams_Mod6_L1_Ex1.png)

You are a Security Operations Analyst working at a company that implemented Microsoft Sentinel. You must learn how to connect log data from the many data sources in your organization. The organization has data from Microsoft 365, Microsoft 365 Defender, Azure resources, non-azure virtual machines, etc. You start connecting the Microsoft sources first.


### <a name="task-1-access-the-microsoft-sentinel-workspace"></a>タスク 1:Microsoft Sentinel ワークスペースにアクセスする

このタスクでは、Microsoft Sentinel ワークスペースにアクセスします。

1. 管理者として **WIN1** 仮想マシンにログインします。パスワードは **Pa55w.rd** です。  

1. Microsoft Edge ブラウザーを開きます。

1. Edge ブラウザーで、Azure portal (https://portal.azure.com ) に移動します。

1. **サインイン** ダイアログ ボックスで、ラボ ホスティング プロバイダーから提供された**テナントの電子メール** アカウントをコピーして貼り付け、**[次へ]** を選択します。

1. **[パスワードの入力]** ダイアログ ボックスで、ラボ ホスティング プロバイダーから提供された**テナント パスワード**をコピーして貼り付け、**[サインイン]** を選択します。

1. Azure portal の検索バーに「*Sentinel*」と入力し、**[Microsoft Sentinel]** を選択します。

1. 前のラボで作成した Microsoft Sentinel ワークスペースを選択します。


### <a name="task-2-connect-the-azure-active-directory-connector"></a>タスク 2:Azure Active Directory コネクタを接続する

このタスクでは、Azure Active Directory コネクタを Microsoft Sentinel に接続します。

1. Under the Configuration area select <bpt id="p1">**</bpt>Data connectors<ept id="p1">**</ept>. In the Data Connectors page, search for the <bpt id="p1">**</bpt>Azure Active Directory<ept id="p1">**</ept> connector and select it from the list.

1. コネクタ情報ブレードで **[コネクタ ページを開く]** を選択します。

1. 構成領域から **[サインイン ログ]** と **[監査ログ]** オプションを選択し、**[変更の適用]** を選択します。


### <a name="task-3-connect-the-azure-active-directory-identity-protection-connector"></a>タスク 3:Azure Active Directory Identity Protection コネクタを接続する

このタスクでは、Azure Active Directory Identity Protection コネクタを Microsoft Sentinel に接続します。

1. [データ コネクタ] タブで、一覧から **Azure Active Directory Identity Protection** コネクタを探して選択します。

1. コネクタ情報ブレードで **[コネクタ ページを開く]** を選択します。

1. 構成 領域から **接続** ボタンを選択します。


### <a name="task-4-connect-the-microsoft-defender-for-cloud-connector"></a>タスク 4:Microsoft Defender for Cloud に接続する

このタスクでは、Microsoft Defender for Cloud コネクタを接続します。

1. [データ コネクタ] タブで、一覧から **Microsoft Defender for Cloud** コネクタを探して選択します。

1. コネクタ情報ブレードで **[コネクタ ページを開く]** を選択します。

1. 構成領域の [サブスクリプション] で、[Azure Pass - スポンサー プラン] サブスクリプションのチェック ボックスをオンにし、 **[状態]** オプションを右側にスライドして **[接続済み]** を示します。

1. [状態] が *[接続済み]* になり、[双方向の同期] が *[有効]* になるはずです。

1. Scroll down and under the "Create incidents - Recommended!" area, select <bpt id="p1">**</bpt>Enable<ept id="p1">**</ept>. This option creates an Analytics rule automatically for this service. You can manually add it later if not enabled here or change its configuration within the <bpt id="p1">*</bpt>Analytics<ept id="p1">*</ept> blade.


### <a name="task-5-connect-the-microsoft-365-defender-connector"></a>タスク 5:Microsoft 365 Defender コネクタを接続する

このタスクでは、Microsoft 365 Directory コネクタを接続します。

1. [データ コネクタ] タブで、一覧から **Microsoft 365 Defender (プレビュー)** コネクタを探して選択します。

1. コネクタ情報ブレードで **[コネクタ ページを開く]** を選択します。

1. [構成] 領域で **[Connect Incident and Alerts](インシデントとアラートの接続)** を選択します。 

1. [イベントの接続] で、 **[名前]** チェック ボックスをオンにして、"Microsoft Defender for Endpoint" のすべてのチェック ボックスをオンにします。

1. "Microsoft Defender for Office 365" について同じことを繰り返します。

1. ページの下部までスクロールし、 **[変更の適用]** を選択します。


### <a name="task-6-connect-the-azure-activity-connector"></a>タスク 6:Azure Activity コネクタを接続する

このタスクでは、Azure Activity コネクタを接続します。

1. [データ コネクタ] タブで、一覧から **Azure Activity** コネクタを探して選択します。

1. コネクタ情報ブレードで **[コネクタ ページを開く]** を選択します。

1. In the Configuration area, scroll down and under "2. Connect your subscriptions..." select <bpt id="p1">**</bpt>Launch Azure Policy Assignment Wizard&gt;<ept id="p1">**</ept>.

1. **[基本]** タブで、 **[スコープ]** の下にある省略記号ボタン [...] を選択し、ドロップダウン リストから [Azure Pass - スポンサーシップ] サブスクリプションを選択して、 **[選択]** をクリックします。

1. **[パラメーター]** タブを選択し、 **[プライマリ Log Analytics ワークスペース]** ドロップダウン リストから自分の *uniquenameDefender* ワークスペースを選択します。

1. **[修復]** タブを選択し、 **[修復タスクの作成]** チェック ボックスをオンにします。

1. **[確認と作成]** ボタンを選択して構成を確認します。

1. **[作成]** を選択して完了します。

## <a name="proceed-to-exercise-2"></a>演習 2 に進みます。
