---
lab:
  title: 演習 2 - プレイブックを作成する
  module: Learning Path 7 - Create detections and perform investigations using Microsoft Sentinel
---

# ラーニング パス 7 - ラボ 1 - 演習 2 - プレイブックを作成する

## ラボのシナリオ

![ラボの概要。](../Media/SC-200-Lab_Diagrams_Mod7_L1_Ex2.png)

あなたは Microsoft Sentinel を実装した企業で働いているセキュリティ運用アナリストです。 Microsoft Sentinel を使って脅威を検出および軽減する方法を学習する必要があります。 ここで、Microsoft Sentinel からルーチンとして実行できるアクションに応答して修復する必要があります。

プレイブックを使用すると、脅威への対応を自動化および調整したり、内部と外部両方の他のシステムと統合したり、分析ルールまたは自動化ルールによってそれぞれトリガーされた場合に、特定のアラートやインシデントに応答して自動的に実行されるように設定できます。 

>                **メモ:** このラボをご自分のペースでクリックして進めることができる、 **[ラボの対話型シミュレーション](https://mslabs.cloudguides.com/guides/SC-200%20Lab%20Simulation%20-%20Create%20a%20playbook)** が用意されています。 対話型シミュレーションとホストされたラボの間に若干の違いがある場合がありますが、示されている主要な概念とアイデアは同じです。 


### タスク 1:Microsoft Teams でセキュリティ オペレーション センター チームを作成する

このタスクでは、このラボで使う Microsoft Teams のチームを作成します。

1. 管理者として WIN1 仮想マシンにログインします。パスワードは**Pa55w.rd**。  

1. Microsoft Edge ブラウザーで、新しいタブを開き、Microsoft Teams ポータル (https://teams.microsoft.com) に移動します。

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


### タスク 2:Microsoft Sentinel プレイブックを作成する

このタスクでは、Microsoft Sentinel でプレイブックとして使用されるロジック アプリを作成します。

1. Microsoft Edge ブラウザーで、[Microsoft Sentinel on GitHub](https://github.com/Azure/Azure-Sentinel) に移動します。

<!--- the Azure portal at https://portal.azure.com.

1. In the **Sign in** dialog box, copy and paste in the **Tenant Email** account provided by your lab hosting provider and then select **Next**.

1. In the **Enter password** dialog box, copy and paste in the **Tenant Password** provided by your lab hosting provider and then select **Sign in**.

1. In the Search bar of the Azure portal, type *Sentinel*, then select **Microsoft Sentinel**.

1. Select your Microsoft Sentinel Workspace you created earlier.

1. Select the **Community** page under the *Content management* area on the left side of the page.

1. On the right pane, select the **Onboard community content** link. This opens a new tab in the Microsoft Edge Browser for Microsoft Sentinel GitHub content. **Hint:** You might need to scroll right to see the link. Alternatively, follow this link instead: [Microsoft Sentinel on GitHub](https://github.com/Azure/Azure-Sentinel). --->

1. 下にスクロールして、**Solutions** フォルダーを選択します。

1. 次に、''**SentinelSOARessentials**'' フォルダー、''**Playbooks**'' フォルダーの順に選択します。

1. "**Post-Message-Teams**" フォルダーを選択します。

1. readme.md ボックスで、[Quick Deployment] (クイック デプロイ) セクションの **[Deploy with incident trigger (recommended)] (インシデント トリガーでデプロイする (推奨))** まで下にスクロールして、 **[Azure へのデプロイ]** ボタンを選びます。**  

1. [Azure サブスクリプション] が選択されていることを確認します。

1. リソース グループで **[新規作成]** を選択し、「*RG-Playbooks*」と入力して **[OK]** を選択します。

1. *[リージョン]* の既定値は **[(米国) 米国東部]** のままにします。

1. [プレイブック名] を "PostMessageTeams-OnIncident" に変更して、 **[確認と作成]** を選びます。**

1. ここで **[作成]** を選択します。 

    >**注:**  次のタスクに進む前に、デプロイが完了するまで待機します。

### タスク 3:Microsoft Sentinel プレイブックを更新する

このタスクでは、作成した新しいプレイブックを適切な接続情報で更新します。

1. Azure portal の検索バーに「*Sentinel*」と入力してから、**[Microsoft Sentinel]** を選択します。

1. Microsoft Sentinel ワークスペースを選択します。

1. [構成] 領域から **[自動化]** を選択し、 **[アクティブなプレイブック]** タブを選択してください。**

1. プレイブックが表示されない場合は、コマンド バーの **[最新の情報に更新]** を選んでください。 前の手順で作成したプレイブックが、**Microsoft Sentinel インシデント**の *[トリガーの種類]* で表示されます。

1. **PostMessageTeams-OnIncident** というプレイブック名を選択します。

1. *PostMessageTeams-OnIncident* の Logic App ページで、コマンド メニューの **[編集]** を選択します。

    >**注:** 場合によっては、ページを更新する必要があります。

1. "最初" のブロックの **[Microsoft Sentinel インシデント (プレビュー)]** を選択します。**

1. **[接続の変更]** リンクを選択します。

1. **[新規追加]** を選択し、 **[サインイン]** を選択します。 新しいウィンドウで、メッセージが表示されたら、Azure サブスクリプション管理者の資格情報を選択します。 ブロックの最後の行に "Connected to your-admin-username" (管理者ユーザー名に接続済み) と表示されます。

1. 次に、"2 番目" のブロック、 **[接続]** を選択します。**

1. **[新規追加]** を選択し、メッセージが表示されたら Azure 管理者の資格情報を選択します。 ブロックの最後の行に "Connected to your-admin-username" (管理者ユーザー名に接続済み) と表示されます。

1. ブロックの名前が **[メッセージを投稿する (V3)(プレビュー)]** に変更されました。 *[Teams]* フィールドの最後にある **[X]** を選択して内容をクリアします。 フィールドは、Microsoft Teams から利用可能な Teams の一覧を含むドロップダウンに変更されます。 **[SOC]** を選択します。

1. *[チャネル]* フィールドでも同じ操作を行い、フィールドの末尾にある **[X]** を選択して内容をクリアします。 フィールドは、SOC チームのチャネルの一覧を含むドロップダウンに変更されます。 **[新しいアラート]** を選択します。

1. コマンド バーの **[保存]** を選択します。 これらはのちのラボで使用します。

## 演習 3 に進む
