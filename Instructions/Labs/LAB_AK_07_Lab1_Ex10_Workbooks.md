---
lab:
  title: 演習 10 - ブックを作成する
  module: Module 7 - Create detections and perform investigations using Microsoft Sentinel
---

# <a name="module-7---lab-1---exercise-10---create-workbooks"></a>モジュール 7 - ラボ 1 - 演習 10 - ワークブックの作成

## <a name="lab-scenario"></a>ラボのシナリオ

![ラボの概要。](../Media/SC-200-Lab_Diagrams_Mod7_L1_Ex8.png)

You are a Security Operations Analyst working at a company that implemented Microsoft Sentinel. Once you have connected your data sources to Microsoft Sentinel, you can visualize and monitor the data using the Microsoft Sentinel adoption of Azure Monitor Workbooks, which provides versatility in creating custom dashboards. 

Microsoft Sentinel を使用すると、データ全体に対してカスタム ブックを作成できます。また、用意されている組み込みのブック テンプレートを使用してデータ ソースに接続すると、すぐにデータ全体の分析情報をすばやく得ることもできます。


### <a name="task-1-explore-workbook-templates"></a>タスク 1:ブック テンプレートを調べる

このタスクでは、Microsoft Sentinel ブック テンプレートを調べます。

1. 管理者として WIN1 仮想マシンにログインします。パスワードは**Pa55w.rd**。  

