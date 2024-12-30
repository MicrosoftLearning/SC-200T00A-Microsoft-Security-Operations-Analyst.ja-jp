---
lab:
  title: 演習 1 - Microsoft Defender for Cloud の有効化
  module: Learning Path 5 - Mitigate threats using Microsoft Defender for Cloud
---

# ラーニング パス 5 - ラボ 1 - 演習 1 - Microsoft Defender for Cloud の有効化

## ラボのシナリオ

あなたは、Microsoft Defender for Cloud を使用してクラウド ワークロード保護を実装している企業に勤務するセキュリティ運用アナリストです。 このラボでは、Microsoft Defender for Cloud を有効にします。

>**重要:** ラーニング パス #5 のラボ演習は、*スタンドアロン*環境にあります。 ラボを完了せずに終了する場合は、構成を再実行する必要があります。

### このラボの推定所要時間: 15 分

### タスク 1: Microsoft Defender for Cloud を有効にする

このタスクでは、Microsoft Defender for Cloud を有効にして構成します。

1. 管理者として **WIN1** 仮想マシンにログインします。パスワードは **Pa55w.rd** です。

1. Microsoft Edge ブラウザーで、Azure portal (<https://portal.azure.com> ) に移動します。
  
    >**注:** ラボの *[ユーザー名]* と *[パスワード]* で **[リソース]** タブを選択してください。 このラボの **<LabUser-XXXXXXXX@LODSPRODXXX.onmicrosoft.com>** アカウントを使用します。

1. **サインイン** ダイアログ ボックスで、ラボ ホスティング プロバイダーの提供した管理者ユーザー名のテナント電子メール アカウントをコピーして貼り付け、**[次へ]** を選択します。

1. **パスワードの入力**ダイアログ ボックスで、ラボ ホスティング プロバイダーの提供した管理者のテナント パスワードをコピーして貼り付け、**サインイン**します。

1. Microsoft Azure portal の検索バーに「*Defender*」と入力し、**[Microsoft Defender for Cloud]** を選択します。

1. Microsoft Defender for Cloud の左側のナビゲーション メニューで *[管理]* セクションを開き、**[環境設定]** を選択します。

1. **[すべて展開]** ボタンを選択すると、すべてのサブスクリプションとリソースが表示されます。

1. **MOC Subscription-lodxxxxxxxx** サブスクリプション (または、お使いの言語での同等の名前) を選択します。

1. 現在、Defender for Cloud プランで保護されている Azure リソースを確認します。

    >**重要:** すべての Defender プランが *[オフ]* の場合は、**[すべてのプランを有効にする]** を選択します。 「$200/月の Microsoft Defender for API プラン 1」を選び、**[保存]** を選びます。** ページの上部にある **[保存]** を選び、"(ご利用の) サブスクリプションの Defender プランが正常に保存されました"** 通知が表示されるまで待ちます。

1. [設定] 領域から **[Settings & monitoring] (設定と監視)** タブを選択します ([保存] の横)。

1. 監視拡張機能を確認します。 これには、Virtual Machines、コンテナー、ストレージ アカウントの構成が含まれます。

1. **[続行]** ボタンを選択するか、ページの右上にある [X] を選択して、[設定と監視] ページを閉じます。

1. ページの右上にある [X] を選択することで [設定] ページを閉じ、**[環境設定]** に戻ります。

<!---1. Select the Log analytics workspace you created earlier *uniquenameDefender* to review the available options and pricing.

1. Select **Enable all plans** (to the right of Select Defender plan) and then select **Save**. Wait for the *"Microsoft Defender plan for workspace uniquenameDefender were saved successfully!"* notification to appear.

    >**Note:** If the page is not being displayed, refresh your Edge browser and try again.

1. Close the Defender plans page by selecting the 'X' on the upper right of the page to go back to the **Environment settings**. --->

### タスク 3: Microsoft Defender for Cloud ダッシュボードについて

1. Microsoft Azure portal の検索バーに「*Defender*」と入力し、**[Microsoft Defender for Cloud]** を選択します。

1. Microsoft Defender for Cloud の左側のナビゲーション メニューの *[全般]* セクションで、**[概要]** を選択します。

1. [概要] ブレードには、セキュリティ態勢の統一されたビューが表示され、セキュリティ態勢、規制コンプライアンス、ワークロード保護、Firewall Manager、インベントリ、Information Protection (プレビュー) など、複数の独立したクラウド セキュリティの柱があります。 これらの各柱には専用のダッシュボードもあり、その垂直に関するより深い洞察とアクションを可能にし、セキュリティプロフェッショナルには簡単なアクセスと可視性を提供します。

    >**注:** 上部のメニュー バーでは、[サブスクリプション] ボタンを選択してサブスクリプションを表示およびフィルター処理できます。 このラボでは 1 つだけ使用しますが、異なるサブスクリプションまたは追加のサブスクリプションを選択すると、選択したサブスクリプションのセキュリティ態勢を反映するようにインターフェイスが調整されます

1. **新機能**アイコン リンクをクリックします。新しいタブが開き、最新のリリース ノートが表示され、新機能、バグ修正などを最新の状態に保つことができます。

    >**注:** 上部のメニューの概数です。このビューでは、接続されているクラウド アカウントと共に、サブスクリプション、アクティブな推奨事項、セキュリティ アラートの概要を確認できます。

1. 上部のメニュー バーで、**[Azure サブスクリプション]** を選択します。 これにより、利用可能なサブスクリプションから選択できる環境設定が表示されます。

1. **[概要]** ページに戻り、**[セキュリティ態勢]** タイルを確認します。 現在の*セキュア スコア*と、完了した制御と推奨事項の数を確認できます。 このタイルを選択すると、サブスクリプション全体のドリルダウン ビューにリダイレクトされます

1. **[規制コンプライアンス]** タイルでは、Azure とハイブリッド クラウド環境の両方の継続的な評価に基づいて、コンプライアンス態勢に関する分析情報を取得できます。 このタイルには、Microsoft Cloud Security ベンチマークと最小のコンプライアンス規制標準である、次の標準が表示されます。 データを表示するには、まずセキュリティ ポリシーを追加する必要があります。

1. このタイルを選択すると、**規制コンプライアンス** ダッシュボードにリダイレクトされます。このダッシュボードでは、標準を追加したり、現在の標準を調べたりすることができます。

1. 次の演習では、*Microsoft Defender for Cloud* **セキュリティ態勢**と**規制コンプライアンス**について引き続き調査します。

## 演習 2 に進みます。
