---
lab:
  title: 演習 2 - Microsoft Defender for Endpoint を使用した攻撃の軽減
  module: Learning Path 2 - Mitigate threats using Microsoft Defender for Endpoint
---

# ラーニング パス 2 - ラボ 1 - 演習 2 - Microsoft Defender for Endpoint を使用した攻撃の軽減

## ラボのシナリオ

![ラボの概要。](../Media/SC-200-Lab_Diagrams_Mod2_L1_Ex2_10_19.png)

あなたは Microsoft Defender for Endpoint を実装している企業で働いているセキュリティ運用アナリストです。 あなたの上司は、いくつかのデバイスをオンボードして、セキュリティ オペレーション (SecOps) チームの応答手順で必要な変更に関する情報を提供しようとしています。

Defender for Endpoint の攻撃の軽減機能を確認するために、デバイスのオンボードが成功したことを確認し、そのプロセス中に発生したアラートとインシデントを調査します。

>**メモ:** このラボをご自分のペースでクリックして進めることができる、 **[ラボの対話型シミュレーション](https://mslabs.cloudguides.com/guides/SC-200%20Lab%20Simulation%20-%20Mitigate%20attacks%20with%20Microsoft%20Defender%20for%20Endpoint)** が用意されています。 対話型シミュレーションとホストされたラボの間に若干の違いがある場合がありますが、示されている主要な概念とアイデアは同じです。

### タスク 1: デバイスのオンボードを確認する

このタスクでは、デバイスが正常にオンボードされていることを確認し、テスト アラートを作成します。

1. Microsoft Edge ブラウザーの Microsoft Defender XDR ポータルにまだアクセスしていない場合は、(https://security.microsoft.com) に移動して、お使いになっているテナントの管理者としてログインします。

1. 左側のメニューの **[アセット]** 領域の下で **[デバイス]** を選択します。 [デバイス] ページに WIN1 が表示されるまで待ち続けます。 そうしないと、後で生成されるアラートを表示するために、このタスクを繰り返さなければならなくなる可能性があります。

    >**注:**  オンボード プロセスを完了してから 1 時間経ってもデバイス一覧にデバイスが表示されない場合は、オンボードまたは接続に問題があるおそれがあります。

1. 左側のメニュー バーから **[設定]** を選択し、設定 ページから **[エンドポイント]** を選択します。

1. [デバイス管理] セクションで **[オンボード]** を選択し、 *[Windows 10 と 11]* がオペレーティング システムとして選択されていることを確認します。 *"最初のデバイスがオンボードされました"* というメッセージが *[完了]* と表示されるようになります。

1. 下にスクロールし、セクション *[2. 検出テストを実行します]* の下で **[コピー]** ボタンを選択して、検出テストのスクリプトをコピーします。  

1. WIN1 仮想マシンの Windows 検索バーで「**CMD**」と入力し、コマンド プロンプト アプリの右側のペインで **[管理者として実行]** を選択します。

1. [ユーザー アカウント制御] ウィンドウが表示されたら **[はい]** を選択し、アプリの実行を許可します。 

1. **[管理者: コマンド プロンプト]** ウィンドウでスクリプトを右クリックして貼り付け、**Enter** キーを押して実行します。

    >**注:**  このウィンドウは、スクリプトが正常に実行されると自動的に閉じられ、数分後に Microsoft Defender XDR ポータル内にアラートが生成されます。

<!--- ### Task 2: Simulated Attacks

>**Note:** The Evaluation lab and the Tutorials & simulations section of the portal is no longer available. Please refer to the **[interactive lab simulation](https://mslabs.cloudguides.com/guides/SC-200%20Lab%20Simulation%20-%20Mitigate%20attacks%20with%20Microsoft%20Defender%20for%20Endpoint)** for a demonstration of the simulated attacks.

1. From the left menu, under **Endpoints**, select **Evaluation & tutorials** and then select **Tutorials & simulations** from the left side.

1. Select the **Tutorials** tab.

1. Under *Automated investigation (backdoor)* you will see a message describing the scenario. Below this paragraph, click **Read the walkthrough**. A new browser tab opens which includes instructions to perform the simulation.

1. In the new browser tab, locate the section named **Run the simulation** (page 5, starting at step 2) and follow the steps to run the attack. **Hint:** The simulation file *RS4_WinATP-Intro-Invoice.docm* can be found back in portal, just below the **Read the walkthrough** you selected in the previous step by selecting the **Get simulation file** button.

    <!--- 1. Repeat the last 3 steps to run another tutorial, *Automated investigation (fileless attack)*. This is no longer working due to win1 AV --->

### タスク 2:アラートとインシデントを調査する

このタスクでは、先ほどのタスクのオンボード検出テスト スクリプトによって生成されたアラートとインシデントを調査します。

1. Microsoft Defender XRD ポータルで、左側のメニュー バーから **[インシデントとアラート]** を選択した後、**[アラート]** を選択します。

1. **[アラート]** ペインで、"疑わしい PowerShell コマンドライン" という名前のアラートを選択してその詳細を読み込みます。**

1. "アラート ストーリー" タイムラインを確認した後、"詳細" タブと "おすすめ" タブを確認します。******

    >**注:**  アラートの "詳細" タブで、"インシデントの詳細" セクションまで下にスクロールし、"1 つのエンドポイント上の実行インシデント" リンクを選択することでインシデントを開くことができます。******

1. Microsoft Defender XRD ポータルで、左側のメニュー バーから **[インシデントとアラート]** を選択した後、**[インシデント]** を選択します

1. "1 つのエンドポイント上の実行インシデント" という名前の新しいインシデントが右側のペインに表示されます。** インシデント名を選択して詳細を読み込みます。

1. (鉛筆アイコンが付いている) **[インシデントの管理]** リンクを選択すると、新しいウィンドウ ブレードが表示されます。

1. **[Incident tags]\(インシデント タグ\)** に「Simulation」と入力し、**[Simulation (Create new)]\(シミュレーション (新規作成)\)** を選んで新しいタグを作成します。

1. **[割り当て先]** トグルを選択して、インシデントの所有者として自分のユーザー アカウント (Me) を追加します。

1. **[分類]** で、ドロップダウン メニューを展開します。

1. **[情報、予期されるアクティビティ]** で、 **[セキュリティ テスト]** を選択します。

1. 必要に応じてコメントを追加し、 **[保存]** を選択してインシデントを更新し、完了します。

1. *[Attack story] (攻撃ストーリー)、[アラート]、[資産]、[調査]、[Evidence and Response] (証拠と応答)* 、および *[概要]* タブの内容を確認します。 "デバイスとユーザー" は "アセット" タブにあります。** 実際のインシデントでは、"攻撃ストーリー" タブに "インシデント グラフ" が表示されます。**** **ヒント:** 一部のタブは、ディスプレイのサイズが原因で非表示になる場合があります。 省略記号タブ (...) を選択して表示します。

<!---    >**Warning:** The simulated attacks here are an excellent source of learning through practice. Only perform the attacks in the instructions provided for this lab when using the course provided Azure tenant.  You may perform other simulated attacks *after* this training course is complete with this tenant. --->

## これでラボは完了です
