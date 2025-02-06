---
lab:
  title: 演習 1 - Microsoft Defender for Cloud の有効化
  module: Learning Path 5 - Mitigate threats using Microsoft Defender for Cloud
---

# ラーニング パス 5 - ラボ 1 - 演習 1 - Microsoft Defender for Cloud の有効化

## ラボのシナリオ

あなたは、Microsoft Defender for Cloud を使用してクラウド ワークロード保護を実装している企業に勤務するセキュリティ運用アナリストです。 このラボでは、Microsoft Defender for Cloud を有効にします。

>**重要:** ラーニング パス #5 のラボ演習は、*スタンドアロン*環境にあります。 ラボを完了せずに終了する場合は、構成を再実行する必要があります。

### このラボの推定所要時間: 25 分

### タスク 1: オンプレミスのサーバーを接続する

このタスクでは、オンプレミスのサーバーを Azure サブスクリプションに接続します。 Azure Arc は、このサーバーにプレインストールされています。 このサーバーは、コンプライアンス標準とワークロード保護を適用するためのリソースを提供するのに、次の演習で使用します。

>**重要:** 次の手順は、以前に作業していたものとは異なるマシンで行います。 参照タブで仮想マシン名を探します。

1. 管理者として **WINServer** 仮想マシンにログインします。パスワードは **Passw0rd!** です。 必要に応じて。  

前述のように、Azure Arc は **WINServer** マシンにプレインストールされています。 これで、このマシンを Azure サブスクリプションに接続します。

1. *WINServer* マシンで、*検索*アイコンを選択し、**cmd** と入力します。

1. 検索結果の*コマンド プロンプト*を右クリックし、**[管理者として実行]** をクリックします。

1. コマンド プロンプト ウィンドウで、次のコマンドを入力します。 *Enter キーを押さないでください*

    ```cmd
    azcmagent connect -g "defender-RG" -l "EastUS" -s "Subscription ID string"
    ```

1. **サブスクリプション ID 文字列** を、ラボ ホスト (*リソース タブ) から提供された *サブスクリプション ID* に置き換えます。 引用符は保持してください。

1. **Enter** を入力してコマンドを実行します (これには数分かかる場合があります)。

    >**注**: *[このファイルを開く方法を選んでください]* というブラウザー選択ウィンドウが表示される場合は、**[Microsoft Edge]** を選択します。

1. *[サインイン]* ダイアログ ボックスに、ラボ ホスティング プロバイダーから提供された**テナントのメール アドレス**と**テナントのパスワード**を入力して、**[サインイン]** を選択します。 *認証が完了*したというメッセージが表示されるまで待ち、ブラウザー タブを閉じて、*コマンド プロンプト* ウィンドウに戻ります。

1. コマンドの実行が完了したら、*コマンド プロンプト* ウィンドウを開いたままにし、次のコマンドを入力して接続が成功したことを確認します。

    ```cmd
    azcmagent show
    ```

1. コマンド出力で、*Agent status* が **Connected** であることを確認します。

### タスク 2: Microsoft Defender for Cloud を有効にする

このタスクでは、Microsoft Defender for Cloud を有効にして構成します。

1. 管理者として **WIN1** 仮想マシンにログインします。パスワードは **Pa55w.rd** です。

1. Microsoft Edge ブラウザーで、Azure portal (<https://portal.azure.com> ) に移動します。
  
1. **サインイン** ダイアログ ボックスで、ラボ ホスティング プロバイダーの提供した管理者ユーザー名のテナント電子メール アカウントをコピーして貼り付け、**[次へ]** を選択します。

1. **パスワードの入力**ダイアログ ボックスで、ラボ ホスティング プロバイダーの提供した管理者のテナント パスワードをコピーして貼り付け、**サインイン**します。

1. Microsoft Azure portal の検索バーに「*Defender*」と入力し、**[Microsoft Defender for Cloud]** を選択します。

1. Microsoft Defender for Cloud の左側のナビゲーション メニューで *[管理]* セクションを開き、**[環境設定]** を選択します。

1. **[すべて展開]** ボタンを選択すると、すべてのサブスクリプションとリソースが表示されます。

1. **MOC Subscription-lodxxxxxxxx** サブスクリプション (または、お使いの言語での同等の名前) を選択します。

1. 現在、Defender for Cloud プランで保護されている Azure リソースを確認します。

<!---
    >**Important:** If all Defender plans are *Off*, select **Enable all plans**. Select the *$200/month Microsoft Defender for APIs Plan 1* and then select **Save**. Select **Save** at the top of the page and wait for the *"Defender plans (for your) subscription were saved successfully!"* notifications to appear.--->

1. *[クラウド セキュリティ態勢管理 (CSPM)]* セクションで、*Defender CSPM* に対して **[オン]** を選択します。

1. *[クラウド ワークロード保護 (CWP)]* セクションで、*Servers プラン 2* に対して **[オン]** を選択します。

1. ページの上部にある **[保存]** ボタンを選択します。

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

    >**注:** *[セキュリティ態勢]* タイルにあるセキュア スコアなどの情報は、計算に最大 24 時間かかります。 この情報は、このラボでは完全には入力されない場合があります。

1. **[規制コンプライアンス]** タイルでは、Azure とハイブリッド クラウド環境の両方の継続的な評価に基づいて、コンプライアンス態勢に関する分析情報を取得できます。 このタイルには、Microsoft Cloud Security ベンチマークと最小のコンプライアンス規制標準である、次の標準が表示されます。 データを表示するには、まずセキュリティ ポリシーを追加する必要があります。

1. このタイルを選択すると、**規制コンプライアンス** ダッシュボードにリダイレクトされます。このダッシュボードでは、標準を追加したり、現在の標準を調べたりすることができます。

1. 次の演習では、*Microsoft Defender for Cloud* **セキュリティ態勢**と**規制コンプライアンス**について引き続き調査します。

## 演習 2 に進みます。
