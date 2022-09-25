---
lab:
  title: 演習 1 - Microsoft Sentinel で脅威ハンティングを実行する
  module: Module 8 - Perform threat hunting in Microsoft Sentinel
---

# <a name="module-8---lab-1---exercise-1---perform-threat-hunting-in-microsoft-sentinel"></a>モジュール 8 - ラボ 1 - 演習 1 - Microsoft Sentinel で脅威ハンティングを実行する

## <a name="lab-scenario"></a>ラボのシナリオ

![ラボの概要。](../Media/SC-200-Lab_Diagrams_Mod8_L1_Ex1.png)

You are a Security Operations Analyst working at a company that implemented Microsoft Sentinel. You have received threat intelligence about a Command and Control (C2 or C&amp;C) technique. You need to perform a hunt and watch for the threat.

><bpt id="p1">**</bpt>Important:<ept id="p1">**</ept> The log data used in the lab was created in the previous module. See <bpt id="p1">**</bpt>Attack 3<ept id="p1">**</ept> on WIN1 server in Exercise 5.

>**注:**  前のモジュールでデータを探索するプロセスを既に経験しているため、このラボでは最初に KQL ステートメントが提供されます。 


### <a name="task-1-create-a-hunting-query"></a>タスク 1:ハンティング クエリの作成

このタスクでは、捜索クエリを作成し、結果をブックマークして、ライブ ストリームを作成します。

1. 管理者として WIN1 仮想マシンにログインします。パスワードは**Pa55w.rd**。  

