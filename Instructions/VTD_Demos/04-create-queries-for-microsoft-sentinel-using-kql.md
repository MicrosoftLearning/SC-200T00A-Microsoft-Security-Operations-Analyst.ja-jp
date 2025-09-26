# モジュール 4 Kusto 照会言語 (KQL) を使用して Microsoft Sentinel のクエリを作成する

<!--- **Note** Successful completion of this demo depends on completing all of the steps in the  [Pre-requisites document](00-prerequisites.md). --->

>**重要:** このラボのクエリは、Zava (以前の Alpine Ski House) デモ環境で実行することをお勧めします。 「ラボ 06 - [Kusto 照会言語 (KQL) を使用して Microsoft Sentinel のクエリを作成する](https://microsoftlearning.github.io/SC-200T00A-Microsoft-Security-Operations-Analyst/Instructions/Labs/LAB_AK_06_Lab1_Ex01_KQL.html/)」では、代わりに SC-200 ラボ環境を使います。 後者のデプロイには 30 分必要です。

## KQL テスト領域にアクセスする

このタスクでは、KQL ステートメントの記述を練習できる Microsoft Sentinel Log Analytics 環境にアクセスします。

1. 管理者として WIN1 仮想マシンにログインします。パスワードは**Pa55w.rd**。  

1. ブラウザーで <https://security.microsoft.com> にアクセスします。 Zava または Alpine Ski House のユーザー資格情報を使ってログインします。

1. 左側のナビゲーション ウィンドウで **[調査と対応]** セクションを展開します。

1. **[ハンティング]** セクションを展開して、**[高度なハンティング]** を選びます。

1. 画面左側の [スキーマ] タブに一覧表示されている使用可能なテーブルを調べます。** *Microsoft Sentinel* のテーブルと *Security and Audit* のテーブルに注意します。

1. クエリエディタで、次のクエリを入力し、実行 ボタンを選択します。  下部のウィンドウにクエリ結果が表示されます。

    ```KQL
    SecurityEvent
    ```

1. 最初のレコードの横にある **[>]** を選択して、行の情報を展開します。

### タスク 2:基本的なKQL ステートメントを実行する

このタスクでは 基本的なKQL ステートメントを作成します。

1. `search` 演算子を使用すると、複数テーブルまたは複数列の検索エクスペリエンスが得られます。 次のクエリは、`search` 演算子の使用方法を示しています。

    > **注:**  `search` 演算子はリソースを多用します。 [時間の範囲] を [過去 3 時間] に制限し、*limit | 100* を使います。****

```KQL
search "err" 

search in (SecurityEvent,SecurityAlert,A*) "err"
```

1. `where` 演算子は、述語の条件を満たす行のサブセットにテーブルをフィルター処理します。 次のクエリは、`where` 演算子の使用方法を示しています。

```KQL
SecurityEvent | where EventID in (4624, 4625)

SecurityEvent 
| where TimeGenerated > ago(1d) 

SecurityEvent 
| where TimeGenerated > ago(1h) and EventID == "4624" 

SecurityEvent 
| where TimeGenerated > ago(1h) 
| where EventID == 4624 
| where AccountType =~ "user" 
```

1. 次のステートメントは、`let` ステートメントを使用して変数を宣言する方法を示しています。 クエリウィンドウで、次のステートメントを、入力し、**[実行]** を選択します。 

```KQL
let timeOffset = 7d;
let discardEventId = 4688;
SecurityEvent
| where TimeGenerated > ago(timeOffset*2) and TimeGenerated < ago(timeOffset)
| where EventID != discardEventId
```

1. 次のステートメントは、`let` ステートメントを使用して動的リストを宣言する方法を示しています。 クエリ ウィンドウで、次のステートメントを入力し、**[実行]** を選択します。 

```KQL
let suspiciousAccounts = datatable(account: string) [
    @"\administrator", 
    @"NT AUTHORITY\SYSTEM"
];
SecurityEvent | where Account in (suspiciousAccounts)
```

1. 次のステートメントは、クエリウィンドウに表示されるクエリ時間範囲内のレコードをすべてのテーブルと列で検索する方法を示しています。 このスクリプトを実行する前に、クエリ ウィンドウで、時間範囲を「最後の時間」に変更します。 次のステートメントを入力し、**[実行]** を選択します。

```KQL
search "err"
```

**警告:** 次のスクリプトのために、必ず時間範囲を "過去 24 時間" に戻してください。

### レンダー演算子を使用してKQLでビジュアライゼーションを作成します

このタスクでは,KQLステートメントを使用した視覚化の生成を使用します

1. 次のステートメントは、棒グラフを使用して結果を視覚化するレンダリング関数を示しています。 クエリ ウィンドウ内 次のステートメントを入力し、**[実行]** を選択します。 

```KQL
SecurityEvent 
| summarize count() by Account
| render barchart
```

1. 次のステートメントは、時系列で結果を視覚化するレンダリング関数を示しています。

bin() 関数では、指定のビン サイズの整数の倍数になるように値を切り捨てます。  summarize by ... と組み合わせてよく使用されます。値のセットが分散している場合、その値は特定の値の小さなセットにグループ化されます。  生成された時系列と render 演算子へのパイプを timechart の種類と結合することで、時系列を視覚化できます。 クエリ ウィンドウ内 次のステートメントを入力し、**[実行]** を選択します。 

```KQL
SecurityEvent 
| summarize count() by bin(TimeGenerated, 1d) 
| render timechart
```

## デモが完了しました
