---
lab:
  title: 演習 2 - Microsoft Defender for Endpoint を使用した攻撃の軽減
  module: Module 2 - Mitigate threats using Microsoft Defender for Endpoint
---

# <a name="module-2---lab-1---exercise-2---mitigate-attacks-with-microsoft-defender-for-endpoint"></a>モジュール 2 - ラボ 1 - 演習 2 - Microsoft Defender for Endpoint を使用した攻撃の軽減

## <a name="lab-scenario"></a>ラボのシナリオ

![ラボの概要。](../Media/SC-200-Lab_Diagrams_Mod2_L1_Ex2.png)

You are a Security Operations Analyst working at a company that is implementing Microsoft Defender for Endpoint. Your manager plans to onboard a few devices to provide insight into required changes to the Security Operations (SecOps) team response procedures.

Defender for Endpoint の攻撃緩和機能を確認するため、シミュレーション攻撃を 2 回行います。


### <a name="task-1-simulated-attacks"></a>タスク 1:シミュレーション攻撃

このタスクでは、シミュレーション攻撃を 2 回行って、Microsoft Defender for Endpoint の機能を確認します。

1. Microsoft Edge ブラウザーの Microsoft 365 Defender ポータルにまだアクセスしていない場合は、(https://security.microsoft.com) に移動し、テナントの Admin としてログインします。

1. メニューから、 **[エンドポイント]** の下で、 **[評価とチュートリアル]** を選択し、左側から **[チュートリアルとシミュレーション]** を選択します。

1. **[チュートリアル]** タブを選択します。

1. Under <bpt id="p1">*</bpt>Automated investigation (backdoor)<ept id="p1">*</ept> you will see a message describing the scenario. Below this paragraph, click <bpt id="p1">**</bpt>Read the walkthrough<ept id="p1">**</ept>. A new browser tab opens which includes instructions to perform the simulation.

1. In the new browser tab, locate the section named <bpt id="p1">**</bpt>Run the simulation<ept id="p1">**</ept> (page 5, starting at step 2) and follow the steps to run the attack. <bpt id="p1">**</bpt>Hint:<ept id="p1">**</ept> The simulation file <bpt id="p2">*</bpt>RS4_WinATP-Intro-Invoice.docm<ept id="p2">*</ept> can be found back in portal, just below the <bpt id="p3">**</bpt>Read the walkthrough<ept id="p3">**</ept> you selected in the previous step by selecting the <bpt id="p4">**</bpt>Get simulation file<ept id="p4">**</ept> button. 

1. 最後の 3 つの手順を繰り返して、 *[Automated investigation (fileless attack)]\(自動調査 (ファイルレス攻撃)\)* を今すぐ実行します。

1. Microsoft 365 Defender ポータルで、左側のメニュー バーから **[インシデントとアラート]** を選択し、 **[インシデント]** を選択します。

1. A new incident called "Multi-stage incident..." will appear in the right pane. Allow at least 5 minutes for the incident to appear. Click the incident name to load its details.

1. **[インシデントの管理]** ボタンを選択すると、新しいウィンドウ ブレードが表示されます。 

1. **[Incident tags]\(インシデント タグ\)** に「Tutorial」と入力し、**[Tutorial (Create new)]\(チュートリアル (新規作成)\)** を選択して新しいタグを作成します。 

1. **[自分に割り当て]** トグルを選択して、インシデントの所有者として自分のユーザー アカウントを追加します。 

1. **[分類]** で、ドロップダウン メニューを展開します。 

1. **[情報、予期されるアクティビティ]** で、 **[セキュリティ テスト]** を選択します。 

1. 必要に応じてコメントを追加し、 **[保存]** をクリックして終了します。

1. Review the contents of the Alerts, Devices, Users, Investigations, Evidence and Response, Graph tabs. <bpt id="p1">**</bpt>Hint:<ept id="p1">**</ept> Some tabs might be hidden due the size of your display. Select the ellipsis tab (...) to make them appear.

>あなたは Microsoft Defender for Endpoint を実装している企業で働いているセキュリティ運用アナリストです。

## <a name="you-have-completed-the-lab"></a>これでラボは完了です。
