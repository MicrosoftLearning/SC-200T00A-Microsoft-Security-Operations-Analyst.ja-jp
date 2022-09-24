
# <a name="microsoft-security-operations-analyst"></a>Microsoft Security Operations Analyst
講師用準備ガイド

## <a name="purpose"></a>目的 

This document is for presenters preparing to teach the Microsoft Security Virtual Training Day for "Defend against threats and Secure CLoud Environments". This material is a subset of the SC-200: Microsoft Security Operations Analyst certification course.

## <a name="demo-prerequisites"></a>デモの前提条件

このコースのラボでは、Microsoft 365 E5ライセンスのテナントと、Azureサブスクリプションの両方が必要です。

* ご自身のために Microsoft Learning Azure Pass を要求できます。
* Ensure that you request these passes at least two weeks before you will be performing the demos. After receiving the pass, you will need to activate it. 
* The Azure pass effectively functions in the same way as the publicly available Microsoft Azure Trial Subscription. This means there are limitations on what you can do with the pass.
* ラボの手順は、[SC-200 Microsoft Learning Github](https://github.com/MicrosoftLearning/SC-200T00A-Microsoft-Security-Operations-Analyst/tree/master/Instructions/VTD_Demos/) リポジトリにあります。
* デモに使用するコンピューターに新しい Microsoft Edge ブラウザーがインストールされていることを確認してください。

## <a name="activate-azure-pass"></a>Activate Azure Pass

## <a name="deploy-defender-for-endpoint"></a>Defender for Endpoint のデプロイ

### <a name="obtain-your-microsoft-365-credentials"></a>Microsoft 365 資格情報の取得

Once you launch the lab, a free trial tenant will be made available to you to access in the Microsoft Virtual Lab environment. This tenant will be automatically assigned a unique username and password. You must retrieve this username and password so that you can sign in to Azure and Microsoft 365 within the Microsoft Virtual Lab environment. 

このドキュメントは、''脅威に対する防御とクラウド環境の保護'' のための Microsoft Security Virtual Training Day を教える準備をしている発表者向けです。

    - この資料は SC-200:Microsoft Security Operations Analyst 認定コースのサブセットです。
    - <bpt id="p1">**</bpt>Tenant password.<ept id="p1">**</ept> This is the password for the admin account provided by your lab hosting provider.
    

### <a name="initialize-microsoft-defender-for-endpoint"></a>Microsoft Defender for Endpoint の初期化

このタスクでは、Microsoft Defender for Endpoint の初期化を行います。


1. 管理者として WIN1 仮想マシンにログインします。パスワードは**Pa55w.rd**。  

1. Open the Microsoft Edge browser, search for "edge browser update", download, and install the new Microsoft Edge browser. This is necessary to ensure you're running the latest version of Microsoft Edge in your hosted virtual machine. Start the new Edge browser.

1. Edge ブラウザーで、 https://security.microsoft.com) の Microsoft 365 Defender ポータルに移動します。

1. **[サインイン]** ダイアログ ボックスで、ラボ ホスティング プロバイダーから提供された管理者ユーザー名のテナント電子メール アカウントをコピーして貼り付け、**[次へ]** を選択します。

1. **パスワードの入力**ダイアログ ボックスで、ラボ ホスティング プロバイダーの提供した管理者のテナント パスワードをコピーして貼り付け、**サインイン**します。

<bpt id="p1">**</bpt>Note<ept id="p1">**</ept>: if you receive a message "You can't access this section.",  wait 5 minutes and try again.  Sometimes the access rules need to propagate the tenant.

1. Microsoft 365 Defender ポータルの左側のメニュー セクションで、[設定] まで下にスクロールします。

1. [設定] で、[エンドポイント] を選択します。

1. [全般] セクションに [データ保有期間] の選択肢が表示されます。

<bpt id="p1">**</bpt>Note<ept id="p1">**</ept>: In the hosted lab environment your data storage location should be selected for you. And, it should be in the appropriate Geography for where this training tenant is being managed. You can still select the Data Retention length, but it is not required.

1. [エンドポイント]、[全般] で、[高度な機能] を選択します。

1. 機能のリストを下にスクロールし、プレビュー機能が **[オン]** であることを確認します。

1. そうでない場合は、スライダーを **[オン]** の位置に移動し、 **[ユーザー設定の保存]** を選択します。  

デモを実行する少なくとも 2 週間前に、これらのパスを要求してください。  

### <a name="onboard-a-device"></a>デバイスのオンボード

このタスクでは、デバイスを Microsoft Defender for Endpoint にオンボードします。

1. Microsoft 365 Defender ポータル (https://security.microsoft.com) ) に移動し、現在ポータルにいない場合は、**テナントの電子メール**資格情報を使用してログインします。

1. 左側のメニュー バーで **[設定]** を選択します。

1. **[エンドポイント]** を選択し、[デバイス管理] セクションで **[オンボード]** を選択します。

1. デバイスのオンボード領域で **[パッケージのダウンロード]** ボタンを選択します。

1. ダウンロードされた zip ファイルをローカル フォルダーに抽出します (［ドキュメント］ フォルダーなど)。

1. パスを受け取った後、そのパスを有効にする必要があります。

**注** 既定で、ファイルは [c:\users\admin\downloads] ディレクトリにあります。
    
1. Answer <bpt id="p1">**</bpt>Y<ept id="p1">**</ept> to questions presented by the script. When complete you should see a message in the command screen that says something like "Successfully onboarded machine..." 

1. Azure Pass は、一般に公開されている Microsoft Azure 試用版サブスクリプションと同じ方法で、効果的に機能します。

1. これは、パスで実行できる操作には制限があることを意味します。

**注** デバイスがポータルに表示されるまでに最高 5 分かかることがあります。


### <a name="configure-role"></a>ロールの構成

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

### <a name="configure-device-groups"></a>デバイス グループの構成

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

1. . On the Devices tab, for the OS condition select <bpt id="p1">**</bpt>Windows 10<ept id="p1">**</ept> and select <bpt id="p2">**</bpt>Next<ept id="p2">**</ept>.

1. On the Preview devices tab, select <bpt id="p1">**</bpt>Show preview<ept id="p1">**</ept> to see the WIN1 virtual machine. Select <bpt id="p1">**</bpt>Next<ept id="p1">**</ept>. 
<bpt id="p1">**</bpt>Hint:<ept id="p1">**</ept> If you do not see the virtual machine in the preview list, go back and select also <bpt id="p2">*</bpt>None<ept id="p2">*</ept> for the OS condition. The data for the VM is not populated yet.

1. [ユーザー アクセス] タブで、**[sg-IT]** を選択し、**[選択したグループを追加する]** を選択します

1. **[完了]** を選択します。

1. Device group configuration has changed. Select <bpt id="p1">**</bpt>Apply changes<ept id="p1">**</ept> to check matches and recalculate groupings.

1. これで、先ほど作成した "Regular" と "グループに属していないデバイス (既定)" という 2 つのデバイス グループが同じ修復レベルで表示されます。


## <a name="deploy-sample-alerts-for-demo-in-module-3"></a>モジュール 3 でデモのサンプル アラートをデプロイする

このタスクでは、サンプルのセキュリティアラートを読み込み、アラートの詳細を確認します。

1. Edge ブラウザーで Azure portal (https://portal.azure.com) を開きます。

1. **[サインイン]** ダイアログ ボックスで、ラボ ホスティング プロバイダーから提供された**テナントの電子メール** アカウントをコピーして貼り付け、 **[次へ]** を選択します。

1. **[パスワードの入力]** ダイアログ ボックスで、ラボ ホスティング プロバイダーから提供された**テナントのパスワード**をコピーして貼り付け、 **[サインイン]** を選択します。

1. Azure portal の検索バーに「*Defender*」と入力し、**[Microsoft Defender for Cloud]** を選択します。

1. **[作業の開始]** メニューの既定の選択肢は **[アップグレード]** です。これを選択するか、今は**スキップ**します。

1. ポータルメニューで **[セキュリティアラート]** を選択します。

1. コマンド バーから **[サンプルアラート]** を選択します。

1. In the Create sample alerts (Preview) pane make sure your subscription is selected.  Make sure all sample alerts are selected and select <bpt id="p1">**</bpt>Create sample alerts<ept id="p1">**</ept>.  

**注**: これは完了するまでに数分かかる場合があります。

## <a name="deploy-microsoft-sentinel-workspace-for-demo-in-module-4"></a>モジュール 4 でデモ用の Microsoft Sentinel ワークスペースをデプロイする

このタスクでは、Microsoft Sentinel ワークスペースを作成します。

1. Edge ブラウザーで、Azure portal (https://portal.azure.com ) に移動します。

1. **[サインイン]** ダイアログ ボックスで、ラボ ホスティング プロバイダーから提供された**テナントの電子メール** アカウントをコピーして貼り付け、 **[次へ]** を選択します。

1. **[パスワードの入力]** ダイアログ ボックスで、ラボ ホスティング プロバイダーから提供された**テナントのパスワード**をコピーして貼り付け、 **[サインイン]** を選択します。

1. Azure portal の検索バーに「*Sentinel*」と入力し、**[Microsoft Sentinel]** を選択します。

1. **[+ 作成]** を選択します。

1. **[+ 新しいワークスペースの作成]** を選択します。

**注** まず、新しい Log Analytics ワークスペースを作成します。

1. 適切なサブスクリプションを選択します。

1. リソースグループの**新規作成** リンクを選択し、選択した新しいリソースグループ名を入力します。

1. 名前 フィールドの インスタンスの詳細 で、LogAnalyticsワークスペースに選択する名前を入力します。

**注:**  この名前は一意である必要があり、Microsoft Sentinel ワークスペース名でもあります。

1. Select the region that is appropriate for you.  The appropriate region may default or your instructor may have specific advice on which region to select.  

1. **[確認および作成]** を選択します。

1. Select <bpt id="p1">**</bpt>Create<ept id="p1">**</ept>. Wait for the new Log Analytics workspace to appear in the list on the Add Microsoft Sentinel to a workspace page.  This may take a minute.

1. 新しく作成したワークスペースが表示されたら、それを選択し、**[追加]** を選択します。

## <a name="create-data-connectors-for-microsoft-sentinel"></a>Microsoft Sentinel 用のデータ コネクタを作成する

### <a name="task-1-access-the-microsoft-sentinel-workspace"></a>タスク 1:Microsoft Sentinel ワークスペースにアクセスする。

このタスクでは、Microsoft Sentinel ワークスペースにアクセスします。

1. 管理者として WIN1 仮想マシンにログインします。パスワードは**Pa55w.rd**。  

1. ラボを起動すると、無料のトライアル テナントを利用して Microsoft Virtual Lab 環境にアクセスできるようになります。

1. Edge ブラウザーで、Azure portal (https://portal.azure.com ) に移動します。

1. **[サインイン]** ダイアログ ボックスで、ラボ ホスティング プロバイダーから提供された**テナントの電子メール** アカウントをコピーして貼り付け、 **[次へ]** を選択します。

1. **[パスワードの入力]** ダイアログ ボックスで、ラボ ホスティング プロバイダーから提供された**テナントのパスワード**をコピーして貼り付け、 **[サインイン]** を選択します。

1. Azure portal の検索バーに「*Sentinel*」と入力し、**[Microsoft Sentinel]** を選択します。

1. 前のラボで作成した Microsoft Sentinel ワークスペースを選択します。

### <a name="task-2-connect-the-azure-active-directory-connector"></a>タスク 2:Azure Active Directory コネクタを接続する

このタスクでは、Azure アクティビティ データ コネクタを接続します。

1. このテナントには自動的に一意のユーザー名とパスワードが割り当てられます。

1. [コネクタ情報] ブレードで **[コネクタ ページを開く]** を選択します。

1. 構成領域から **[サインイン ログ]** と **[監査ログ]** オプションを選択し、**[変更の適用]** を選択します。

### <a name="task-3-connect-the-azure-active-directory-identity-protection-connector"></a>タスク 3:Azure Active Directory Identity Protection コネクタを接続する

このタスクでは、Azure Active Directory Identity Protection コネクタを接続します。

1. [データ コネクタ] タブで、リストから **[Azure Active Directory Identity Protection]** コネクタを選択します。

1. [コネクタ情報] ブレードで **[コネクタ ページを開く]** を選択します。

1. **[接続]** を選択します。

### <a name="task-4-connect-the-microsoft-defender-for-cloud-connector"></a>タスク 4:Microsoft Defender for Cloud コネクタを接続する。

このタスクでは、Microsoft Defender for Cloud コネクタを接続します。

1. [データ コネクタ] タブで、リストから **[Microsoft Defender for Cloud]** コネクタを選択します。

1. [コネクタ情報] ブレードで **[コネクタ ページを開く]** を選択します。

1. Microsoft Virtual Lab 環境で Azure と Microsoft 365 にサインインするには、このユーザー名とパスワードを取得する必要があります。

### <a name="task-5-connect-the-microsoft-defender-for-cloud-apps-connector"></a>タスク 5:Microsoft Defender for Cloud Apps コネクタを接続する。

このタスクでは、Microsoft Defender for Cloud Apps コネクタを接続します。

1. [データ コネクタ] タブで、リストから **[Microsoft Defender for Cloud Apps]** コネクタを選択します。

1. [コネクタ情報] ブレードで **[コネクタ ページを開く]** を選択します。

1. **[構成]** セクションの **[手順]** タブで、 **[アラート]** を選択してから、 **[変更の適用]** を選択します。

### <a name="task-6-connect-the-microsoft-defender-for-office-365-connector"></a>タスク 6:Microsoft Defender for Office 365 に接続する

このタスクでは、Microsoft Defender for Office 365 コネクタを接続します。

1. [データ コネクタ] タブで、一覧から **[Microsoft Defender for Office 365]** コネクタを選択します。

1. [コネクタ情報] ブレードで **[コネクタ ページを開く]** を選択します。

1. **[接続]** を選択します。

### <a name="task-7-connect-the-microsoft-defender-for-identity-connector"></a>タスク 7:Microsoft Defender for forIdentity コネクタに接続する

このタスクでは、Microsoft Defender for Identity コネクタを接続します。

1. [データ コネクタ] タブで、一覧から **[Microsoft Defender for Identity]** コネクタを選択します。

1. [コネクタ情報] ブレードで **[コネクタ ページを開く]** を選択します。

1. Review the Connecting Options. Don't connect. This is for informational purposes only.

### <a name="task-8-connect-the-microsoft-defender-for-endpoint-connector"></a>タスク 8:Microsoft Defender for Endpointコネクタに接続する

このタスクでは、Microsoft Defender for Endpoint コネクタを接続します。

1. [データ コネクタ] タブで、一覧から **[Microsoft Defender for Endpoint]** コネクタを選択します。

1. [コネクタ情報] ブレードで [コネクタ ページを開く] を選択します。

1. **[接続]** を選択します。

### <a name="task-9-connect-the-microsoft-365-defender-connector"></a>タスク 9:Microsoft 365 Defender コネクタを接続する

このタスクでは、Microsoft 365 Directory コネクタを接続します。

1. [データ コネクタ] タブで、一覧から **[Microsoft 365 Defender]** コネクタを選択します。

1. [コネクタ情報] ブレードで **[コネクタ ページを開く]** を選択します。

1. Microsoft Defender for Endpointのすべてのチェックボックスを選択します。

1. **[変更の適用]** を選択します。

### <a name="task-3-connect-a-non-azure-windows-machine"></a>タスク 3:非 Azure Windows マシンを接続する。

このタスクでは、非 Azure Windows 仮想マシンを Microsoft Sentinel に接続します。

1. 管理者として、次のパスワードを使用して WIN2 仮想マシンにログインします:**Pa55w.rd**。  

1. このコースは、学習パートナーが複数の認証済みラボ ホスティング プロバイダーのいずれかを使用して実施することもあり、お使いになっているテナントに関連のあるテナント ID を取得する実際の手順はラボ ホスティング プロバイダーに応じて異なります。

1. ブラウザーを開き、ご自身の資格情報を使用して Azure Portal (https://portal.azure.com ) にログインします。

1. Azure Portal の検索バーに「*Sentinel*」と入力し、**[Microsoft Sentinel]** を選択します。

1. Microsoft Sentinel ワークスペースを選択します。

1. [データ コネクタ] タブで、リストから **[レガシ エージェントを使用したセキュリティ イベント]** コネクタを選択します。

1. [コネクタ情報] ブレードで **[コネクタ ページを開く]** を選択します。

1. ストリーミングするイベントの選択領域で、**[すべてのイベント]** を選択し、**[変更の適用]** を選択します。

1. **[非 Azure Windows マシンにエージェントをインストールする]** を選択します。

このため、コース内での当該情報の取得方法については、講師が必要な指示を行います。

1. **[Azure 以外の Windows マシンのエージェントをダウンロードしてインストールする]** を選択します。 

1. **Windows エージェントのダウンロード (64 ビット)** のリンクを選択します。

1. ダウンロードした.exeファイルを実行し、確認と表示される可能性のあるユーザーアカウント制御プロンプトを実行します。

1. ウェルカム ダイアログで **[次へ]** を選択します。

1. 後ほど使用できるよう以下の情報に留意してください。

1. [エージェントのセットアップ オプション] プロンプトで、**[Azure ログ分析 (OMS) にエージェントを接続する]** オプションを選択し、**[次へ]** を選択します。

1. ブラウザで、エージェントの管理ページから**ワークスペースID**をコピーし、ダイアログのワークスペースIDに貼り付けます。 

1. ブラウザで、エージェントの管理ページから主キーをコピーし、ダイアログの**主キー**に貼り付けます。 

1. **[次へ]** を選択します。

1. [Microsoft Update] ページで、**[次へ]** を選択します。

2. その後、 **[インストール]** を選択します。

### <a name="task-4-install-and-collect-sysmon-logs"></a>タスク 4:Sysmonログをインストールして収集します。

このタスクでは、Sysmonログをインストールして収集します。

You should still be connected to the WIN2 virtual machine.  The following instructions will install Sysmon with the default configuration.  You should research community based configurations for Sysmon to be used on production machines.

1. ブラウザーで、https://docs.microsoft.com/sysinternals/downloads/sysmon に移動します。

1. **Sysmonのダウンロード**を選択して、ページからSysmonをダウンロードします。

1. ダウンロードしたファイルを開き、ファイルを新しいディレクトリc：\ sysmonに抽出します。

1. **テナント サフィックス ID。**

1. *cd \sysmon* と入力します

1. *notepad sysmon.xml* と入力して、新しいファイルを作成します。

1. ブラウザーでタブを開き、https://github.com/SwiftOnSecurity/sysmon-config/blob/master/sysmonconfig-export.xml に移動します。

1. そのファイルの内容を Github から先ほど作成した sysmon.xml メモ帳ファイルにコピーしてファイルを保存します。

1. コマンド プロンプトで、「sysmon.exe -accepteula -i sysmon.xml」と入力して Enter キーを押します

1. ブラウザーで Azure portal (https://portal.azure.com ) に移動します。 

1. Azure portal の検索バーに「*Sentinel*」と入力してから、**[Microsoft Sentinel]** を選択します。

1. Microsoft Sentinel で、[構成] 領域から **[設定]** を選択し、 **[ワークスペース設定]** タブを選択します。

1. Microsoft Sentinel ワークスペースが選択されていることを確認してください。

1. [設定] で、**[エージェント構成]** を選択します。

1. **[Windows イベント ログ]** タブを選択します。

1. **[Windows イベント ログの追加]** ボタンを選択します。

1. "ログ名" フィールドに「**Microsoft-Windows-Sysmon/Operational**」と入力します。

1. **[適用]** を選択します。

## <a name="conduct-attacks"></a>攻撃を実施する

### <a name="task-1-attack-windows-configured-with-defender-for-endpoint"></a>タスク 1:Defender for Endpoint によって構成した Windows を攻撃します。

このタスクでは、Microsoft Defender for Endpoint が構成されているホストに対して攻撃を実行します。

1. 管理者として WIN1 仮想マシンにログインします。パスワードは**Pa55w.rd**。  

1. この ID は、ラボ全体で Microsoft 365 にサインインする際に使用する onmicrosoft.com アカウント用です。

1. コマンドプロンプトで、各行の後に Enter キーを押して、各行にコマンドを入力します。
```
cd \
mkdir temp
cd temp
```
1. 攻撃 1 -次のコマンドをコピーして実行します。

```
REG ADD "HKCU\SOFTWARE\Microsoft\Windows\CurrentVersion\Run" /V "SOC Test" /t REG_SZ /F /D "C:\temp\startup.bat"
```

1. 攻撃 2 - 次のコマンドをコピーして実行します。

```
notepad c2.ps1
```
**[はい]** を選択して新しいファイルを作成し、以下の PowerShell スクリプトを c2.ps1 にコピーして **[保存]** を選択します。

形式は **{username}@M365xZZZZZZ.onmicrosoft.com** です。ZZZZZZ はラボ ホスティング プロバイダーの提供した一意のテナント サフィックス ID です。

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
後で使用できるよう、この ZZZZZZ を記録しておきます。

### <a name="task-2-attack-windows-configured-with-sysmon"></a>タスク 2:Sysmon で構成された攻撃ウィンドウ

このタスクでは、セキュリティ イベント コネクタが構成され、Sysmon が構成されているホストに対して攻撃を実行します。

1. 管理者として、次のパスワードを使用して WIN2 仮想マシンにログインします:**Pa55w.rd**。  

1. ラボの手順で Microsoft 365 ポータルにサインインするよう指示されたら、ここで取得した ZZZZZZ の値を入力してください。

1. コマンドプロンプトで、各行の後に Enter キーを押して、各行にコマンドを入力します。
```
cd \
mkdir temp
cd \temp
```

1. 攻撃 1 -次のコマンドをコピーして実行します。

```
REG ADD "HKCU\SOFTWARE\Microsoft\Windows\CurrentVersion\Run" /V "SOC Test" /t REG_SZ /F /D "C:\temp\startup.bat"
```

1. 攻撃 2 - このコマンドをコピーして実行し、各行の後に Enter キーを押して各行にコマンドを入力します。

```
net user theusernametoadd /add
net user theusernametoadd ThePassword1!
net localgroup administrators theusernametoadd /add
```