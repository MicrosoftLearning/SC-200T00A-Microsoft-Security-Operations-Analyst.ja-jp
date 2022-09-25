# <a name="module-7---threat-hunting-in-microsoft-sentinel"></a>モジュール 7 - Microsoft Sentinel での脅威ハンティング

**注**: このデモを正常に完了するには、[前提条件ドキュメント](00-prerequisites.md)のすべての手順を完了する必要があります。 

## <a name="create-a-hunting-query"></a>ハンティング クエリの作成

このタスクでは、捜索クエリを作成し、結果をブックマークして、ライブ ストリームを作成します。

1. 管理者として WIN1 仮想マシンにログインします。パスワードは**Pa55w.rd**。  

1. Edge ブラウザーで、Azure portal (https://portal.azure.com ) に移動します。

1. **[サインイン]** ダイアログ ボックスで、ラボ ホスティング プロバイダーから提供された**テナントの電子メール** アカウントをコピーして貼り付け、 **[次へ]** を選択します。

1. **[パスワードの入力]** ダイアログ ボックスで、ラボ ホスティング プロバイダーから提供された**テナントのパスワード**をコピーして貼り付け、 **[サインイン]** を選択します。

1. Azure portal の検索バーに「*Sentinel*」と入力し、**[Microsoft Sentinel]** を選択します。

1. Microsoft Sentinel ワークスペースを選択します。

1. **[ログ]** を選択します。 

1. 新規クエリ1のスペースに以下のKQLステートメントを入力します。

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

1. The goal of this statement is to provide a visualization to check for a C2 beaconing out on a consistent basis.  Take time to adjust the 3m setting to 30s and more.  Change the count_ &gt; 5 setting to other threshold counts to witness the impact.

1. You have now identified DNS requests that are beaconing to a C2 server.  Next, determine which devices are beaconing.  Enter the following KQL Statement:

```KQL
let lookback = 2d;
DeviceEvents | where TimeGenerated >= ago(lookback) 
| where ActionType == "DnsQueryResponse"
| extend c2 = substring(tostring(AdditionalFields.DnsQueryString),0,indexof(tostring(AdditionalFields.DnsQueryString),".")) 
| where c2 startswith "sub"
| summarize cnt=count() by bin(TimeGenerated, 5m), c2, DeviceName
| where cnt > 15
```

**注:** 生成されるログ データは、オンボードされたデバイスからのもののみです。

1. ウィンドウの右上にある **[X]** を選択して *[ログ]* ウィンドウを閉じ、**[OK]** を選択して変更を破棄します。 

1. Microsoft Sentinel ポータルの脅威管理領域で **[ハンティング]** ページを選択します。

1. コマンド バーで **[新しいクリエ]** を選択します。

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

1. The number of results is shown in the middle pane under the <bpt id="p1">*</bpt>Results<ept id="p1">*</ept> column. Alternatively, scroll up to see the count over the <bpt id="p1">*</bpt>Results<ept id="p1">*</ept> box..

1. **[結果を表示]** を選択します。

1. 結果の最初の行を選択します。 

1. **[ブックマークの追加]** を選択します。

1. 表示されるペインで、**[作成]** を選択します。

1. Microsoft Sentinel ポータルの [ハンティング] ページに戻ります。

1. **[ブックマーク]** タブを選択します。

1. 結果の一覧で ブックマークを選択します。

1. フライアウトペインで、**[調査]** を選択します。

1. グラフを調査する

1. Microsoft Sentinel ポータルの [ハンティング] ページに戻ります。

1. **[クリエ]** タブを選択します

1. **[C2 Hunt]** クエリを選択します。

1. 行の最後にある **[...]** を選択して、コンテキスト メニューを開きます。

1. **[ライブストリームに追加]** を選択します。

## <a name="you-have-completed-the-demo"></a>デモが完了しました。