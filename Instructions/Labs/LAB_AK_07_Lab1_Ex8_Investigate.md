---
lab:
  title: 演習 8 - インシデントを調査する
  module: Module 7 - Create detections and perform investigations using Microsoft Sentinel
---

# <a name="module-7---lab-1---exercise-8---investigate-incidents"></a>モジュール 7 - ラボ 1 - 演習 8 - インシデントを調査する

## <a name="lab-scenario"></a>ラボのシナリオ


You are a Security Operations Analyst working at a company that implemented Microsoft Sentinel. You already created Scheduled and Microsoft Security Analytics rules. The Fusion and Anomalies Analytics rules are also enabled in your environment. Now is the time to investigate the Incidents created by them.

An incident can include multiple alerts. It is an aggregation of all the relevant evidence for a specific investigation. The properties related to the alerts, such as severity and status, are set at the incident level. After you let Microsoft Sentinel know what kinds of threats you are looking for and how to find them, you can monitor detected threats by investigating incidents.


### <a name="task-1-investigate-an-incident"></a>タスク 1:問題を調査する

このタスクでは、インシデントを調査します。

1. 管理者として WIN1 仮想マシンにログインします。パスワードは**Pa55w.rd**。  

1. Edge ブラウザーで、Azure portal (https://portal.azure.com ) に移動します。

1. **[サインイン]** ダイアログ ボックスで、ラボ ホスティング プロバイダーから提供された**テナントの電子メール** アカウントをコピーして貼り付け、 **[次へ]** を選択します。

1. **[パスワードの入力]** ダイアログ ボックスで、ラボ ホスティング プロバイダーから提供された**テナントのパスワード**をコピーして貼り付け、 **[サインイン]** を選択します。

1. Azure portal の検索バーに「*Sentinel*」と入力し、**[Microsoft Sentinel]** を選択します。

1. 先ほど作成した Microsoft Sentinel ワークスペースを選択します。

1. **インシデント**ページを選択します。

1. インシデントの一覧を確認します。

    ><bpt id="p1">**</bpt>Note:<ept id="p1">**</ept> The Analytics rules are generating alerts and incidents on the same specific log entry. Remember that this was done in the <bpt id="p1">*</bpt>Query scheduling<ept id="p1">*</ept> configuration to generate more alerts and incidents to be utilized in the lab.
  
1. *[MDE Startup RegKey]* インシデントのいずれかを選択します。

1. Review the incident details on the right blade that opened. Scroll down and select the <bpt id="p1">**</bpt>View full details<ept id="p1">**</ept> button.

1. インシデントの左側のブレードで、状態を **[アクティブ]** に変更し、 **[適用]** を選択します。

1. *[タグ]* 領域まで下にスクロールし、[**+**] を選択して「**RegKey**」と入力し、**[OK]** を選択します。

1. ページの中央で、 **[コメント]** タブを選択します。

1. コメント ボックスに、「*I will research this*」と入力して **[コメント]** ボタンを選択し、新しいコメントを送信します。

1. あなたは、Microsoft Sentinel を実装した会社で働いているセキュリティ運用アナリストです。

1. あなたはスケジュール済みおよび Microsoft セキュリティ分析ルールを既に作成しています。

1. Fusion と異常分析ルールも環境で有効になっています。

1. ここで、それらによって作成されたインシデントを調査します。

1.  When you select an entity, a window on the right opens for more detailed information. Review the <bpt id="p1">**</bpt>Info<ept id="p1">**</ept> page.

1. インシデントには複数のアラートを含めることができます。

1. **[エンティティ]** ボタンを選択し、*WIN1* に関連する *[エンティティ]* と *[アラート]* を確認します。

1. ページの右上にある **[X]** を選択して、調査グラフを閉じます。

1. これは、特定の調査に関連するすべての証拠を集計したものです。

1. 重大度や状態など、アラートに関連するプロパティはインシデント レベルで設定されます。

## <a name="proceed-to-exercise-9"></a>演習 9 に進む