1. Edge ブラウザーで、Azure portal (https://portal.azure.com ) に移動します。

1. **[サインイン]** ダイアログ ボックスで、ラボ ホスティング プロバイダーから提供された**テナントの電子メール** アカウントをコピーして貼り付け、 **[次へ]** を選択します。

1. **[パスワードの入力]** ダイアログ ボックスで、ラボ ホスティング プロバイダーから提供された**テナントのパスワード**をコピーして貼り付け、 **[サインイン]** を選択します。

1. Azure portal の検索バーに「*Sentinel*」と入力し、**[Microsoft Sentinel]** を選択します。

1. Microsoft Sentinel ワークスペースを選択します。

1. Select <bpt id="p1">**</bpt>Workbooks<ept id="p1">**</ept>. The <bpt id="p1">*</bpt>Templates<ept id="p1">*</ept> tab is selected by default.

1. Search for and select the <bpt id="p1">**</bpt>Identity &amp; Access<ept id="p1">**</ept> template workbook. In the right pane, scroll down and select the <bpt id="p1">**</bpt>View template<ept id="p1">**</ept> button.

1. Review the contents of the workbook. It shows insights into Identity and access operations by collecting and analyzing security logs, using the audit and sign-in logs to gather insights into use of Microsoft products.

1. 右上隅にある **[X]** を選択してブックを閉じます。


### <a name="task-2-save-and-modify-a-workbook-template"></a>タスク 2:ブック テンプレートを保存して変更する

このタスクでは、ブック テンプレートを保存して変更します。

1. **[Microsoft Sentinel - ブック - テンプレート]** タブに戻る必要があります。 **[Azure AD 監査ログ]** を検索して選択し、右側のペインで下にスクロールし、 **[保存]** ボタンを選択します。 

1. *[リージョン]* の既定値は **[米国東部]** のままにして、 **[OK]** を選択します。

1. **[保存されたワークブックの表示]** ボタンを選択します。

1. コマンド バーで **[編集]** を選択して、ブックの変更を有効にします。

1. Read the banner that informs you of a new feature to compare workbooks. Dismiss the message by selecting the banner.

1. あなたは、Microsoft Sentinel を実装した会社で働いているセキュリティ運用アナリストです。

1. Microsoft Sentinel にデータ ソースを接続した後、Microsoft Sentinel による Azure Monitor ブックの適用を使用して、データを視覚化および監視できます。これにより、多用途のカスタム ダッシュボードを作成できます。

1. 表示された [*列の設定の編集*] ウィンドウの [*列*] 内で、 **[操作数 (ヒートマップ + 書式付き)]** を選択します。

1. Review the settings, in particular the options for <bpt id="p1">*</bpt>Column renderer<ept id="p1">*</ept>. For <bpt id="p1">*</bpt>Color palette<ept id="p1">*</ept>, select <bpt id="p2">**</bpt>32-color categorical<ept id="p2">**</ept>.

1. [*列*] 内で、 **[傾向 (スパーク ライン + 書式付き)]** を選択します。

1. 設定を確認し、[*列レンダラー*] で **[Spark 領域]** を選択し、[*カラー パレット*] で好みの色を選択します。

1. Select <bpt id="p1">**</bpt>Save and Close<ept id="p1">**</ept>. Now we are going to review how one tile/grid control can be used to filter the results in another tile/grid.

1. [*クエリ項目の編集: クエリ - 2*] のコマンド バーで **[詳細設定]** を選択します。

1. Review the <bpt id="p1">*</bpt>When items are selected, export parameters<ept id="p1">*</ept> setting. Notice the <bpt id="p1">*</bpt>UserInfo<ept id="p1">*</ept> field is selected.

1. Scroll down and select <bpt id="p1">**</bpt>Done Editing<ept id="p1">**</ept> at the bottom of the query (not the top menu). Look at the changed colors for <bpt id="p1">*</bpt>Operations count<ept id="p1">*</ept> and <bpt id="p2">*</bpt>Trend<ept id="p2">*</ept>.

1. 画面の右側に表示された円グラフ *上位アクティブ ユーザー* の下にある **[編集]** を選択します。  

1. In the <bpt id="p1">*</bpt>Logs query<ept id="p1">*</ept>, locate <bpt id="p2">*</bpt>UserInfo<ept id="p2">*</ept>. The query is using the parameter exported from the other query to filter results.

1. 下にスクロールし、(上部のメニューではなく) クエリの下部にある **[編集完了]** を選択します。

1. Scroll up and select <bpt id="p1">**</bpt>Done Editing<ept id="p1">**</ept> at the top menu and select the <bpt id="p2">**</bpt>Save<ept id="p2">**</ept> icon. Close the workbook by selecting the <bpt id="p1">**</bpt>X<ept id="p1">**</ept> in the top-right corner.


### <a name="task-3-create-a-workbook"></a>タスク 3:ブックを作成する

このタスクでは、高度な視覚化を備えた新しいワークブックを作成します。

1. Microsoft Sentinel ポータルの **ブック** 領域に戻る必要があります。

1. **[+ ブックの追加]** を選択して、新しいブックを最初から作成します。 

    >**注:**  これは新しいブックですが、スタートアップ テンプレートを使用します。

1. ブックを編集するには、 **[編集]** を選択します。

1. ブックの最初の段落の下にある **[編集]** ボタンを選択します。 

1. *[## 新しいブック]* の上に「*# マイブック*」とを入力します。

1. Select <bpt id="p1">**</bpt>Done Editing<ept id="p1">**</ept> on the bottom menu, for the <bpt id="p2">*</bpt>Editing text item: text - 2<ept id="p2">*</ept>. Notice that your header increased size and name changed.

1. 唯一表示されている横棒グラフの下にある **[編集]** を選択します。

1. すべてのテーブル全体のカウントの *union* ステートメントを提供する KQL ステートメントを確認します。

1. [*クエリ項目の編集: クエリ - 2*] では、下にスクロールし、下部のメニューにある **[編集完了]** を選択します。

1. 横棒グラフの [*編集*] ボタンの横にある省略記号 **[...]** を選択し、 **[+ 追加]** 、 **[クエリの追加]** の順に選択します。

1. クエリ ボックスに、「**SecurityEvent**」と入力します。

1. *[時間の範囲]* を **[過去 4 時間]** に変更します。

1. *[視覚化]* を **[時間グラフ]** に変更します。

1. クエリのコマンド バーから **[スタイル]** を選択します。

1. **[この項目をカスタム幅にする]** ボックスを選択します。

1. *[パーセント幅]* を **[25]** に、 *[最大幅]* を **[25]** に設定します。

1. 次に、クエリのコマンド バーから **[詳細設定]** を選択します。

1. **[編集していないときに更新アイコンを表示する]** ボックスを選択します。 

1. 新しい *[クエリ項目の編集: クエリ - 2]* の場合は、下にスクロールし、下部のメニューにある **[編集完了]** を選択します。

1. 下にスクロールし、ブックの下部で **[+ 追加]** 、 **[クエリの追加]** の順に選択します。

1. クエリ ボックスに、「**SecurityEvent**」と入力します。

1. *[時間の範囲]* を **[過去 4 時間]** に変更します。

1. *[視覚化]* を **[グリッド]** に変更します。

1. クエリのコマンド バーから **[スタイル]** を選択します。

1. **[この項目をカスタム幅にする]** ボックスを選択します。

1. *[パーセント幅]* を **[75]** に、 *[最大幅]* を **[75]** に設定します。

1. 新しい *[クエリ項目の編集: クエリ - 3]* では、下にスクロールし、下部のメニューにある **[編集完了]** を選択します。

1. ブックのコマンド バーで **[編集完了]** を選択します。

1. Select the <bpt id="p1">**</bpt>Save<ept id="p1">**</ept> icon, change the <bpt id="p2">*</bpt>Title<ept id="p2">*</ept> to <bpt id="p3">**</bpt>My Workbook<ept id="p3">**</ept> and leave other values as default. Select <bpt id="p1">**</bpt>Save<ept id="p1">**</ept> again to commit the changes. 

1. 右上の **[X]** を選択するか、Microsoft Sentinel ポータルで **[ブック]** を選択して、ブックを閉じます。

1. *[ブック]* ページに戻り、 **[マイ ブック]** タブを選択します。

1. 作成したばかりのブック **My Workbook** を選択します。

1. 右側のペインで、 **[保存されたブックの表示]** を選択してブックを確認します。

## <a name="proceed-to-exercise-11"></a>演習 11 に進む
