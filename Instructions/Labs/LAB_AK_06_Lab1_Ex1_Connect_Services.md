---
lab:
    title: '演習 1 - データ コネクタを使用して Microsoft Sentinel にデータを接続する'
    module: 'モジュール 6 – ログを Microsoft Sentinel に接続する'
---

# モジュール 6 - ラボ 1 - 演習 1 - データ コネクタを使用して Microsoft Sentinel にデータを接続する

## ラボ シナリオ

あなたは、Microsoft Sentinel を実装した会社で働いているセキュリティ オペレーションアナリストです。組織内の多くのデータ ソースからのログ データを接続する方法について学習する必要があります。組織には、Microsoft 365、Microsoft 365 Defender、Azure リソース、Azure 以外の仮想マシン、ネットワーク アプライアンスからのデータがあります。

あなたは、Microsoft Sentinel データ コネクタを使用して、さまざまなソースからのログ データを統合することを計画しています。組織の各データ ソースを適切な Microsoft Sentinel データ コネクタにマップする管理用のコネクタ計画を作成する必要があります。


### タスク 1: Microsoft Sentinel ワークスペースにアクセスする。

このタスクでは、Microsoft Sentinel ワークスペースにアクセスします。

1. 管理者として WIN1 仮想マシンにログインします。パスワードは**Pa55w.rd** です。  

2. Microsoft Edge ブラウザーを開きます。

3. Microsoft Edge ブラウザーで Azure portal (https://portal.azure.com) に移動します。

4. **サインイン** ダイアログ ボックスで、ラボ ホスティング プロバイダーから提供された**テナントの電子メール**アカウントをコピーして貼り付け、「**次へ**」を選択します。

5. **パスワードの入力**ダイアログ ボックスで、ラボ ホスティング プロバイダーから提供された**テナントパスワード** をコピーして貼り付け、「**サインイン**」を選択します。

6. Azure portal の検索バーに「*Sentinel*」と入力し、「**Microsoft Sentinel Sentinel**」を選択します。

7. 前のラボで作成した Microsoft Sentinel ワークスペースを選択します。


### タスク 2: Azure Active Directory コネクタを接続する

このタスクでは、Azure Active Directory コネクタを Microsoft Sentinel に接続します。

1. 構成 セクションで、「**データコネクタ**」を選択します。  データ コネクタ ページで、リストから**Azure Active Directory** タイルを選択します。

2. コネクタ情報ブレードで「**コネクタページを開く**」を選択します。

3. 構成から「**Sign-in Logs**」および「**監査ログ**」オプションを選択し、「**変更の適用**」を選択します。


### タスク 3: Azure Active Directory Identity Protection コネクタを接続する

このタスクでは、Azure Active Directory Identity Protection コネクタを Microsoft Sentinel に接続します。

1. 「データ コネクタ」タブから、「**Azure Active Directory Identity Protection**」コネクタを検索し、リストから選択します。

2. コネクタ情報ブレードで「**コネクタページを開く**」を選択します。

3. 「構成」 領域から 「**接続**」 ボタンを選択します。


### タスク 4: Microsoft Defender for Cloud コネクタを接続する。

このタスクでは、Microsoft Defender for Cloud コネクタを接続します。

1. 「データ コネクタ」タブから、「**Microsoft Defender for Cloud**」コネクタを検索し、リストから選択します。

2. コネクタ情報ブレードで「**コネクタページを開く**」を選択します。

3. 「サブスクリプション」 の下の 「構成」 領域で、Azure サブスクリプションを選択します。

4. Azure サブスクリプションの「状態」を「**接続済み**」に変更します。

5. 下にスクロールして、「Create incidents - Recommended!」 領域で、「**Enable**」 をクリックします。


### タスク 5: Microsoft Defender for Cloud Apps コネクタを接続する。

このタスクでは、Microsoft Defender for Cloud Apps コネクタを接続します。

1. 「データ コネクタ」タブから、「**Microsoft Defender for Cloud Apps**」コネクタを検索し、リストから選択します。

2. コネクタ情報ブレードで「**コネクタページを開く**」を選択します。

3. 「**アラート**」 を選択し、「**変更の適用**」 をクリックします。


### タスク 6: Microsoft Defender for Office 365 を接続する

このタスクでは、Microsoft Defender for Office 365 コネクタを接続します。

1. 「データ コネクタ」タブから、「**Microsoft Defender for Office 365 (プレビュー)**」コネクタを検索し、リストから選択します。

2. コネクタ情報ブレードで「**コネクタページを開く**」を選択します。

3. 構成領域で、「**接続**」を選択します。


### タスク 7: Microsoft Defender for Identity コネクタ。

このタスクでは、Microsoft Defender for Identity コネクタ確認します。

1. 「データ コネクタ」タブから、「**Microsoft Defender for Identity**」コネクタを検索し、リストから選択します。

2. コネクタ情報ブレードで「**コネクタページを開く**」を選択します。

3. 接続オプションを確認します。接続しない。これは情報提供のみを目的としています。


### タスク 8: Microsoft Defender for Endpointコネクタに接続する

このタスクでは、Microsoft Defender for Endpoint コネクタを接続します。

1. 「データ コネクタ」タブから、「**Microsoft Defender for Endpoint**」コネクタを検索し、リストから選択します。

2. コネクタ情報ブレードで「**コネクタページを開く**」を選択します。

3. 構成領域で、「**接続**」をクリックします。


### タスク 9: Microsoft 365 Defender コネクタを接続する

このタスクでは、Microsoft 365 Directory コネクタを接続します。

1. 「データ コネクタ」タブから、「**Microsoft 365 Defender (プレビュー)**」コネクタを検索し、リストから選択します。

2. コネクタ情報ブレードで「**コネクタページを開く**」を選択します。

3. 「**名前**」チェックボックスを選択して、Microsoft Defender for Endpoint のすべてのチェックボックスを選択します。

4. 「**変更の適用**」を選択します。


### タスク 10: Azure Activity コネクタを接続する。

このタスクでは、Azure Activity コネクタを接続します。

1. 「データ コネクタ」タブから、「**Azure Activity**」コネクタを検索し、リストから選択します。

2. コネクタ情報ブレードで「**コネクタページを開く**」を選択します。

3. 構成領域で、「**Launch Azure Policy Assignment Wizard>**」 (Azure ポリシーの割り当てウィザードの起動) を選択します。

4. **基本**タブで、「**スコープ**」の下で、3 つのドット付きのボタンを選択し、ドロップダウン リストからサブスクリプションを選択して、「**選択**」をクリックします。

5. 「**パラメーター**」タブを選択し、「**Primary Log Analytics ワークスペース**」ドロップダウン リストから、自分の Microsoft Sentinel ワークスペースを選択します。

6. 「**修復**」タブを選択し、「**修復タスクの作成**」チェックボックスを選択します。

7. 「**確認および作成**」ボタンを選択して、設定を確認します。

8. 「**作成**」を選択して完了します。

## 演習 2 に進みます。
