---
ms.openlocfilehash: db32880d4180f36923dff34b1b2cd9e8640cd2ec
ms.sourcegitcommit: c026d30237cf9a0efdc6e7bbc58a395ecbc9e250
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/03/2022
ms.locfileid: "147449883"
---
# <a name="module-4-create-queries-for-microsoft-sentinel-using-kusto-query-language-kql"></a>モジュール 4 Kusto 照会言語 (KQL) を使用して Microsoft Sentinel のクエリを作成する

**注**: このデモを正常に完了するには、[前提条件ドキュメント](00-prerequisites.md)のすべての手順を完了する必要があります。 

## <a name="access-the-kql-testing-area"></a>KQLテストエリアにアクセスします。

このタスクでは、KQLステートメントの記述を練習できるLog Analytics環境にアクセスします。

1. 管理者として WIN1 仮想マシンにログインします。パスワードは **Pa55w.rd**。  

2. ブラウザーで https://aka.ms/lademo にアクセスします。 MOD管理者の資格情報を使用してログインします。 

3. 画面左側のタブのリストから使用可能なテーブルを調べます。

4. クエリエディタで、次のクエリを入力し、実行 ボタンを選択します。  下部のウィンドウにクエリ結果が表示されます。

    ```KQL
    SecurityEvent
    ```

5. 最初のレコードの横にある **[>]** を選択して、行の情報を展開します。

### <a name="task-2-run-basic-kql-statements"></a>タスク 2:基本的なKQL ステートメントを実行する

このタスクでは 基本的なKQL ステートメントを作成します。

1. 次のステートメントは、letステートメントを使用して変数をデモンストレーションする方法を示しています。 クエリウィンドウで、次のステートメントを、入力し、**[実行]** を選択します。 


```KQL
let timeOffset = 7d;
let discardEventId = 4688;
SecurityEvent
| where TimeGenerated > ago(timeOffset*2) and TimeGenerated < ago(timeOffset)
| where EventID != discardEventId
```

1. 次のステートメントは、letステートメントを使用して動的リストを宣言する方法を示しています。 クエリ ウィンドウで、次のステートメントを入力し、**[実行]** を選択します。 


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

### <a name="create-visualizations-in-kql-with-the-render-operator"></a>レンダー演算子を使用してKQLでビジュアライゼーションを作成します

このタスクでは,KQLステートメントを使用した視覚化の生成を使用します

1. 次のステートメントは、棒グラフを使用して結果を視覚化するレンダリング関数を示しています。 クエリ ウィンドウ内 次のステートメントを入力し、**[実行]** を選択します。 

```KQL
SecurityEvent 
| summarize count() by Account
| render barchart
```

2. 次のステートメントは、時系列で結果を視覚化するレンダリング関数を示しています。

bin() 関数では、指定のビン サイズの整数の倍数になるように値を切り捨てます。  summarize by ... と組み合わせてよく使用されます。値のセットが分散している場合、その値は特定の値の小さなセットにグループ化されます。  生成された時系列と render 演算子へのパイプを timechart の種類と結合することで、時系列を視覚化できます。 クエリ ウィンドウ内 次のステートメントを入力し、**[実行]** を選択します。 

```KQL
SecurityEvent 
| summarize count() by bin(TimeGenerated, 1d) 
| render timechart
```

## <a name="you-have-completed-the-demo"></a>デモが完了しました。

