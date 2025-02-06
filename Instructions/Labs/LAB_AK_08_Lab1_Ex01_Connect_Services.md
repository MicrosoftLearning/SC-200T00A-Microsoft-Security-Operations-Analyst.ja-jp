---
lab:
  title: 演習 1 - データ コネクタを使用して Microsoft Sentinel にデータを接続する
  module: Learning Path 8 - Connect logs to Microsoft Sentinel
---

# ラーニング パス 8: ラボ 1: 演習 1: データ コネクタを使用して Microsoft Sentinel にデータを接続する

## ラボのシナリオ

![ラボの概要。](../Media/SC-200-Lab_Diagrams_Mod6_L1_Ex1.png)

あなたは、Microsoft Sentinel を実装した会社で働いているセキュリティ運用アナリストです。 組織内の多くのデータ ソースからのログ データを接続する方法について学習する必要があります。 組織には、Microsoft 365、Microsoft 365 Defender、Azure リソース、Azure 以外の仮想マシンなどからのデータがあります。最初に、Microsoft のソースに接続します。

>**重要:** ラーニング パス #8 のラボ演習は、*スタンドアロン*環境にあります。 ラボを完了せずに終了する場合は、構成を再実行する必要があります。

### このラボの推定所要時間: 20 分

### タスク 1:Microsoft Sentinel ワークスペースにアクセスする

このタスクでは、Microsoft Sentinel ワークスペースにアクセスします。

>**注:** Microsoft Sentinel は、**defenderWorkspace** という名前で Azure サブスクリプションに事前にデプロイされており、必要な*コンテンツ ハブ* ソリューションがインストールされています。

1. 管理者として **WIN1** 仮想マシンにログインします。パスワードは **Pa55w.rd** です。  

1. Microsoft Edge ブラウザーを開きます。

1. Edge ブラウザーで、Azure portal (<https://portal.azure.com> ) に移動します。

1. **サインイン** ダイアログ ボックスで、ラボ ホスティング プロバイダーから提供された**テナントの電子メール** アカウントをコピーして貼り付け、**[次へ]** を選択します。

1. **[パスワードの入力]** ダイアログ ボックスで、ラボ ホスティング プロバイダーから提供された**テナントパスワード**をコピーして貼り付け、**[サインイン]** を選択します。

1. Azure portal の検索バーに「*Sentinel*」と入力してから、**[Microsoft Sentinel]** を選択します。

1. Microsoft Sentinel **defenderWorkspace** を選択します。

1. 次のタスクに進みます。

### タスク 2: Microsoft Defender for Cloud データ コネクタを接続する

このタスクでは、Microsoft Defender for Cloud データ コネクタを接続します。

   <!--- >>**Important:** To *Enable* Bi-directional sync, please rerun  **[Lab 05 Exercise 1](https://microsoftlearning.github.io/SC-200T00A-Microsoft-Security-Operations-Analyst/Instructions/Labs/LAB_AK_05_Lab1_Ex01_Enable_MDC.html)**, Task 2, and select **Setup** from the *Microsoft Defender for Cloud* navigation menu to verify all eligible Azure subscriptions are onboarded. --->

1. Microsoft Sentinel ナビゲーション メニューで、**[コンテンツ管理]** セクションまで下にスクロールし、**[コンテンツ ハブ]** を選択します。

1. *[コンテンツ ハブ]* で、「**Microsoft Defender for Cloud**」ソリューションを検索し、一覧から選択します。

1. *Microsoft Defender for Cloud* ソリューションの詳細ページで、**[管理]** を選択します

    >**注:** *Microsoft Defender for Cloud* ソリューションでは、*サブスクリプション ベースの Microsoft Defender for Cloud (レガシ)* データ コネクタ、*テナント ベースの Microsoft Defender for Cloud (プレビュー)* データ コネクタ、および分析ルールがインストールされます。 テナントに複数のサブスクリプションがある場合、*テナント ベースの Microsoft Defender for Cloud (プレビュー)* データ コネクタが使用されます。

1. *サブスクリプション ベースの Microsoft Defender for Cloud (レガシ)* データ コネクタ チェックボックスを選択し、**[コネクタ ページを開く]** を選択します。

1. *[構成]* セクションで、*MOC Subscription-XXXXXXXXXXX* のチェックボックスを**オン**にし、**[接続]** リンクを選択するか、**[状態]** オプションを右にスライドします。

1. 双方向の同期を有効にするには、**[すべてのサブスクリプションに対して Microsoft Defender を有効にする]** リンクを選択します。

1. *[Microsoft Defender for Cloud] - [はじめに]* ページで、*MOC Subscription-XXXXXXXXXXX* のチェック ボックスがオンで、*[Microsoft Defender プラン]* が *[オン - 部分的 (試用期間は残り 30 日です)]* になっている必要があります。

1. 右上隅の **[X] (閉じる)** ボタンを選択して、*[はじめに]* ページを閉じます。 *Microsoft Defender for Cloud* の構成ページに戻るはずです。

1. *MOC Subscription-XXXXXXXXXXX* の *[状態]* が **[接続済み]** になり、*[双方向の同期]* が *[有効]* になっているはずです。

    <!--- 1. Scroll down and under the *Create incidents - Recommended!* area, verify that *Create incidents automatically from all alerts generated in this connected service* is **Enabled**. --->

### タスク 3: Azure Activity データ コネクタを接続する

このタスクでは、*Azure Activity* データ コネクタを接続します。

1. Microsoft Sentinel ナビゲーション メニューで、*[コンテンツ管理]* セクションまで下にスクロールし、**[コンテンツ ハブ]** を選択します。

1. *[コンテンツ ハブ]* で、「**Azure Activity**」ソリューションを検索し、一覧から選択します。

1. *[Azure アクティビティ]* ソリューションの詳細ページで、**[管理]** を選択します。

    >**注:** *Azure Activity* ソリューションでは、*Azure Activity* データ コネクタ、12 個の分析ルール、14 個のハンティング クエリ、1 つのブックがインストールされます。

1. *Azure Activity* データ コネクタを選択し、 **[コネクタ ページを開く]** を選択します。

1. *[構成]* 領域の *[手順]* タブで、"2. 診断設定の新しい..." まで下にスクロールし、 **[[Azure Policy の割り当て] ウィザードの起動>]** を選択します。

1. **[基本]** タブで、**[スコープ]** の下にある省略記号ボタン ([...]) を選択し、ドロップダウン リストから *MOC Subscription-XXXXXXXXXXX* サブスクリプションを選択して、**[選択]** をクリックします。

1. **[パラメーター]** タブを選択し、 **[プライマリ Log Analytics ワークスペース]** ドロップダウン リストから自分の *uniquenameDefender* ワークスペースを選択します。 このアクションにより、Log Analytics ワークスペースに情報を送信するサブスクリプション構成が適用されます。

1. **[修復]** タブを選択し、 **[修復タスクの作成]** チェック ボックスをオンにします。 このアクションにより、既存の Azure リソースにポリシーが適用されます。

1. **[確認と作成]** ボタンを選択して構成を確認します。

1. **[作成]** を選択して完了します。

## 演習 2 に進みます。
