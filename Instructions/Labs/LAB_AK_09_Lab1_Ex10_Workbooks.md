---
lab:
  title: 演習 10 - ブックを作成する
  module: Learning Path 9 - Create detections and perform investigations using Microsoft Sentinel
---

# ラーニング パス 9 - ラボ 1 - 演習 10 - ワークブックの作成

## ラボのシナリオ

![ラボの概要。](../Media/SC-200-Lab_Diagrams_Mod7_L1_Ex10.png)

あなたは、Microsoft Sentinel を実装した会社で働いているセキュリティ運用アナリストです。 Microsoft Sentinel にデータ ソースを接続した後、Microsoft Sentinel による Azure Monitor ブックの適用を使用して、データを視覚化および監視できます。これにより、多用途のカスタム ダッシュボードを作成できます。 

Microsoft Sentinel を使用すると、データ全体に対してカスタム ブックを作成できます。また、用意されている組み込みのブック テンプレートを使用してデータ ソースに接続すると、すぐにデータ全体の分析情報をすばやく得ることもできます。

>**重要:** ラーニング パス #9 のラボ演習は、*スタンドアロン*環境にあります。 ラボを完了せずに終了する場合は、構成を再実行する必要があります。

### このラボの推定所要時間: 30 分

### タスク 1:ブック テンプレートを調べる

このタスクでは、Microsoft Sentinel ブック テンプレートを調べます。

>**注:** Microsoft Sentinel は、**defenderWorkspace** という名前で Azure サブスクリプションに事前にデプロイされており、必要な *Content Hub* ソリューションがインストールされています。

1. 管理者として WIN1 仮想マシンにログインします。パスワードは**Pa55w.rd**。  

