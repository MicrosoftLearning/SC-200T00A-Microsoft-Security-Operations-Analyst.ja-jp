---
lab:
  title: 演習 1 ‐ Microsoft セキュリティ規則を変更する
  module: Learning Path 9 - Create detections and perform investigations using Microsoft Sentinel
---

# ラーニング パス 9 - ラボ 1 - 演習 1 - Microsoft セキュリティ規則を変更する

## ラボのシナリオ

![ラボの概要。](../Media/SC-200-Lab_Diagrams_Mod7_L1_Ex1.png)

あなたは、Microsoft Sentinel を実装した会社で働いているセキュリティ運用アナリストです。 Azure Sentinel を使って脅威を検出および軽減する方法を学習する必要があります。 まず、Defender for Cloud から Microsoft Sentinel に送信されるアラートを重大度でフィルター処理する必要があります。

>**重要:** ラーニング パス #9 のラボ演習は、*スタンドアロン*環境にあります。 ラボを完了せずに終了する場合は、構成を再実行する必要があります。

### このラボの推定所要時間: 10 分

### タスク 1:Microsoft Securityルールの有効化

このタスクでは、Microsoftセキュリティルールを有効化します。

>**注:** Microsoft Sentinel は、**defenderWorkspace** という名前で Azure サブスクリプションに事前にデプロイされており、必要な*コンテンツ ハブ* ソリューションがインストールされています。

1. 管理者として WIN1 仮想マシンにログインします。パスワードは**Pa55w.rd**。  

1. Microsoft Edge ブラウザーで、Azure portal (<https://portal.azure.com>) に移動します。

1. **[サインイン]** ダイアログ ボックスで、ラボ ホスティング プロバイダーから提供された**テナントの電子メール** アカウントをコピーして貼り付け、**[次へ]** を選択します。

1. **[パスワードの入力]** ダイアログ ボックスで、ラボ ホスティング プロバイダーから提供された**テナントパスワード**をコピーして貼り付け、**[サインイン]** を選択します。

1. Azure portal の検索バーに「*Sentinel*」と入力してから、**[Microsoft Sentinel]** を選択します。

1. Microsoft Sentinel **defenderWorkspace** を選択します。

1. 構成領域から **[分析]** を選択します。

1. コマンド バーの **[+ 作成]** ボタンを選択して、 **[Microsoft インシデントの作成規則]** を選択します。

1. *[名前]* に「**Create incidents based on Defender for Cloud**」と入力します。

1. 下にスクロールし、*[Microsoft セキュリティ サービス]* で **[Microsoft Defender for Cloud]** を選びます。

1. [重大度でフィルター処理] で [カスタム] オプションを選び、重大度レベルとして **[低]** 、 **[中]** 、 **[高]** を選んで、ルールに戻ります。** **

1. **[次へ: 自動応答]** ボタンを選択してから、 **[次へ: 確認と作成]** ボタンを選択します。

1. 行った変更を確認し、 **[保存]** ボタンを選択します。 分析ルールが保存され、Defender for Cloud にアラートがある場合は、インシデントが作成されます。

1. これで、1 つの *Fusion* と 2 つの *Microsoft Security* のアラートの種類が作成されます。

## 演習 2 に進みます。
