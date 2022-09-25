---
lab:
  title: 演習 2 - プレイブックを作成する
  module: Module 7 - Create detections and perform investigations using Microsoft Sentinel
---

# <a name="module-7---lab-1---exercise-2---create-a-playbook"></a>モジュール 7 - ラボ 1 - 演習 2 - プレイブックを作成する

## <a name="lab-scenario"></a>ラボのシナリオ

![ラボの概要。](../Media/SC-200-Lab_Diagrams_Mod7_L1_Ex2.png)

You are a Security Operations Analyst working at a company that implemented Microsoft Sentinel. You must learn how to detect and mitigate threats using Microsoft Sentinel. Now, you want to respond and reMediate actions that can be run from Microsoft Sentinel as a routine.

プレイブックを使用すると、脅威への対応を自動化および調整したり、内部と外部両方の他のシステムと統合したり、分析ルールまたは自動化ルールによってそれぞれトリガーされた場合に、特定のアラートやインシデントに応答して自動的に実行されるように設定できます。 


### <a name="task-1-create-a-security-operations-center-team-in-microsoft-teams"></a>タスク 1:Microsoft Teams でセキュリティ オペレーション センター チームを作成する

このタスクでは、このラボ用のMicrosoft Teamsを作成します。

1. 管理者として WIN1 仮想マシンにログインします。パスワードは**Pa55w.rd**。  