1. Edge ブラウザーで、Azure portal (<https://portal.azure.com> ) に移動します。

1. **[サインイン]** ダイアログ ボックスで、ラボ ホスティング プロバイダーから提供された**テナントの電子メール** アカウントをコピーして貼り付け、 **[次へ]** を選択します。

1. **[パスワードの入力]** ダイアログ ボックスで、ラボ ホスティング プロバイダーから提供された**テナントのパスワード**をコピーして貼り付け、 **[サインイン]** を選択します。

1. Azure portal の検索バーに「*Sentinel*」と入力してから、**[Microsoft Sentinel]** を選択します。

1. Microsoft Sentinel **defenderWorkspace** を選択します。

1. ナビゲーション メニューの *[脅威管理]* セクションの下で **[ブック]** を選択します。

1. *[テンプレート]* タブを選択し、**[Azure アクティビティ]** テンプレート ブックを検索して選択します。

1. 右側の詳細ウィンドウで下にスクロールし、 **[テンプレートの表示]** ボタンを選択します。

1. ブックの内容を確認します。 アクティビティ ログからデータを収集して分析し、Azure サブスクリプションの操作の分析情報が表示されます。

1. 右上隅にある **[X]** を選択してブックを閉じます。

### タスク 2:ブック テンプレートを保存して変更する

このタスクでは、ブック テンプレートを保存して変更します。

1. *[Azure アクティビティ]* ブックが選択されているままで、**[Microsoft Sentinel | ブック | テンプレート]** タブに戻っているはずです。

1. もう一度下にスクロールし、*[Azure アクティビティ]* ブックの詳細ウィンドウで **[保存]** ボタンを選択します。

1. *[リージョン]* の既定値は **[米国東部]** のままにして、 **[OK]** を選択します。

1. **[保存されたワークブックの表示]** ボタンを選択します。

1. コマンド バーで **[編集]** を選択して、ブックの変更を有効にします。

1. *[呼び出し元のアクティビティ]* 領域まで下にスクロールし、列を書式設定する、*[アクティビティ]* 列の色を見ます。 グリッドの下にある **[編集]** ボタンを選択します。

1. **[列の設定]** ボタンを選択します。これは、[*クエリの実行*] コマンド バーの右側にあります。 **ヒント:** このボタンは、KQL クエリからのデータがある場合のみ表示されます。

1. 表示された *[列の設定の編集]* ブレードの *[列]* 内で、 **[アクティビティ]** を選択します。

1. *[列レンダラー]* の値を **[ヒートマップ]** に変更します。 *[カラー パレット]* を下にスクロールして **[32 色のカテゴリ]** を選択します。

1. **[適用]** を選択して **[保存して閉じる]** を選択します。 *[アクティビティ]* 列の変更に注意してください。

1. (上部のメニューではなく) クエリの下部にある **[編集完了]** を選択します。

1. 上部のメニューにある **[編集完了]** を選択し、 **[保存]** アイコンを選択します。 

1. 右上隅にある **[X]** を選択してブックを閉じます。


### タスク 3:ブックを作成する

このタスクでは、高度な視覚化を備えた新しいワークブックを作成します。

1. Microsoft Sentinel ポータルの **ブック** 領域に戻る必要があります。

1. **[+ ブックの追加]** を選択して、新しいブックを最初から作成します。 

    >**注:**  これは新しいブックですが、スタートアップ テンプレートを使用します。

1. ブックを編集するには、 **[編集]** を選択します。

1. ブックの最初の段落の下にある **[編集]** ボタンを選択します。

1. *## New workbook* の上の新しい行に「 *# My workbook*」と入力します。

1. *[テキスト項目の編集: テキスト - 2]* のセクションの下部の **[編集完了]** を選択します。 ヘッダーのサイズが大きくなり、名前が変更されたことに注意してください。

1. 唯一表示されている横棒グラフの下にある **[編集]** を選択します。

1. すべてのテーブル全体のカウントの *union* ステートメントを提供する KQL ステートメントを確認します。

1. [*クエリ項目の編集: クエリ - 2*] では、下にスクロールし、下部のメニューにある **[編集完了]** を選択します。

1. 横棒グラフの [*編集*] ボタンの横にある省略記号 **[...]** を選択し、 **[+ 追加]** 、 **[クエリの追加]** の順に選択します。

1. クエリ ボックスに、「**SecurityEvent**」と入力します。

1. *[時間の範囲]* を「**過去 1 時間**」に変更します。

1. *[視覚化]* を **[時間グラフ]** に変更します。

1. クエリのコマンド バーから **[スタイル]** タブを選択します。

1. **[この項目をカスタム幅にする]** ボックスを選択します。

1. *[パーセント幅]* を **[25]** に、 *[最大幅]* を **[25]** に設定します。

1. 次に、クエリのコマンド バーから **[詳細設定]** タブを選択します。

1. **[編集していないときに更新アイコンを表示する]** ボックスを選択します。

1. 新しい *[クエリ項目の編集: クエリ - 2]* の場合は、下にスクロールし、下部のメニューにある **[編集完了]** を選択します。

1. 下にスクロールし、ブックの下部で **[+ 追加]** 、 **[クエリの追加]** の順に選択します。

1. クエリ ボックスに、「**SecurityEvent**」と入力します。

1. *[時間の範囲]* を「**過去 1 時間**」に変更します。

1. *[視覚化]* を **[グリッド]** に変更します。

1. クエリのコマンド バーから **[スタイル]** を選択します。

1. **[この項目をカスタム幅にする]** ボックスを選択します。

1. *[パーセント幅]* を **[75]** に、 *[最大幅]* を **[75]** に設定します。

1. 新しい *[クエリ項目の編集: クエリ - 3]* では、下にスクロールし、下部のメニューにある **[編集完了]** を選択します。

1. ブックの上部コマンド バーで **[編集完了]** を選択します。

1. **[保存]** アイコンを選択し、 *[タイトル]* を **My Workbook** に変更します。

1. 必要に応じて **RG-Defender** リソース グループを選択し、他の値は既定値のままにします。

1. **[適用]** を選択して変更をコミットします。 

1. 右上の **[X]** を選択するか、Microsoft Sentinel ポータルで **[ブック]** を選択して、ブックを閉じます。

1. *[ブック]* ページに戻り、 **[マイ ブック]** タブを選択します。

1. 作成したばかりのブック **My Workbook** を選択します。

1. 右側のペインで、 **[保存されたブックの表示]** を選択してブックを確認します。

## 演習 11 に進む
