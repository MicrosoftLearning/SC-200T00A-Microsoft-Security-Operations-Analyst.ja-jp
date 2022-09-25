# <a name="module-4-create-queries-for-microsoft-sentinel-using-kusto-query-language-kql"></a>モジュール 4 Kusto 照会言語 (KQL) を使用して Microsoft Sentinel のクエリを作成する

**注**: このデモを正常に完了するには、[前提条件ドキュメント](00-prerequisites.md)のすべての手順を完了する必要があります。 

## <a name="access-the-kql-testing-area"></a>KQLテストエリアにアクセスします。

このタスクでは、KQLステートメントの記述を練習できるLog Analytics環境にアクセスします。

1. 管理者として WIN1 仮想マシンにログインします。パスワードは**Pa55w.rd**。  

2. Go to <ph id="ph1">https://aka.ms/lademo</ph> in your browser. Login with the MOD Administrator credentials. 

3. 画面左側のタブのリストから使用可能なテーブルを調べます。

4. In the query editor, enter the following query and select the Run button.  You should see the query results in the bottom window.

    ```KQL
    SecurityEvent
    ```

5. 最初のレコードの横にある **[>]** を選択して、行の情報を展開します。

### <a name="task-2-run-basic-kql-statements"></a>タスク 2:基本的なKQL ステートメントを実行する

このタスクでは 基本的なKQL ステートメントを作成します。

1. The following statement demonstrates the use of the let statement to declare variables. In the Query Window, enter the following statement and select <bpt id="p1">**</bpt>run<ept id="p1">**</ept>: 


```KQL
let timeOffset = 7d;
let discardEventId = 4688;
SecurityEvent
| where TimeGenerated > ago(timeOffset*2) and TimeGenerated < ago(timeOffset)
| where EventID != discardEventId
```

1. The following statement demonstrates the use of the let statement to declare a dynamic list. In the Query Window enter the following statement and select <bpt id="p1">**</bpt>run<ept id="p1">**</ept>: 


```KQL
let suspiciousAccounts = datatable(account: string) [
    @"\administrator", 
    @"NT AUTHORITY\SYSTEM"
];
SecurityEvent | where Account in (suspiciousAccounts)
```

1. The following statement demonstrates searching across all tables and columns for records within the query time range display in the query window. In the Query Window before running this script change the Time range to "Last hour". Enter the following statement and select <bpt id="p1">**</bpt>run<ept id="p1">**</ept>: 

```KQL
search "err"
```

**警告:** 次のスクリプトのために、必ず時間範囲を "過去 24 時間" に戻してください。

### <a name="create-visualizations-in-kql-with-the-render-operator"></a>レンダー演算子を使用してKQLでビジュアライゼーションを作成します

このタスクでは,KQLステートメントを使用した視覚化の生成を使用します

1. The following statement demonstrates the render function visualizing results with a barchart. In the Query Window. Enter the following statement and select <bpt id="p1">**</bpt>run<ept id="p1">**</ept>: 

```KQL
SecurityEvent 
| summarize count() by Account
| render barchart
```

2. 次のステートメントは、時系列で結果を視覚化するレンダリング関数を示しています。

ブラウザーで https://aka.ms/lademo にアクセスします。 

```KQL
SecurityEvent 
| summarize count() by bin(TimeGenerated, 1d) 
| render timechart
```

## <a name="you-have-completed-the-demo"></a>デモが完了しました。

