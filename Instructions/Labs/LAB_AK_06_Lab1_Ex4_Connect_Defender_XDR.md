---
lab:
  title: 演習 4 - データ コネクタを使用して Defender XDR を Microsoft Sentinel に接続する
  module: Learning Path 6 - Connect logs to Microsoft Sentinel
---

# ラーニング パス 6 - ラボ 1 - 演習 4 - データ コネクタを使用して Defender XDR を Microsoft Sentinel に接続する

## ラボのシナリオ

![ラボの概要。](../Media/SC-200-Lab_Diagrams_Mod6_L1_Ex4.png)

あなたは、Microsoft Defender XDR と Microsoft Sentinel の両方を展開した会社で働いているセキュリティ運用アナリストです。 Microsoft Sentinel を Defender XDR に接続する統合セキュリティ運用プラットフォームを準備する必要があります。 次の手順では、Defender XDR コンテンツ ハブ ソリューションをインストールし、Defender XDR データ コネクタを Microsoft Sentinel に展開します。

### タスク 1:Defender XDR を接続する

このタスクでは、Microsoft Defender XDR コネクタを展開します。

1. 管理者として WIN1 仮想マシンにログインします。パスワードは**Pa55w.rd**。  

1. Microsoft Edge ブラウザーで、Azure portal (<https://portal.azure.com>) に移動します。

1. **[サインイン]** ダイアログ ボックスで、ラボ ホスティング プロバイダーから提供された**テナントの電子メール** アカウントをコピーして貼り付け、**[次へ]** を選択します。

1. **[パスワードの入力]** ダイアログ ボックスで、ラボ ホスティング プロバイダーから提供された**テナントパスワード**をコピーして貼り付け、**[サインイン]** を選択します。

1. Azure portal の検索バーに「*Sentinel*」と入力してから、**[Microsoft Sentinel]** を選択します。

1. 先ほど作成した Microsoft Sentinel ワークスペースを選択します。

1. Microsoft Sentinel の左側のメニューで、 **[コンテンツ管理]** セクションまで下にスクロールし、 **[コンテンツ ハブ]** を選択します。

1. *[コンテンツ ハブ]* で、**Microsoft Defender XDR** ソリューションを検索し、リストから選択します。

1. *Microsoft Defender XDR* ソリューションの詳細ページで、**[インストール]** を選択します。

1. インストールが完了したら、**Microsoft Defender XDR** ソリューションを検索して選択します。

1. *Microsoft Defender XDR* ソリューションの詳細ページで、**[管理]** を選択します

>**注:**  *Microsoft Defender XDR* ソリューションでは、*Microsoft Defender XDR* データ コネクタ、ハンティング クエリ、ブック、分析ルールがインストールされます。

1. *[Microsoft Defender XDR]* データ コネクタ チェック ボックスをオンにし、**[コネクタ ページを開く]** を選択します。

1. *[手順]* タブの *[構成]* セクションで、*[これらの製品の Microsoft インシデント作成ルールをすべてオフにすることを**** お勧めします]* のチェック ボックスをオフにし、**[インシデントとアラートを接続する]** ボタンを選択します。

1. 接続が成功したことを示すメッセージが表示されるはずです。

## これでラボは完了です
