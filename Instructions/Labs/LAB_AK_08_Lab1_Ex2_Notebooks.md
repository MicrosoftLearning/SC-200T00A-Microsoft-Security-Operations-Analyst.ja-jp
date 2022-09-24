---
lab:
  title: 演習 2 - Microsoft Sentinel でのノートブックを使用した脅威ハンティング
  module: Module 8 - Perform threat hunting in Microsoft Sentinel
---

# <a name="module-8---lab-1---exercise-2---threat-hunting-using-notebooks-with-microsoft-sentinel"></a>モジュール 8 - ラボ 1 - 演習 2 - Microsoft Sentinel でのノートブックを使用した脅威ハンティング

## <a name="lab-scenario"></a>ラボのシナリオ



You are a Security Operations Analyst working at a company that implemented Microsoft Sentinel. You need to explore the benefits of threat hunting with Microsoft Sentinel Notebooks. You can use notebooks to:

- 一部の Python 機械学習機能など、Microsoft Sentinel 何もしないと提供されない分析を実行します。
- カスタムのタイムラインやプロセス ツリーなど、Microsoft Sentinel で何もしないと提供されないデータ視覚化を作成します。
- オンプレミスのデータ セットなど、Microsoft Sentinel の外部にあるデータ ソースを統合する


### <a name="task-1-explore-notebooks"></a>タスク 1:ノートブックの探索

このタスクでは、Microsoft Sentinel でノートブックを使用する方法について説明します。

1. 管理者として WIN1 仮想マシンにログインします。パスワードは**Pa55w.rd**。  

1. Edge ブラウザーで、Azure portal (https://portal.azure.com ) に移動します。

1. **[サインイン]** ダイアログ ボックスで、ラボ ホスティング プロバイダーから提供された**テナントの電子メール** アカウントをコピーして貼り付け、 **[次へ]** を選択します。

1. **[パスワードの入力]** ダイアログ ボックスで、ラボ ホスティング プロバイダーから提供された**テナントのパスワード**をコピーして貼り付け、 **[サインイン]** を選択します。

1. Azure portal の検索バーに「*Sentinel*」と入力し、**[Microsoft Sentinel]** を選択します。

1. Microsoft Sentinel ワークスペースを選択します。

1. Microsoft Sentinel ワークスペースで、**[Notebooks]** を選択します。

1. Next, you need to create an AzureML Workspace. Select <bpt id="p1">**</bpt>Configure Azure Machine Learning<ept id="p1">**</ept> and then select <bpt id="p2">**</bpt>Create new Azure ML workspace<ept id="p2">**</ept> button in the command bar.

1. [サブスクリプション] ボックスでお使いのサブスクリプションを選択します。

1. リソース グループの **[新規作成]** を選択し、名前として「*RG-MachineLearning*」と入力して、**[OK]** を選択します。 

1. ワークスペースの詳細 セクションで次の作業を行います。

     - お使いのワークスペースに一意の名前を付けます。
     - *[リージョン]* の既定値は **[米国東部]** のままにします。
     - 既定のストレージ アカウント、キーボールト、およびアプリケーション インサイト情報を保持します。
     - [コンテナー レジストリ] オプションは、**[なし]** のままにできます。

1. At the bottom of the page, select <bpt id="p1">**</bpt>Review + create<ept id="p1">**</ept>. When you see the <bpt id="p1">*</bpt>"Validation passed"<ept id="p1">*</ept> message, select <bpt id="p2">**</bpt>Create<ept id="p2">**</ept>. 

     >**注:**  Machine Learning ワークスペースのデプロイには数分かかる場合があります。

1. *デプロイが完了しました* というメッセージが表示されたら、Microsoft Sentinel ポータルに戻ります。

1. **[Notebooks]** を選択し、中央のコマンド バーから **[テンプレート]** タブを選択します。 

1. **[Microsoft Sentinel ML ノートブックのファースト ステップ ガイド]** を選択します。 

1. On the right pane, scroll down and select <bpt id="p1">**</bpt>Create from template<ept id="p1">**</ept> button. Review the default option and select <bpt id="p1">**</bpt>Save<ept id="p1">**</ept>.

1. あなたは、Microsoft Sentinel を実装した会社で働いているセキュリティ運用アナリストです。

1. Microsoft Azure Machine Learning スタジオで情報ウィンドウが表示されたら、**[閉じる]** を選択します。

1. コマンド バーの **[コンピューティング]** インスタンス セレクターの右側にある **[+]** 記号を選択して、新しいコンピューティング インスタンスを作成します。

1. Microsoft Sentinel Notebooks を使った脅威ハンティングの利点を調査する必要があります。

1. Notebooks は次の用途に使用できます。

1. Select the <bpt id="p1">**</bpt>Create<ept id="p1">**</ept> button at the bottom of the screen. Close any feedback window that may appear. This will take a few minutes, you will see a notification (bell icon) when it is done.

1. Once the Compute has been created and running, verify that the kernel to use is <bpt id="p1">*</bpt>Python 3.8 - AzureML<ept id="p1">*</ept>. <bpt id="p1">**</bpt>Hint:<ept id="p1">**</ept> This is shown in the right of the command bar. You can also increase your screen size by selecting <bpt id="p1">**</bpt><ph id="ph1">&lt;&lt;</ph><ept id="p1">**</ept> under the <bpt id="p2">*</bpt>Notebooks<ept id="p2">*</ept> menu.

1. コマンド バーの**消しゴム** アイコンを選んで、ノートブックのすべての結果をクリアし、*作業の開始* のチュートリアルに従います。

><bpt id="p1">**</bpt>Note:<ept id="p1">**</ept> If you cannot complete the steps above to access the Notebook, you can follow it on its GitHub page instead. See the notebook file here: <bpt id="p1">[</bpt>Microsoft Sentinel Notebooks on GitHub<ept id="p1">](https://github.com/Azure/Azure-Sentinel-Notebooks/blob/8122bca32387d60a8ee9c058ead9d3ab8f4d61e6/A%20Getting%20Started%20Guide%20For%20Azure%20Sentinel%20ML%20Notebooks.ipynb)</ept> 

## <a name="you-have-completed-the-lab"></a>これでラボは完了です。
