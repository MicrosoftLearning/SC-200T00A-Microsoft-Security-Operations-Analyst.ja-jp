---
ms.openlocfilehash: fb8d611ee9301793d2f051799f9128892f868e25
ms.sourcegitcommit: a90325f86a3497319b3dc15ccf49e0396c4bf749
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/07/2022
ms.locfileid: "141493891"
---

# <a name="microsoft-security-operations-analyst"></a>Microsoft Security Operations Analyst
講師用準備ガイド

## <a name="purpose"></a>目的 

このドキュメントは、"セキュリティを最新化し、脅威から身を守る" ための Microsoft セキュリティ仮想トレーニングデーを教える準備をしているプレゼンターを対象としています。 この資料は SC-200:Microsoft Security Operations Analyst 認定コースのサブセットです。

## <a name="demo-prerequisites"></a>デモの前提条件

このコースのラボでは、Microsoft 365 E5ライセンスのテナントと、Azureサブスクリプションの両方が必要です。
* ご自身のために Microsoft Learning Azure Pass を要求できます
* デモを実行する少なくとも 2 週間前に、これらのパスを要求してください。 パスを受け取った後、そのパスを有効にする必要があります。 
* Azure Pass は、一般に公開されている Microsoft Azure 試用版サブスクリプションと同じ方法で、効果的に機能します。 これは、パスで実行できる操作には制限があることを意味します。
* ラボの手順は、[SC-200 Microsoft Learning Github](https://github.com/MicrosoftLearning/SC-200T00A-Microsoft-Security-Operations-Analyst/tree/master/Instructions/VTD_Demos/) リポジトリにあります。
* デモに使用するコンピューターに新しい Microsoft Edge ブラウザーがインストールされていることを確認してください。

## <a name="activate-azure-pass"></a>Activate Azure Pass

## <a name="deploy-defender-for-endpoint"></a>Defender for Endpoint のデプロイ

### <a name="obtain-your-microsoft-365-credentials"></a>Microsoft 365 資格情報の取得

ラボを起動すると、無料のトライアル テナントを利用して Microsoft Virtual Lab 環境にアクセスできるようになります。 このテナントには自動的に一意のユーザー名とパスワードが割り当てられます。 Microsoft Virtual Lab 環境で Azure と Microsoft 365 にサインインするには、このユーザー名とパスワードを取得する必要があります。 

このコースは、学習パートナーが複数の認証済みラボ ホスティング プロバイダーのいずれかを使用して実施することもあり、お使いになっているテナントに関連のあるテナント ID を取得する実際の手順はラボ ホスティング プロバイダーに応じて異なります。 このため、コース内での当該情報の取得方法については、講師が必要な指示を行います。 後ほど使用できるよう以下の情報に留意してください。

    - **テナント サフィックス ID。** この ID は、ラボ全体で Microsoft 365 にサインインする際に使用する onmicrosoft.com アカウント用です。 形式は **{username}@M365xZZZZZZ.onmicrosoft.com** です。ZZZZZZ はラボ ホスティング プロバイダーの提供した一意のテナント サフィックス ID です。 後で使用できるよう、この ZZZZZZ を記録しておきます。 ラボの手順で Microsoft 365 ポータルにサインインするよう指示されたら、ここで取得した ZZZZZZ の値を入力してください。
    - **テナント パスワード。** これは、ラボ ホスティング プロバイダーの提供する管理者アカウント向けのパスワードです。
    

### <a name="initialize-microsoft-defender-for-endpoint"></a>Microsoft Defender for Endpoint の初期化

このタスクでは、Microsoft Defender for Endpoint ポータルの初期化を行います。


1.  管理者として WIN1 仮想マシンにログインします。パスワードは **Pa55w.rd**。  

2.  Microsoft Edge ブラウザーを開いて、「edge ブラウザー更新」を検索し、新しい Microsoft Edge ブラウザーをダウンロードしてインストールします。 この手順は、ホスティングされている仮想マシンで確実に Microsoft Edge の最新版を実行する上で重要です。 新しいMicrosoft Edge ブラウザーを起動します。

3.  Edge ブラウザーで、Microsoft Defender セキュリティ センター (https://securitycenter.microsoft.com) に移動します。

4. **[サインイン]** ダイアログ ボックスで、ラボ ホスティング プロバイダーから提供された管理者ユーザー名のテナント電子メール アカウントをコピーして貼り付け、**[次へ]** を選択します。

5. **パスワードの入力** ダイアログ ボックスで、ラボ ホスティング プロバイダーの提供した管理者のテナント パスワードをコピーして貼り付け、**サインイン** します。

**注**: "このセクションにアクセスできません" というメッセージが表示されたら、5 分待ってから再びお試しください。  アクセス ルールでテナントを広める必要があるかもしれません。  

6. **Microsoft セキュリティ センター** セットアップのステップ 2 で **[次へ]** を選択します。

7. ステップ 3「**基本設定のセットアップ**」では、このトレーニング テナントの管理に適したデータ ストレージの場所を選択します。  コースの講師と確認した方がよいかもしれません。

8. プレビュー機能が **オン** になっていることを確認してください。

9. **[次へ]** を選択します。  

10. **[クラウド インスタンスの作成]** で [続行] を選択します

11. **Microsoft Defender for Endpoint アカウントの作成中** の進行状況バーが完了すると、 ステップ 4 のオプションが表示されます。  **Microsoft Defender for Endpoint を使用して開始** を選択します。

12. [セットアップ未完了] ダイアログ ボックスで **[このまま続行]** を選択します。

**注**:セットアップは **完了** します。  次のタスクではデバイスのオンボードを行います。  

### <a name="onboard-a-device"></a>デバイスのオンボード

このタスクでは、デバイスを Microsoft Defender for Endpoint にオンボードします。

1. Microsoft Defender セキュリティ センター (https://securitycenter.microsoft.com) に移動します。現在ポータルを使用していない場合は、**テナントの電子メール** の資格情報を使用してログインします。

2. 左側のメニュー バーで **[設定]** を選択します。

3. デバイス管理セクションで **[オンボーディング]** を選択します。

4. デバイスのオンボード領域で **[パッケージのダウンロード]** ボタンを選択します。

5. ダウンロードされた zip ファイルをローカル フォルダーに抽出します (［ドキュメント］ フォルダーなど)。

6. 抽出されたファイル (WindowsDefenderATPLocalOnboardingScript.cmd) を右クリックし、**[管理者として実行]** を選択します。  Windows SmartScreen が表示されたら、[実行する] を選択します。

**注** 既定で、ファイルは [c:\users\admin\downloads] ディレクトリにあります。
    
7. スクリプトの質問に対して、**[Y]** と回答します。 完了したら、コマンド画面に "マシンが正常にオンボードされました..." のような内容のメッセージが表示されます。 

8. ポータルの [オンボーディング] ページで、検出テスト スクリプトをコピーして、オープン コマンド ウィンドウで実行します。  新しい **[管理者: コマンド プロンプト]** ウィンドウを開く必要があるかもしれません。その場合は、Windows 検索バーで「*CMD*」と入力し、**[管理者として実行]** を選択します。

9. Microsoft Defender セキュリティ センターのポータル メニューで、**[デバイス インベントリ]** を選択します。 お使いになっているデバイスがリストに表示されます。

**注** デバイスがポータルに表示されるまでに最高 5 分かかることがあります。


### <a name="configure-role"></a>ロールの構成

このタスクでは、デバイス グループで使用するロールを設定します。

1. Microsoft Defender セキュリティ センターのポータルで、左側のメニュー バーから **[設定]** を選択します。 

2. アクセス許可領域で、**[ロール]** を選択します。

3. **[ロールをオンにする]** ボタンを選択します。

4. **[項目の追加]** を選択します。

5. ロールの追加 ダイアログで以下を入力します。ロール名:Tier  [Live Response capabilities]\(ライブ応答機能\): チェックボックスをオン  [詳細]: オン

6. **[次へ]** を選択します。

7. [割り当てられたユーザー グループ] タブで **[sg-IT]** を選択し、**[選択したグループを追加する]** を選択します。

8. **[保存]** を選択します。


### <a name="configure-device-groups"></a>デバイス グループの構成

このタスクでは、アクセス コントロールと自動化の設定が可能なデバイス グループを構成します。

1. 左側のメニュー バーで **[設定]** を選択します。 

2. アクセス許可領域で **[デバイス グループ]** を選択します。

3. **[デバイス グループの追加]** を選択します。

4. 全般 タブに次の情報を入力します。

- デバイス グループ名:定期
- 自動化レベル:完全 - 脅威を自動的に修復する
- メンバー:名前は TESTLAB と同じになります

5. **[次へ]** を選択します。

6. [ユーザー アクセス] タブで、**[sg-IT]** を選択し、**[選択したグループを追加する]** を選択します

7. **[完了]** を選択します。

8. これでデバイス グループの構成が変わりました。 変更を適用して一致を確認し、グループ化を再計算します。


## <a name="deploy-sample-alerts-for-demo-in-module-2"></a>モジュール　2　でデモのサンプル　アラートをデプロイする

このタスクでは、サンプルのセキュリティアラートを読み込み、アラートの詳細を確認します。

2. Edge ブラウザーで Azure portal (https://portal.azure.com ) を開きます。

3. **[サインイン]** ダイアログ ボックスで、ラボ ホスティング プロバイダーから提供された **テナントの電子メール** アカウントをコピーして貼り付け、 **[次へ]** を選択します。

4. **[パスワードの入力]** ダイアログ ボックスで、ラボ ホスティング プロバイダーから提供された **テナントのパスワード** をコピーして貼り付け、 **[サインイン]** を選択します。

5. Azure portal の検索バーに「*セキュリティ*」と入力し、**[セキュリティ センター]** を選択します。

1. セキュリティ　センターのアップグレードを求めるメッセージが表示されたら、下部にある　 **[スキップ]** 　をクリックします。

6. ポータルメニューで **[セキュリティアラート]** を選択します。

7. コマンド バーから **[サンプルアラート]** を選択します。

8. サンプルアラートの作成（プレビュー）ペインで、サブスクリプションが選択されていることを確認します。  すべてのサンプルアラートが選択されていることを確認し、**[サンプルアラートの作成]** を選択します。  

**注**: これは完了するまでに数分かかる場合があります。

## <a name="deploy-azure-sentinel-workspace-for-demo-in-module-4"></a>モジュール　4　でデモ用の Azure Sentinel ワークスペースをデプロイする

このタスクでは、Azure Sentinel ワークスペースを作成します。

3.  Edge ブラウザーで、Azure portal (https://portal.azure.com ) に移動します。

4. **[サインイン]** ダイアログ ボックスで、ラボ ホスティング プロバイダーから提供された **テナントの電子メール** アカウントをコピーして貼り付け、 **[次へ]** を選択します。

5. **[パスワードの入力]** ダイアログ ボックスで、ラボ ホスティング プロバイダーから提供された **テナントのパスワード** をコピーして貼り付け、 **[サインイン]** を選択します。

6. Azure portal の検索バーに「*Sentinel*」と入力し、**[Azure Sentinel]** を選択します。

7. **[+ 作成]** を選択します。

8. **[+ 新しいワークスペースの作成]** を選択します。

**注** まず、新しい Log Analytics ワークスペースを作成します。

9. 適切なサブスクリプションを選択します。

10. リソースグループの **新規作成** リンクを選択し、選択した新しいリソースグループ名を入力します。

11. 名前 フィールドの インスタンスの詳細 で、LogAnalyticsワークスペースに選択する名前を入力します。

**注:**  この名前は、AzureSentinelワークスペース名にもなります。

12. 適切な領域を選択します。  適切な領域が既定になる場合や、インストラクターがどの領域を選択するかについて具体的なアドバイスをする場合があります。  

13. **[確認および作成]** を選択します。

14. **［作成］** を選択します 新しいLogAnalyticsワークスペースがAzureSentinelをワークスペースに追加ページのリストに表示されるのを待ちます。  これには時間がかかることがあります。

16. 新しく作成したワークスペースが表示されたら、それを選択し、**[追加]** を選択します。

## <a name="create-data-connectors-for-azure-sentinel"></a>Azure Sentinel のデータ コネクタを作成する

### <a name="task-1-access-the-azure-sentinel-workspace"></a>タスク 1:AzureSentinel ワークスペースにアクセスします。

このタスクでは、Azure Sentinel ワークスペースにアクセスします。

1. 管理者として WIN1 仮想マシンにログインします。パスワードは **Pa55w.rd**。  

2. ブラウザを開き、新しいMicrosoft Edgeブラウザーを検索、ダウンロード、およびインストールします。 新しいMicrosoft Edge ブラウザーを起動します。

3. Edge ブラウザーで、Azure portal (https://portal.azure.com ) に移動します。

4. **[サインイン]** ダイアログ ボックスで、ラボ ホスティング プロバイダーから提供された **テナントの電子メール** アカウントをコピーして貼り付け、 **[次へ]** を選択します。

5. **[パスワードの入力]** ダイアログ ボックスで、ラボ ホスティング プロバイダーから提供された **テナントのパスワード** をコピーして貼り付け、 **[サインイン]** を選択します。

6. Azure portal の検索バーに「*Sentinel*」と入力し、**[Azure Sentinel]** を選択します。

7. 前のラボで作成した AzureSentinel ワークスペースを選択します。

### <a name="task-2-connect-the-azure-active-directory-connector"></a>タスク 2:Azure Active Directory コネクタを接続する

このタスクでは、Azure アクティビティ データ コネクタを接続します。

1. 構成領域で、**[データ コネクタ]** を選択します。  データ コネクタ ページで、リストから **Azure Active Directory** タイルを選択します。

2. [コネクタ情報] ブレードで **[コネクタ ページを開く]** を選択します。

3. 構成領域から **[サインイン ログ]** と **[監査ログ]** オプションを選択し、**[変更の適用]** を選択します。

### <a name="task-3-connect-the-azure-active-directory-identity-protection-connector"></a>タスク 3:Azure Active Directory Identity Protection コネクタを接続する

このタスクでは、Azure Active Directory Identity Protection コネクタを接続します。

1. [データ コネクタ] タブで、リストから **[Azure Active Directory Identity Protection]** コネクタを選択します。

2. [コネクタ情報] ブレードで **[コネクタ ページを開く]** を選択します。

3. **[接続]** を選択します。

### <a name="task-4-connect-the-azure-defender-connector"></a>タスク 4:Azure Directory コネクタを接続する

このタスクでは、Azure Directory コネクタを接続します。

1. [データ コネクタ] タブで、一覧から **[Azure Defender]** コネクタを選択します。

2. [コネクタ情報] ブレードで **[コネクタ ページを開く]** を選択します。

3. 接続オプションを確認します。 接続しない。 これは情報提供のみを目的としています。

### <a name="task-5-connect-the-microsoft-cloud-app-security-connector"></a>タスク 5:Microsoft Cloud AppSecurityコネクタを接続する。

このタスクでは、Microsoft Cloud App Security コネクタを接続します。

1. [データ コネクタ] タブで、一覧から **[Microsoft Cloud App Security]** コネクタを選択します。

2. [コネクタ情報] ブレードで **[コネクタ ページを開く]** を選択します。

3. **[アラート]** を選択し、**[変更の適用]** を選択します。

### <a name="task-6-connect-the-microsoft-defender-for-office-365-connector"></a>タスク 6:Microsoft Defender for Office 365 に接続する

このタスクでは、Microsoft Defender for Office 365 コネクタを接続します。

1. [データ コネクタ] タブで、一覧から **[Microsoft Defender for Office 365]** コネクタを選択します。

2. [コネクタ情報] ブレードで **[コネクタ ページを開く]** を選択します。

3. **[接続]** を選択します。

### <a name="task-7-connect-the-microsoft-defender-for-identity-connector"></a>タスク 7:Microsoft Defender for forIdentity コネクタに接続する

このタスクでは、Microsoft Defender for Identity コネクタを接続します。

1. [データ コネクタ] タブで、一覧から **[Microsoft Defender for Identity]** コネクタを選択します。

2. [コネクタ情報] ブレードで **[コネクタ ページを開く]** を選択します。

3. 接続オプションを確認します。 接続しない。 これは情報提供のみを目的としています。

### <a name="task-8-connect-the-microsoft-defender-for-endpoint-connector"></a>タスク 8:Microsoft Defender for Endpointコネクタに接続する

このタスクでは、Microsoft Defender for Endpoint コネクタを接続します。

1. [データ コネクタ] タブで、一覧から **[Microsoft Defender for Endpoint]** コネクタを選択します。

2. [コネクタ情報] ブレードで [コネクタ ページを開く] を選択します。

3. **[接続]** を選択します。

### <a name="task-9-connect-the-microsoft-365-defender-connector"></a>タスク 9:Microsoft 365 Defender コネクタを接続する

このタスクでは、Microsoft 365 Directory コネクタを接続します。

1. [データ コネクタ] タブで、一覧から **[Microsoft 365 Defender]** コネクタを選択します。

2. [コネクタ情報] ブレードで **[コネクタ ページを開く]** を選択します。

3. Microsoft Defender for Endpointのすべてのチェックボックスを選択します。

4. **[変更の適用]** を選択します。

### <a name="task-3-connect-a-non-azure-windows-machine"></a>タスク 3:非 Azure Windows マシンを接続する。

このタスクでは、非 Azure Windows 仮想マシンを Azure Sentinel に接続します。

1. 管理者として、次のパスワードを使用して WIN2 仮想マシンにログインします:**Pa55w.rd**。  

2. ブラウザを開き、新しいMicrosoft Edgeブラウザーを検索、ダウンロード、およびインストールします。 新しいMicrosoft Edge ブラウザーを起動します。

3. ブラウザーを開き、ご自身の資格情報を使用して Azure Portal (https://portal.azure.com ) にログインします。

4. Azure portal の検索バーに「*Sentinel*」と入力し、**[Azure Sentinel]** を選択します。

5. Azure Sentinel ワークスペースを選択します。

6. [データ コネクタ] タブで、リストから **[セキュリティ イベント]** コネクタを選択します。

7. [コネクタ情報] ブレードで **[コネクタ ページを開く]** を選択します。

8. ストリーミングするイベントの選択領域で、**[すべてのイベント]** を選択し、**[変更の適用]** を選択します。

9. **[Azure 以外の Windows 仮想マシンにエージェントをインストールする]** を選択します。

**注:**  Windows仮想マシンへのエージェントのインストールと非Azure　Windowsマシンへのエージェントのインストールの手順が逆になる場合があります。 リンクは、テキストが逆になっている場合でも、適切な場所に移動します。

10. **[Azure 以外の Windows 仮想マシンのエージェントをダウンロードしてインストールする]** を選択します。 

11. **Windows エージェントのダウンロード (64 ビット)** のリンクを選択します。

12. ダウンロードした.exeファイルを実行し、確認と表示される可能性のあるユーザーアカウント制御プロンプトを実行します。

13. ウェルカム ダイアログで **[次へ]** を選択します。

14. [Microsoft ソフトウェアライセンス条項] ページで **[同意する]** を選択します。  宛先プロンプトで、**[次へ]** を選択します。

15. [エージェントのセットアップ オプション] プロンプトで、**[Azure ログ分析 (OMS) にエージェントを接続する]** オプションを選択し、**[次へ]** を選択します。

16. ブラウザで、エージェントの管理ページから **ワークスペースID** をコピーし、ダイアログのワークスペースIDに貼り付けます。 

17. ブラウザで、エージェントの管理ページから主キーをコピーし、ダイアログの **主キー** に貼り付けます。 

18. **[次へ]** を選択します。

19. [Microsoft Update] ページで、**[次へ]** を選択します。

20. その後、 **[インストール]** を選択します。

### <a name="task-4-install-and-collect-sysmon-logs"></a>タスク 4:Sysmonログをインストールして収集します。

このタスクでは、Sysmonログをインストールして収集します。

引き続きWIN2 仮想マシンに接続する必要があります。  次の手順では、既定構成でSysmonをインストールします。  実稼働マシンで使用するSysmonのコミュニティベースの構成を調査する必要があります

1. ブラウザーで、 https://docs.microsoft.com/sysinternals/downloads/sysmon に移動します。

2. **Sysmonのダウンロード** を選択して、ページからSysmonをダウンロードします。

3. ダウンロードしたファイルを開き、ファイルを新しいディレクトリc：\ sysmonに抽出します。

4. WindowsのWIN2タスクバーの検索ボックスに *コマンド* を入力します。  検索結果には、コマンドプロンプトアプリが表示されます。  コマンドプロンプトアプリを右クリックし、**管理者として実行** を選択します。  表示されるユーザー アカウント制御のプロンプトを確認します。

5. *cd \sysmon* と入力します

6. *notepad sysmon.xml* と入力して、新しいファイルを作成します。

7. ブラウザーでタブを開き、 https://github.com/SwiftOnSecurity/sysmon-config/blob/master/sysmonconfig-export.xml に移動します。

8. そのファイルの内容をGithubから作成したsysmon.xmlメモ帳ファイルにコピーしてファイルを保存します。

9. コマンド プロンプトで、「sysmon.exe -accepteula -i sysmon.xml」と入力して Enter キーを押します。

10. ブラウザーで Azure portal (https://portal.azure.com ) に移動します。 

11. Azure portal の検索バーに「*Sentinel*」と入力し、**[Azure Sentinel]** を選択します。

12. Azure Sentinel で、構成領域から **[設定]** を選択し、**[ワークスペースの設定]** タブを選択します。

13. AzureSentinelワークスペースが選択されていることを確認してください。

14. [設定] で、**[エージェント構成]** を選択します。

15. **[Windows イベント ログ]** タブを選択します。

16. **[Windows イベント ログの追加]** ボタンを選択します。

17. "ログ名" フィールドに「**Microsoft-Windows-Sysmon/Operational**」と入力します。

18. **[適用]** を選択します。

## <a name="conduct-attacks"></a>攻撃を実施する

### <a name="task-1-attack-windows-configured-with-defender-for-endpoint"></a>タスク 1:Defender for Endpoint によって構成した Windows を攻撃します。

このタスクでは、Microsoft Defender for Endpoint が構成されているホストに対して攻撃を実行します。

1. 管理者として WIN1 仮想マシンにログインします。パスワードは **Pa55w.rd**。  

2. タスク バーの検索で、*Command* と入力します。  検索結果にコマンド プロンプトが表示されます。  コマンド プロンプトを右クリックして、 **[管理者として実行]** を選択します。 表示されるユーザー アカウント制御のプロンプトを確認します。

3. コマンドプロンプトで、各行の後に Enter キーを押して、各行にコマンドを入力します。
```
cd \
mkdir temp
cd temp
```
4. 攻撃 1 -次のコマンドをコピーして実行します。

```
REG ADD "HKCU\SOFTWARE\Microsoft\Windows\CurrentVersion\Run" /V "SOC Test" /t REG_SZ /F /D "C:\temp\startup.bat"
```

5. 攻撃 3 -次のコマンドをコピーして実行します。

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

### <a name="task-2-attack-windows-configured-with-sysmon"></a>タスク 2:Sysmon で構成された攻撃ウィンドウ

このタスクでは、セキュリティ イベント コネクタが構成され、Sysmon が構成されているホストに対して攻撃を実行します。

1. 管理者として、次のパスワードを使用して WIN2 仮想マシンにログインします:**Pa55w.rd**。  

2. タスクバーの検索で、*CMD* と入力します。  検索結果にコマンド プロンプトが表示されます。  コマンド プロンプトを右クリックして、 **[管理者として実行]** を選択します。

3. コマンドプロンプトで、各行の後に Enter キーを押して、各行にコマンドを入力します。
```
cd \
mkdir temp
cd \temp
```

4. 攻撃 1 -次のコマンドをコピーして実行します。

```
REG ADD "HKCU\SOFTWARE\Microsoft\Windows\CurrentVersion\Run" /V "SOC Test" /t REG_SZ /F /D "C:\temp\startup.bat"
```

5. 攻撃 2 - このコマンドをコピーして実行し、各行の後に Enter キーを押して各行にコマンドを入力します。

```
net user theusernametoadd /add
net user theusernametoadd ThePassword1!
net localgroup administrators theusernametoadd /add
```