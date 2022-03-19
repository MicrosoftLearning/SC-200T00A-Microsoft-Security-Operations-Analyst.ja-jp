---
lab:
  title: 演習 1 - データ コネクタを使用して Microsoft Sentinel にデータを接続する
  module: Module 6 - Connect logs to Microsoft Sentinel
ms.openlocfilehash: 1f946958246be76294aa75463b5f9877905d6090
ms.sourcegitcommit: 175df7de88c9a609f8caf39840664bf992c5b6dc
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/05/2022
ms.locfileid: "138025445"
---
# <a name="module-6---lab-1---exercise-1---connect-data-to-microsoft-sentinel-using-data-connectors"></a>モジュール 6 - ラボ 1 - 演習 1 - データ コネクタを使用して Microsoft Sentinel にデータを接続する

## <a name="lab-scenario"></a>ラボのシナリオ

あなたは、Microsoft Sentinel を実装した会社で働いているセキュリティ運用アナリストです。 組織内の多くのデータ ソースからのログ データを接続する方法について学習する必要があります。 組織には、Microsoft 365、Microsoft 365 Defender、Azure リソース、Azure 以外の仮想マシンなどからのデータがあります。最初に、Microsoft のソースに接続します。


### <a name="task-1-access-the-microsoft-sentinel-workspace"></a>タスク 1:Microsoft Sentinel ワークスペースにアクセスする

このタスクでは、Microsoft Sentinel ワークスペースにアクセスします。

1. 管理者として WIN1 仮想マシンにログインします。パスワードは **Pa55w.rd**。  

1. Microsoft Edge ブラウザーを開きます。

1. Edge ブラウザーで、Azure portal (https://portal.azure.com ) に移動します。

1. **サインイン** ダイアログ ボックスで、ラボ ホスティング プロバイダーから提供された **テナントの電子メール** アカウントをコピーして貼り付け、「**次へ**」を選択します。

1. **パスワードの入力** ダイアログ ボックスで、ラボ ホスティング プロバイダーから提供された **テナントパスワード** をコピーして貼り付け、「**サインイン**」を選択します。

1. Azure portal の検索バーに「*Sentinel*」と入力してから、 **[Microsoft Sentinel]** を選択します。

1. 前のラボで作成した Microsoft Sentinel ワークスペースを選択します。


### <a name="task-2-connect-the-azure-active-directory-connector"></a>タスク 2:Azure Active Directory コネクタを接続する

このタスクでは、Azure Active Directory コネクタを Microsoft Sentinel に接続します。

1. 構成領域で、[**データ コネクタ]** を選択します。 [データ コネクタ] ページで、一覧から **Azure Active Directory** コネクタを探して選択します。

1. コネクタ情報ブレードで「**コネクタページを開く**」を選択します。

1. 構成領域から「**サインインログ**」および「**監査ログ**」オプションを選択し、「**変更の適用**」を選択します。


### <a name="task-3-connect-the-azure-active-directory-identity-protection-connector"></a>タスク 3:Azure Active Directory Identity Protection コネクタを接続する

このタスクでは、Azure Active Directory Identity Protection コネクタを Microsoft Sentinel に接続します。

1. [データ コネクタ] タブで、一覧から **Azure Active Directory Identity Protection** コネクタを探して選択します。

1. コネクタ情報ブレードで「**コネクタページを開く**」を選択します。

1. 構成 領域から **接続** ボタンを選択します。


### <a name="task-4-connect-the-microsoft-defender-for-cloud-connector"></a>タスク 4:Microsoft Defender for Cloud に接続する

このタスクでは、Microsoft Defender for Cloud コネクタを接続します。

1. [データ コネクタ] タブで、一覧から **Microsoft Defender for Cloud** コネクタを探して選択します。

1. コネクタ情報ブレードで「**コネクタページを開く**」を選択します。

1. [構成] 領域の [サブスクリプション] で、[Azure Pass - スポンサーシップ] サブスクリプションのチェック ボックスをオンにして、 **[接続]** を選択します。

1. 「接続」メッセージを確認し、 **[OK]** を選択して続行します。 [状態] が *[接続済み]* になり、[双方向の同期] が *[有効]* になるはずです。

1. 下にスクロールし、[Create incidents - Recommended!]\(インシデントの作成 - 推奨\) 領域で、 **[有効]** を選択します。 このオプションを選択すると、このサービスに対して分析ルールが自動的に作成されます。 ここで有効にしなくても、後で *[分析]* ブレードを使って、手動で追加したり、構成を変更したりできます。


### <a name="task-5-connect-the-microsoft-365-defender-connector"></a>タスク 5:Microsoft 365 Defender コネクタを接続する

このタスクでは、Microsoft 365 Directory コネクタを接続します。

1. [データ コネクタ] タブで、一覧から **Microsoft 365 Defender (プレビュー)** コネクタを探して選択します。

1. コネクタ情報ブレードで「**コネクタページを開く**」を選択します。

1. [構成] 領域で **[Connect Incident and Alerts]\(インシデントとアラートの接続\)** を選択します。 

1. [イベントの接続] で、 **[名前]** チェック ボックスをオンにして、"Microsoft Defender for Endpoint" のすべてのチェック ボックスをオンにします。

1. "Microsoft Defender for Office 365" について同じことを繰り返します。

1. ページの下部までスクロールし、 **[変更の適用]** を選択します。


### <a name="task-6-connect-the-azure-activity-connector"></a>タスク 6:Azure Activity コネクタを接続する

このタスクでは、Azure Activity コネクタを接続します。

1. [データ コネクタ] タブで、一覧から **Azure Activity** コネクタを探して選択します。

1. コネクタ情報ブレードで「**コネクタページを開く**」を選択します。

1. 構成 領域で、下にスクロールして、2. 診断設定の新しい... で **Azure Policy の割り当て ウィザードの起動>** を選択します。

1. **[基本]** タブで、 **[スコープ]** の下にある省略記号ボタン [...] を選択し、ドロップダウン リストから [Azure Pass - スポンサーシップ] サブスクリプションを選択して、 **[選択]** をクリックします。

1. **[パラメーター]** タブを選択し、 **[プライマリ Log Analytics ワークスペース]** ドロップダウン リストから自分の *uniquenameDefender* ワークスペースを選択します。

1. **[修復]** タブを選択し、 **[修復タスクの作成]** チェック ボックスをオンにします。

1. **[確認と作成]** ボタンを選択して構成を確認します。

1. **[作成]** を選択して完了します。

## <a name="proceed-to-exercise-2"></a>演習 2 に進みます。