1. Edge ブラウザーで、Azure portal (https://portal.azure.com ) に移動します。

1. **[サインイン]** ダイアログ ボックスで、ラボ ホスティング プロバイダーから提供された**テナントの電子メール** アカウントをコピーして貼り付け、 **[次へ]** を選択します。

1. **[パスワードの入力]** ダイアログ ボックスで、ラボ ホスティング プロバイダーから提供された**テナントのパスワード**をコピーして貼り付け、 **[サインイン]** を選択します。

1. Azure portal の検索バーに「*Sentinel*」と入力し、**[Microsoft Sentinel]** を選択します。

1. Microsoft Sentinel ワークスペースを選択します。

1. **[ログ]** を選択します。 

1. *[新しいクエリ 1]* スペースに以下の KQL ステートメントを入力します。

   >**重要:** 最初に KQL クエリをメモ帳に貼り付けて、そこから *[新しいクエリ 1]* ログ ウィンドウにコピーしてエラーを回避してください。

    ```KQL
    let lookback = 2d;
    DeviceEvents | where TimeGenerated >= ago(lookback) 
    | where ActionType == "DnsQueryResponse"
    | extend c2 = substring(tostring(AdditionalFields.DnsQueryString),0,indexof(tostring(AdditionalFields.DnsQueryString),"."))
    | where c2 startswith "sub"
    | summarize count() by bin(TimeGenerated, 3m), c2
    | where count_ > 5
    | render timechart 
    ```

    ![Screenshot](../Media/SC200_hunting1.png)

1. The goal of the previous KQL query is to provide a visualization for a C2 beaconing on a consistent basis. Adjust grouping of values by changing the <bpt id="p1">*</bpt>3m<ept id="p1">*</ept> setting to <bpt id="p2">**</bpt>30s<ept id="p2">**</ept> within bin() and <bpt id="p3">**</bpt>Run<ept id="p3">**</ept> the query again.

1. Change it back to <bpt id="p1">*</bpt>3m<ept id="p1">*</ept>. Now change the <bpt id="p1">*</bpt>count_<ept id="p1">*</ept> threshold to <bpt id="p2">**</bpt>10<ept id="p2">**</ept> and <bpt id="p3">**</bpt>Run<ept id="p3">**</ept> the query again to witness the impact.

1. You have now identified DNS requests that are beaconing to a C2 server. Next, determine which devices are beaconing. <bpt id="p1">**</bpt>Run<ept id="p1">**</ept> the following KQL Statement:

    ```KQL
    let lookback = 2d;
    DeviceEvents | where TimeGenerated >= ago(lookback) 
    | where ActionType == "DnsQueryResponse"
    | extend c2 = substring(tostring(AdditionalFields.DnsQueryString),0,indexof(tostring(AdditionalFields.DnsQueryString),".")) 
    | where c2 startswith "sub"
    | summarize cnt=count() by bin(TimeGenerated, 5m), c2, DeviceName
    | where cnt > 15
    ```

    ![Screenshot](../Media/SC200_hunting2.png)

    >**注:**  生成されるログ データは、WIN1 デバイスからのもののみです。

1. ウィンドウの右上にある **[X]** を選択して *[ログ]* ウィンドウを閉じ、 **[OK]** を選択して変更を破棄します。 

1. Microsoft Sentinel ワークスペースをもう一度選択し、[脅威の管理] 領域で **[ハンティング]** ページを選択します。

1. コマンド バーで **[+ 新しいクリエ**] を選択します。

1. *[カスタム クエリの作成]* ウィンドウで、*[名前]* に「**C2 Hunt**」と入力します

1. *カスタム クエリ*には、次の KQL ステートメントを入力します。

    ```KQL
    let lookback = 2d;
    DeviceEvents | where TimeGenerated >= ago(lookback) 
    | where ActionType == "DnsQueryResponse"
    | extend c2 = substring(tostring(AdditionalFields.DnsQueryString),0,indexof(tostring(AdditionalFields.DnsQueryString),"."))
    | where c2 startswith "sub"
    | summarize cnt=count() by bin(TimeGenerated, 5m), c2, DeviceName
    | where cnt > 15
    ```

1. 下にスクロールし、*[エンティティ マッピング (プレビュー)]* で次のように選択します。

    - *[エンティティの種類]* ドロップダウン リストで、**[ホスト]** を選択します。
    - *[識別子]* ドロップダウン リストで、**[HostName]** を選択します。
    - *[値]* ドロップダウン リストで、**[DeviceName]** を選択します。

1. 下にスクロールし、*[戦術と手法]* で **[コマンドと制御]** を選び、**[作成]** を選択してハンティング クエリを作成します。

1. *[Microsoft Sentinel - ハンティング]* ブレードで、先ほど作成したクエリ *C2 Hunt* をリストで探します。

1. リストから **[C2 Hunt]** を選択します。

1. 右ペインで下にスクロールし、**[クエリの実行]** ボタンを選択します。

1. あなたは、Microsoft Sentinel を実装した会社で働いているセキュリティ運用アナリストです。

1. コマンドと制御 (C2 または C&C) 手法に関する脅威インテリジェンスを受け取りました。

1. 結果の最初の行のチェックボックスをオンにします。 

1. 中央のコマンド バーで、**[ブックマークの追加]** ボタンを選択します。

1. 既定で設定されている値を確認し、*[ブックマークの追加]* ブレードで **[作成]** を選択します。

1. ウィンドウの右上にある **[X]** を選択して *[ログ]* ウィンドウを閉じ、**[OK]** を選択して変更を破棄します。 

1. Microsoft Sentinel ポータルの [ハンティング] ページに戻り、中央のペインで **[ブックマーク]** タブを選択します。

1. 結果リストから、先ほど作成した **C2 Hunt** ブックマークを選択します。

1. その脅威に対して捜索とウォッチを実行する必要があります。

1. 前のモジュールで行ったのと同じように調査グラフを調べます。

1. ウィンドウの右上にある **[X]** を選択して *[調査]* グラフ ウィンドウを閉じ、**[OK]** を選択して変更を破棄します。 

1. **[クエリ]** タブを選択します。

1. もう一度 **C2 Hunt** クエリを探して選択します。

1. Right-click your query and select <bpt id="p1">**</bpt>Add to livestream<ept id="p1">**</ept>. <bpt id="p1">**</bpt>Hint:<ept id="p1">**</ept> This also can be done by sliding right and selecting the ellipsis <bpt id="p2">**</bpt>(...)<ept id="p2">**</ept> at the end of the row to open a context menu.

1. **重要:** このラボで使用されるログ データは、前のモジュールで作成されたものです。


### <a name="task-2-create-a-nrt-query-rule"></a>タスク 2:NRT クエリ ルールを作成する

演習 5 の WIN1 サーバーの**攻撃 3** を参照してください。


1. Microsoft Sentinel で **[分析]** ページを選択します。 

1. **[作成]** タブを選択し、 **[NRT クエリ ルール]** を選択します
1. This starts the "Analytics rule wizard". For the <bpt id="p1">*</bpt>General<ept id="p1">*</ept> tab type:

    |設定|[値]|
    |---|---|
    |名前|**NRT C2 ハント**|
    |説明|**NRT C2 ハント**|
    |方針|**コマンドとコントロール**|
    |Severity|**高**|

1. **[次へ: ルール ロジックを設定]** ボタンを選択します。 


1. *[ルール クエリ]* に次の KQL ステートメントを入力します。

    ```KQL
    DeviceEvents | where TimeGenerated >= ago(lookback) 
    | where ActionType == "DnsQueryResponse"
    | extend c2 = substring(tostring(AdditionalFields.DnsQueryString),0,indexof(tostring(AdditionalFields.DnsQueryString),"."))
    | where c2 startswith "sub"
    | summarize cnt=count() by bin(TimeGenerated, 5m), c2, DeviceName
    | where cnt > 15
    ```

><bpt id="p1">**</bpt>Note:<ept id="p1">**</ept> We are purposely generating many incidents for the same data. This enables the Lab to use these alerts.

1. Leave the rest of the options with the defaults. Select <bpt id="p1">**</bpt>Next: Incident settings&gt;<ept id="p1">**</ept> button.

1. *[インシデント設定]* タブについては、既定値のままにし、 **[次へ: 自動応答 >]** ボタンを選択します。

1. *[自動応答]* タブでは、 *[アラートの自動化]* で **[PostMessageTeams-OnAlert]** を選んでから、 **[次へ: Review]\(次へ: 確認\)** をクリックします。

1. *[確認]* タブで、 **[作成]** ボタンを選択して新しいスケジュール化された分析ルールを作成します。



### <a name="task-3-create-a-search"></a>タスク 3:検索の作成

このタスクでは、検索ジョブを使用して C2 を検索します。 


1. Microsoft Sentinel で **[検索]** ページを選択します。 

1. **[復元]** タブを選択します。

><bpt id="p1">**</bpt>Note:<ept id="p1">**</ept> The lab will not have Archived tables to restore from.  The normal process would restore archived tables to include in the Search job.
1. **[キャンセル]** を選択します。
1. **[検索]** タブを選択します。
1. *Table* を選択し、**DeviceRegistryEvents** に変更します
1. 検索ボックスに「**reg.exe**」と入力します。  
1. **[保存した検索]** を選択します。 
1. 検索ジョブにより、**DeviceRegistryEvents_####_SRCH** という名前の新しいテーブルが作成されます。 
1. Wait for the search job to complete.  The status will display <bpt id="p1">*</bpt>Updating<ept id="p1">*</ept>. Then <bpt id="p1">*</bpt>In progress<ept id="p1">*</ept>. Then <bpt id="p1">*</bpt>Search completed<ept id="p1">*</ept>. 
1. **[検索結果の表示]** を選択します。
1. *[ログ]* で新しいタブを開きます。
1. 新しいテーブル名 **DeviceRegistryEvents_####_SRCH** を入力して実行します。

## <a name="proceed-to-exercise-2"></a>演習 2 に進みます。
