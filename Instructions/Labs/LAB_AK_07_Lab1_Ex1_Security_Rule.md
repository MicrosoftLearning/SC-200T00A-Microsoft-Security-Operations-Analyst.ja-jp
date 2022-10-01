---
lab:
  title: 演習 1 ‐ Microsoft セキュリティ規則を変更する
  module: Module 7 - Create detections and perform investigations using Microsoft Sentinel
---

# <a name="module-7---lab-1---exercise-1---modify-a-microsoft-security-rule"></a>モジュール 7 - ラボ 1 - 演習 1 - Microsoft セキュリティ規則を有効にする

## <a name="lab-scenario"></a>ラボのシナリオ

![ラボの概要。](../Media/SC-200-Lab_Diagrams_Mod7_L1_Ex1.png)

You are a Security Operations Analyst working at a company that implemented Microsoft Sentinel. You must learn how to detect and mitigate threats using Microsoft Sentinel. First, you need to filter the alerts coming from Defender for Cloud into Microsoft Sentinel, by Severity. 


### <a name="task-1-activate-a-microsoft-security-rule"></a>タスク 1:Microsoft Securityルールの有効化

このタスクでは、Microsoftセキュリティルールを有効化します。

1. 管理者として WIN1 仮想マシンにログインします。パスワードは**Pa55w.rd**。  

1. Edge ブラウザーで、Azure portal (https://portal.azure.com) ) に移動します。

1. **[サインイン]** ダイアログ ボックスで、ラボ ホスティング プロバイダーから提供された**テナントの電子メール** アカウントをコピーして貼り付け、**[次へ]** を選択します。

1. **[パスワードの入力]** ダイアログ ボックスで、ラボ ホスティング プロバイダーから提供された**テナント パスワード**をコピーして貼り付け、**[サインイン]** を選択します。

1. Azure portal の検索バーに「*Sentinel*」と入力し、**[Microsoft Sentinel]** を選択します。

1. 前のラボで作成した Microsoft Sentinel ワークスペースを選択します。

1. Select <bpt id="p1">**</bpt>Analytics<ept id="p1">**</ept> from the Configuration area. By default, you will see the <bpt id="p1">*</bpt>Active rules<ept id="p1">*</ept>. Click on <bpt id="p1">*</bpt>Rule templates<ept id="p1">*</ept>.

1. Search for and select <bpt id="p1">**</bpt>Create incidents based on Microsoft Defender for Cloud<ept id="p1">**</ept>. This rule was activated by the Defender for Cloud connector we configured in "Module 6 - Exercise 1 - Task 4". 

1. 右側のブレードで、 **[編集]** ボタンを選択します。

1. ページを下にスクロールし、[Analytics ルール ロジック - 重大度でフィルター処理する] の下の *[カスタム]* ドロップダウン リストを選択します。

1. 重大度レベルで **[低]** を選択解除し、ルールに戻ります。

1. 下部にある **[次: 自動応答]** ボタンを選択し、 **[次へ:Review](次へ: 確認)** をクリックします。

1. Review the changes made and select the <bpt id="p1">**</bpt>Save<ept id="p1">**</ept> button. The Analytics rule will be saved.

## <a name="proceed-to-exercise-2"></a>演習 2 に進みます。
