---
lab:
  title: 演習 4 - エンティティの行動分析を調べる
  module: Module 7 - Create detections and perform investigations using Microsoft Sentinel
ms.openlocfilehash: 78664847f5aac7ce5c2ecffbcb0ba8dd1a0e005d
ms.sourcegitcommit: f8918eddeaa7a7a480e92d0e5f2f71143c729d60
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/08/2022
ms.locfileid: "147038041"
---
# <a name="module-7---lab-1---exercise-4---explore-entity-behavior-analytics"></a>モジュール 7 - ラボ 1 - 演習 4 - エンティティの行動分析を調べる

## <a name="lab-scenario"></a>ラボのシナリオ

あなたは、Microsoft Sentinel を実装した会社で働いているセキュリティ運用アナリストです。 あなたはスケジュール済みおよび Microsoft セキュリティ分析ルールを既に作成しています。 


エンティティ行動分析を実行して異常を検出し、エンティティ分析ページが提供されるように、Microsoft Sentinel を構成する必要があります。


### <a name="task-1-enable-entity-behavior"></a>タスク 1:エンティティの行動を有効にする 

このタスクでは、Microsoft Sentinel でエンティティ行動分析を有効にします。

1. 管理者として WIN1 仮想マシンにログインします。パスワードは **Pa55w.rd**。  

1. Edge ブラウザーで、Azure portal (https://portal.azure.com ) に移動します。

1. **[サインイン]** ダイアログ ボックスで、ラボ ホスティング プロバイダーから提供された **テナントの電子メール** アカウントをコピーして貼り付け、 **[次へ]** を選択します。

1. **[パスワードの入力]** ダイアログ ボックスで、ラボ ホスティング プロバイダーから提供された **テナントのパスワード** をコピーして貼り付け、 **[サインイン]** を選択します。

1. Azure portal の検索バーに「*Sentinel*」と入力してから、**[Microsoft Sentinel]** を選択します。

1. 先ほど作成した Microsoft Sentinel ワークスペースを選択します。

1. **[Entity behavior]\(エンティティの行動\)** ページを選択します。
1. *[Entity behavior settings]\(エンティティの行動の設定\)* のポップアップで、 **[Set EUBA]\(EUBA の設定\)** を選択します。
1. 次のページで、 **[Set UEBA]\(UEBA の設定\)** を選択します。
1. *"エンティティの行動の構成ページ"* で、#1 の機能を **[オン]** に切り替えます。 
1. *2.* で、 **[Azure Active Directory]** を選択します。 次に、**[適用]** を選択します。
1. *3.* で、 **[監査ログ]** 、 **[Azure アクティビティ]** 、 **[セキュリティ イベント]** 、 **[Signin Logs]\(サインイン ログ\)** を選択します。 
1. 次に、**[適用]** を選択します。
1. ラボの間、頻繁にこのページに戻り、取り込まれたログ データと作成されたアラートに基づいて設定されたエンティティを確認します。


### <a name="task-2-confirm-and-review-anomalies-rules"></a>タスク 2:異常ルールを確認する

このタスクでは、異常分析ルールが有効になっていることを確認します。

1. **[分析]** ページを選択します。
1. **[Anomalies]\(異常\)** タブを選択します。
1. ルールの状態列が *[有効]* になっていることを確認します。
1. 任意のルールを選択します。 次に、ルール ブレードで **[編集]** を選択します。
1. *[全般]* タブの情報を確認します。 次に、**次へ:構成**
1. *[構成]* タブの情報を確認します。 次に、右上隅にある **[X]** を選択して、分析ルール ウィザードを終了します。


## <a name="proceed-to-exercise-5"></a>演習 5 に進みます
