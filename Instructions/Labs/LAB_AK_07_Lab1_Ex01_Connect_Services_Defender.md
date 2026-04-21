---
lab:
  title: 演習 1 - データ コネクタを使用して Microsoft Sentinel にデータを接続する
  module: Learning Path 7 - Connect logs to Microsoft Sentinel
  description: あなたは Microsoft Sentinel を実装した企業で働いているセキュリティ運用アナリストです。 組織内の多くのデータ ソースからのログ データを接続する方法について学習する必要があります。 組織には、Microsoft 365、Microsoft Defender XDR、Azure リソース、Azure 以外の仮想マシンなどからのデータがあります。最初に、Microsoft のソースに接続します。
  duration: 20 minutes
  level: 200
  islab: true
  primarytopics:
    - Azure
    - Microsoft 365
    - Microsoft Defender
    - Microsoft Defender XDR
    - Microsoft Sentinel
---

# ラーニング パス 7 - ラボ 1 - 演習 1 - データ コネクタを使用して Microsoft Sentinel にデータを接続する

## ラボのシナリオ

![ラボの概要。](../Media/SC-200-Lab_Diagrams_Mod6_L1_Ex1.png)

あなたは Microsoft Sentinel を実装した企業で働いているセキュリティ運用アナリストです。 組織内の多くのデータ ソースからのログ データを接続する方法について学習する必要があります。 組織には、Microsoft 365、Microsoft Defender XDR、Azure リソース、Azure 以外の仮想マシンなどからのデータがあります。最初に、Microsoft のソースに接続します。

>**重要:** ラーニング パス #7 のラボ演習は、*スタンドアロン*環境にあります。 ラボを完了せずに終了する場合は、構成を再実行する必要があります。

### このラボの推定所要時間: 20 分

### タスク 1: Microsoft Defender XDR で Microsoft Sentinel ワークスペースにアクセスする

このタスクでは、Microsoft Sentinel ワークスペースにアクセスします。

>**注:** Microsoft Sentinel は既に、あなたの Azure サブスクリプション内に **sentinelworkspace-01** という名前で事前デプロイされており、必要な *Content Hub* ソリューションがインストール済みです。

1. 管理者として **WIN1** 仮想マシンにログインします。パスワードは **Pa55w.rd** です。  

1. Microsoft Edge ブラウザーを開きます。

1. Edge ブラウザーで、Defender XDR (`https://security.microsoft.com`) に移動します。

1. **[サインイン]** ダイアログ ボックスで、ラボ ホスティング プロバイダーから提供された**テナントの電子メール** アカウントをコピーして貼り付け、**[次へ]** を選択します。

1. **[パスワードの入力]** ダイアログ ボックスで、ラボ ホスティング プロバイダーから提供された**テナントパスワード**をコピーして貼り付け、**[サインイン]** を選択します。

    >**注:**  パスワードの代わりに "一時アクセス パス" (TAP) を入力するように求められる場合があります。** これは、[リソース] タブにも表示されます。メッセージが表示されたら、TAP 値をコピーして貼り付け、**[サインイン]** を選択します。

1. 次のタスクに進みます。

### タスク 2: Microsoft Defender for Cloud データ コネクタを管理する

このタスクでは、Microsoft Defender for Cloud データ コネクタの管理について確認します。

1. Microsoft Defender のナビゲーション メニューで、下スクロールして **[Microsoft Sentinel]** セクションを展開します。

1. **[コンテンツ管理]** セクションを展開して **[Content Hub]** を選択します。

1. *[コンテンツ ハブ]* で、「**Microsoft Defender for Cloud**」ソリューションを検索し、一覧から選択します。

1. Microsoft Defender for Cloud ソリューションの詳細ページで、**[管理]** を選択します。

    >**注:** *Microsoft Defender for Cloud* ソリューションでは、*サブスクリプション ベースの Microsoft Defender for Cloud (レガシ)* データ コネクタ、*テナント ベースの Microsoft Defender for Cloud (プレビュー)* データ コネクタ、および分析ルールがインストールされます。 テナントに複数のサブスクリプションがある場合、*テナント ベースの Microsoft Defender for Cloud (プレビュー)* データ コネクタが使用されます。

1. *[テナントベースの Microsoft Defender for Cloud]* データ コネクタ チェックボックスを選択し、**[コネクタ ページを開く]** を選択します。

1. Azure portal の [データ コネクタ] ページに新しいブラウザー タブが開きます。 状態は *[接続済み]* と表示されるはずです。

1. *[手順]* タブの *[構成]* セクションを確認します。

1. "Microsoft Defender for Cloud アラートは、Microsoft 365 Defender を介してストリームに接続される" ことと、"Microsoft Defender XDR が接続されている間は切断できない" ことに注意してください。

1. また、*[詳細] ペイン*で、*[データ型]* が *[SecurityAlert]* テーブルを使用することにも注意してください。

1. これで、このブラウザー タブを閉じて、Microsoft Defender XDR に戻ることができます。

### タスク 3: Azure アクティビティ データ コネクタを管理する

このタスクでは、*[Azure アクティビティ]* データ コネクタの管理について確認します。

1. 引き続き Microsoft Sentinel の *Content Hub* で操作する必要があります。

1. *[コンテンツ ハブ]* で、「**Azure Activity**」ソリューションを検索し、一覧から選択します。

1. *[Azure アクティビティ]* ソリューションの詳細ページで、**[管理]** を選択します。

    >**注:** *Azure Activity* ソリューションでは、*Azure Activity* データ コネクタ、13 個の分析ルール、14 個のハンティング クエリ、1 つのブックがインストールされます。

1. *Azure Activity* データ コネクタを選択し、 **[コネクタ ページを開く]** を選択します。

1. 状態は *[接続済み]* と表示されているはずです

1. **[設定]** タブの *[テーブル管理]* セクションで、**[AzureActivity]** テーブルのチェックボックスをオンにします。 *[データ保持設定]* の*歯車*が表示されます。

1. **[データ保持設定]** を選択し、*[Analytics レベル]* の *[AzureActivity の管理]* を確認します。

    >**注:** このデータ コネクタは、Defender XDR に完全に移植されます。

1. ページの右上隅にある **[X]** を選択して、*[AzureActivity の管理]* ページを閉じます。

1. ページの上部にある **[詳細オプション]** タブを選択して、*[UEBA の構成]* の設定を確認します。 この設定は、*Azure アクティビティに対して有効になっていることに注意してください。

1. ブラウザーの*階層リンク*に従って *Content Hub に戻り、終了します。

## 演習 2 に進みます。
