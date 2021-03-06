---
lab:
  title: 演習 2 - Microsoft Sentinel でのノートブックを使用した脅威ハンティング
  module: Module 8 - Perform threat hunting in Microsoft Sentinel
ms.openlocfilehash: 27db8985c2581a04345396e47ee0f0d2e97eb931
ms.sourcegitcommit: a90325f86a3497319b3dc15ccf49e0396c4bf749
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/07/2022
ms.locfileid: "141493954"
---
# <a name="module-8---lab-1---exercise-2---threat-hunting-using-notebooks-with-microsoft-sentinel"></a>モジュール 8 - ラボ 1 - 演習 2 - Microsoft Sentinel でのノートブックを使用した脅威ハンティング

## <a name="lab-scenario"></a>ラボのシナリオ



あなたは、Microsoft Sentinel を実装した会社で働いているセキュリティ運用アナリストです。 Microsoft Sentinel Notebooks を使った脅威ハンティングの利点を調査する必要があります。 Notebooks は次の用途に使用できます。

- 一部の Python 機械学習機能など、Microsoft Sentinel 何もしないと提供されない分析を実行します。
- カスタムのタイムラインやプロセス ツリーなど、Microsoft Sentinel で何もしないと提供されないデータ視覚化を作成します。
- オンプレミスのデータ セットなど、Microsoft Sentinel の外部にあるデータ ソースを統合する


### <a name="task-1-explore-notebooks"></a>タスク 1:ノートブックの探索

このタスクでは、Microsoft Sentinel でノートブックを使用する方法について説明します。

1. 管理者として WIN1 仮想マシンにログインします。パスワードは **Pa55w.rd**。  

1. Edge ブラウザーで、Azure portal (https://portal.azure.com ) に移動します。

1. **[サインイン]** ダイアログ ボックスで、ラボ ホスティング プロバイダーから提供された **テナントの電子メール** アカウントをコピーして貼り付け、 **[次へ]** を選択します。

1. **[パスワードの入力]** ダイアログ ボックスで、ラボ ホスティング プロバイダーから提供された **テナントのパスワード** をコピーして貼り付け、 **[サインイン]** を選択します。

1. Azure portal の検索バーに「*Sentinel*」と入力してから、 **[Microsoft Sentinel]** を選択します。

1. Microsoft Sentinel ワークスペースを選択します。

1. Microsoft Sentinel ワークスペースで、 **[Notebooks]** を選択します。

1. 次に、AzureML ワークスペースを作成する必要があります。 **[Azure Machine Learning の構成]** を選択し、コマンド バーの **[新しい Azure ML ワークスペースの作成]** ボタンを選択します。

1. [サブスクリプション] ボックスでお使いのサブスクリプションを選択します。

1. リソース グループの **[新規作成]** を選択し、名前として「*RG-MachineLearning*」と入力して、 **[OK]** を選択します。 

1. ワークスペースの詳細 セクションで次の作業を行います。

     - お使いのワークスペースに一意の名前を付けます。
     - *[リージョン]* の既定値は **[(米国) 米国東部]** のままにします。
     - 既定のストレージ アカウント、キーボールト、およびアプリケーション インサイト情報を保持します。
     - 「コンテナー レジストリ」オプションは、「**なし**」のままにできます。

1. ページの下部で **[確認および作成]** を選択します。 *検証に成功しました* というメッセージが表示されたら、 **[作成]** を選択します。 

     >**注:**  Machine Learning ワークスペースのデプロイには数分かかる場合があります。

1. *デプロイが完了しました* というメッセージが表示されたら、Microsoft Sentinel ポータルに戻ります。

1. **[Notebooks]** を選択し、中央のコマンド バーから **[テンプレート]** タブを選択します。 

1. **[Microsoft Sentinel ML ノートブックのファースト ステップ ガイド]** を選択します。 

1. 右側のペインで、下にスクロールし、 **[ノートブック テンプレートの複製]** ボタンを選択します。 既定のオプションを確認し、 **[保存]** を選択します。

1. 保存が完了したら、 **[ノートブックの起動]** ボタンを選択します。 これにより Microsoft Azure Machine Learning スタジオに移動します。

1. Microsoft Azure Machine Learning スタジオで情報ウィンドウが表示されたら、 **[閉じる]** を選択します。

1. コマンド バーの **[コンピューティング]** インスタンス セレクターの右側にある **[+]** 記号を選択して、新しいコンピューティング インスタンスを作成します。

1. *[コンピューティング名]* フィールドに一意の名前を入力します。 これにより、コンピューティング インスタンスが識別されます。

1. 下にスクロールし、使用可能な最初のオプションを選択します。 **ヒント:** ワークロードの種類:Notebooks での開発と軽量テスト。

1. 画面の下部にある **[作成]** ボタンを選択します。 表示される可能性のあるフィードバック ウィンドウをすべて閉じます。 これには数分かかり、完了すると通知 (ベル アイコン) が表示されます。

1. コンピューティングが作成されて実行されたら、使用するカーネルが *Python 3.8 - AzureML* であることを確認します。 **ヒント:** これは、コマンド バーの右側に表示されます。 *[Notebooks]* メニューの下の **[<<]** を選択して、画面のサイズを大きくすることもできます。

1. コマンド バーの **消しゴム** アイコンを選んで、ノートブックのすべての結果をクリアし、*作業の開始* のチュートリアルに従います。

>**注:**  上記の手順を完了してノートブックにアクセスできない場合、代わりにその GitHub ページの手順に従うことができます。 ノートブックファイルをここでご覧ください:[GitHub の Microsoft Sentinel Notebooks](https://github.com/Azure/Azure-Sentinel-Notebooks/blob/8122bca32387d60a8ee9c058ead9d3ab8f4d61e6/A%20Getting%20Started%20Guide%20For%20Azure%20Sentinel%20ML%20Notebooks.ipynb) 

## <a name="you-have-completed-the-lab"></a>これでラボは完了です。
