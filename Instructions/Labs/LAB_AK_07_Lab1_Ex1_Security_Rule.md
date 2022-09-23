---
lab:
  title: 演習 1 ‐ Microsoft セキュリティ規則を変更する
  module: Module 7 - Create detections and perform investigations using Microsoft Sentinel
ms.openlocfilehash: 266335a86b6ee3c1d86aaa4acf67cd1785aa5d2f
ms.sourcegitcommit: f8918eddeaa7a7a480e92d0e5f2f71143c729d60
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/08/2022
ms.locfileid: "147038005"
---
# <a name="module-7---lab-1---exercise-1---modify-a-microsoft-security-rule"></a>モジュール 7 - ラボ 1 - 演習 1 - Microsoft セキュリティ規則を有効にする

## <a name="lab-scenario"></a>ラボのシナリオ

![ラボの概要。](../Media/SC-200-Lab_Diagrams_Mod7_L1_Ex1.png)

あなたは、Microsoft Sentinel を実装した会社で働いているセキュリティ運用アナリストです。 Azure Sentinel を使って脅威を検出および軽減する方法を学習する必要があります。 まず、Defender for Cloud から Microsoft Sentinel に送信されるアラートを重大度でフィルター処理する必要があります。 


### <a name="task-1-activate-a-microsoft-security-rule"></a>タスク 1:Microsoft Securityルールの有効化

このタスクでは、Microsoftセキュリティルールを有効化します。

1. 管理者として WIN1 仮想マシンにログインします。パスワードは **Pa55w.rd**。  

1. Edge ブラウザーで、Azure portal (https://portal.azure.com) ) に移動します。

1. **[サインイン]** ダイアログ ボックスで、ラボ ホスティング プロバイダーから提供された **テナントの電子メール** アカウントをコピーして貼り付け、**[次へ]** を選択します。

1. **[パスワードの入力]** ダイアログ ボックスで、ラボ ホスティング プロバイダーから提供された **テナント パスワード** をコピーして貼り付け、**[サインイン]** を選択します。

1. Azure portal の検索バーに「*Sentinel*」と入力し、**[Microsoft Sentinel]** を選択します。

1. 前のラボで作成した Microsoft Sentinel ワークスペースを選択します。

1. 構成領域から **[分析]** を選択します。 既定で、*アクティブな規則* が表示されます。

1. **[Microsoft Defender for Cloud に基づいてインシデントを作成する]** を選択します。 このルールは、"モジュール 6 - 演習 1 - タスク 4" で構成した Defender for Cloud のコネクタによってアクティブ化されました。 

1. 右側のブレードで、 **[編集]** ボタンを選択します。

1. ページを下にスクロールし、[Analytics ルール ロジック - 重大度でフィルター処理する] の下の *[カスタム]* ドロップダウン リストを選択します。

1. 重大度レベルで **[低]** を選択解除し、ルールに戻ります。

1. 下部にある **[次: 自動応答]** ボタンを選択し、 **[次へ:Review]\(次へ: 確認\)** をクリックします。

1. 行った変更を確認し、 **[保存]** ボタンを選択します。 分析ルールが保存されます。

## <a name="proceed-to-exercise-2"></a>演習 2 に進みます。