1. Edge ブラウザーで、新しいタブを開き、Microsoft Teams ポータル (https://teams.microsoft.com) ) に移動します。

1. **[サインイン]** ダイアログ ボックスで、ラボ ホスティング プロバイダーから提供された**テナントの電子メール** アカウントをコピーして貼り付け、 **[次へ]** を選択します。

1. **[パスワードの入力]** ダイアログ ボックスで、ラボ ホスティング プロバイダーから提供された**テナントのパスワード**をコピーして貼り付け、 **[サインイン]** を選択します。

1. 表示される可能性のある Teams ポップアップをすべて閉じます。

1. まだ選択されていない場合は、左側のメニューの **[Teams]** を選択し、下部にある **[チームに参加、またはチームを作成します]** を選択します。

1. メイン ウィンドウで **[チームの作成]** ボタンを選択します。

1. **[最初から]** ボタンを選択します。

1. **[プライベート]** ボタンを選択します。

1. チームに名前を付けます: 「**SOC**」と入力し、**[作成]** ボタンを選択します。

1. SOC にメンバーを追加 画面で、**スキップ** ボタンを選択します。 

1. [Teams] ブレードを下にスクロールし、新しく作成された SOC チームを見つけ、名前の右側にある省略記号 **[...]** を選択し、 **[チャネルの追加]** を選択します。

1. "新しいアラート" のチャネル名を入力し、**[追加]** ボタンを選択します。**


### <a name="task-2-create-a-playbook-in-microsoft-sentinel"></a>タスク 2:Microsoft Sentinel プレイブックを作成する

このタスクでは、Microsoft Sentinel でプレイブックとして使用されるロジック アプリを作成します。

1. Edge ブラウザーで、Azure portal (https://portal.azure.com ) に移動します。

1. **[サインイン]** ダイアログ ボックスで、ラボ ホスティング プロバイダーから提供された**テナントの電子メール** アカウントをコピーして貼り付け、 **[次へ]** を選択します。

1. **[パスワードの入力]** ダイアログ ボックスで、ラボ ホスティング プロバイダーから提供された**テナントのパスワード**をコピーして貼り付け、 **[サインイン]** を選択します。

1. Azure portal の検索バーに「*Sentinel*」と入力し、**[Microsoft Sentinel]** を選択します。

1. 先ほど作成した Microsoft Sentinel ワークスペースを選択します。

1. ページの左側にある *[コンテンツ管理]* 領域の下にある **[コミュニティ]** ページを選択します。

1. On the right pane, select the <bpt id="p1">**</bpt>Onboard community content<ept id="p1">**</ept> link. This will open a new tab in the Edge Browser for Microsoft Sentinel GitHub content.

1. **Solutions** フォルダーを選択します。

1. 次に、**Teams** フォルダーを選択し、**Playbooks** フォルダーを選択します。

1. "**Post-Message-Teams**" フォルダーを選択します。

1. readme.md ボックスで、2 番目の *[クイック デプロイ]* オプションの **[Deploy with alert trigger]/(アラート トリガーを使用してデプロイする)** まで下にスクロールし、 **[Azure に配置する]** ボタンを選択します。  

    ><bpt id="p1">**</bpt>VERY IMPORTANT<ept id="p1">**</ept>: Be aware that they are two different Microsoft Sentinel triggers to use, Incident and Alert. Make sure you are selecting the Alert (second) one.

1. [Azure サブスクリプション] が選択されていることを確認します。

1. リソース グループで **[新規作成]** を選択し、「*RG-Playbooks*」と入力して **[OK]** を選択します。

1. *[リージョン]* の既定値は **[(米国) 米国東部]** のままにします。

1. Make sure the <bpt id="p1">*</bpt>Playbook Name<ept id="p1">*</ept> is "PostMessageTeams-OnAlert" and select <bpt id="p2">**</bpt>Review + create<ept id="p2">**</ept>. <bpt id="p1">**</bpt>Hint:<ept id="p1">**</ept> If the name is different, go back to GitHub and select the <bpt id="p2">**</bpt>Deploy with alert trigger<ept id="p2">**</ept> playbook.

1. ここで **[作成]** を選択します。 

    >**注:**  次のタスクに進む前に、デプロイが完了するまで待機します。


### <a name="task-3-update-a-playbook-in-microsoft-sentinel"></a>タスク 3:Microsoft Sentinel プレイブックを更新する

このタスクでは、作成した新しいプレイブックを適切な接続情報で更新します。

1. Azure portal の検索バーに「*Sentinel*」と入力してから、**[Microsoft Sentinel]** を選択します。

1. Microsoft Sentinel ワークスペースを選択します。

1. *[構成]* 領域から **[自動化]** を選択し、 **[アクティブなプレイブック]** タブを選択します。

1. Select the <bpt id="p1">**</bpt>PostMessageTeams-OnAlert<ept id="p1">**</ept> playbook. <bpt id="p1">**</bpt>Hint:<ept id="p1">**</ept> If you do not see the playbook, refresh the Azure portal page by pressing Ctrl+F5.

1. *PostMessageTeams-OnAlert* の Logic App ページで、コマンド メニューの **[編集]** を選択します。

1. *"最初"* のブロックの **[Microsoft Sentinel アラート]** を選択します。

1. **[接続の変更]** リンクを選択します。

1. あなたは、Microsoft Sentinel を実装した会社で働いているセキュリティ運用アナリストです。

1. 次に、*2 番目の* ブロック、 **[アラート - インシデントの取得]** を選択します。

1. **[接続の変更]** リンクを選択します。

1. Microsoft Sentinel を使って脅威を検出および軽減する方法を学習する必要があります。

1. 次に、*3 番目の* ブロック、 **[接続]** を選択します。

1. ここで、Microsoft Sentinel からルーチンとして実行できるアクションに応答して修復する必要があります。

1. The block has now been renamed to <bpt id="p1">**</bpt>Post a message (V3)<ept id="p1">**</ept>, at the end of the <bpt id="p2">*</bpt>Team<ept id="p2">*</ept> field, select the <bpt id="p3">**</bpt>X<ept id="p3">**</ept> to clear the contents. The field will be changed to a drop-down with a listing of the available Teams from Microsoft Teams. Select <bpt id="p1">**</bpt>SOC<ept id="p1">**</ept>.

1. Do the same for the <bpt id="p1">*</bpt>Channel<ept id="p1">*</ept> field, select the <bpt id="p2">**</bpt>X<ept id="p2">**</ept> at the end of the field to clear the contents. The field will be changed to a drop-down with a listing of the Channels of the SOC Teams. Select <bpt id="p1">**</bpt>New Alerts<ept id="p1">**</ept>.

1. コマンド バーの **[保存]** を選択します。

これらはのちのラボで使用します。

## <a name="proceed-to-exercise-3"></a>演習 3 に進む
