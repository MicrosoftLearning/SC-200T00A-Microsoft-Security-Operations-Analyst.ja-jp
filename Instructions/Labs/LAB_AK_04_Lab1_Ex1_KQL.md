---
lab:
    title: '演習 1 - Kusto クエリ言語 (KQL) を使用した Microsoft Sentinel 用のクエリの作成'
    module: 'モジュール 4 - Kusto クエリ言語 (KQL) を使用したMicrosoft Sentinel用のクエリの作成'
---

# モジュール 4 - ラボ 1 - 演習 1 - Kusto クエリ言語 (KQL) を使用した Microsoft Sentinel 用のクエリの作成

## ラボ シナリオ
あなたは、Microsoft Sentinel を実装しようとしている会社で働いているセキュリティ オペレーションアナリストです。悪意のあるアクティビティを検索し、視覚化を表示し、脅威ハンティングを実行するためにログ データ分析を行う責任があります。ログ データのクエリを実行するには、Kusto クエリ言語 (KQL) を使用します。

>**ヒント:** このラボでは、多くの KQL スクリプトを Microsoft Sentinel に入力します。スクリプトは、このラボの開始部のファイルで提供されます。それらをダウンロードするための代替の場所は以下の通りです。  https://github.com/MicrosoftLearning/SC-200T00JA-Microsoft-Security-Operations-Analyst/tree/master/Allfiles


### タスク 1: KQLテストエリアにアクセスします。

このタスクでは、KQLステートメントの記述を練習できるLog Analytics環境にアクセスします。

1. 管理者として WIN1 仮想マシンにログインします。パスワードは**Pa55w.rd** です。  

2. ブラウザーで https://aka.ms/lademo にアクセスします。MOD管理者の資格情報を使用してログインします。 

3. 画面左側のタブのリストから使用可能なテーブルを調べます。

4. クエリエディタで、次のクエリを入力し、「**実行**」ボタンを選択します。  下部のウィンドウにクエリ結果が表示されます。

```KQL
SecurityEvent
```

5. 最初のレコードの横にある「**>**」を選択して、行の情報を展開します。


### タスク 2: 基本的なKQL ステートメントを実行する

このタスクでは 基本的なKQL ステートメントを作成します。

>**重要:**  それぞれのクエリで、クエリ ウィンドウから前のステートメントをクリアするか、最後に開いたタブ (最大 25) の後の「**+**」を選択して新しいクエリ ウィンドウを開きます。

1. 次のステートメントは、letステートメントを使用して変数をデモンストレーションする方法を示しています。クエリ ウィンドウ内次のステートメントを入力し、「**実行**」を選択します。 

```KQL
let timeOffset = 7d;
let discardEventId = 4688;
SecurityEvent
| where TimeGenerated > ago(timeOffset*2) and TimeGenerated < ago(timeOffset)
| where EventID != discardEventId
```

2. 次のステートメントは、letステートメントを使用して動的リストを宣言する方法を示しています。クエリウィンドウで、次のステートメントを入力し、「**実行**」を選択します。 

```KQL
let suspiciousAccounts = datatable(account: string) [
    @"\administrator", 
    @"NT AUTHORITY\SYSTEM"
];
SecurityEvent | where Account in (suspiciousAccounts)
```

3. 次のステートメントは、"let" ステートメントを使用して動的リストを宣言する方法を示しています。クエリ ウィンドウ内次のステートメントを入力し、「**実行**」を選択します。 

```KQL
let LowActivityAccounts =
    SecurityEvent 
    | summarize cnt = count() by Account 
    | where cnt < 10;
LowActivityAccounts | where Account contains "sql"
```

4. 次のステートメントは、クエリウィンドウに表示されるクエリ時間範囲内のレコードをすべてのテーブルと列で検索する方法を示しています。このスクリプトを実行する前に、クエリウィンドウで、「**時間範囲**」を「最後の時間」に変更します。次のステートメントを入力し、「**実行**」を選択します。 

```KQL
search "err"
```

>**警告**：次のスクリプトのために、必ず時間範囲を「過去24時間」に戻してください。

5. 次のステートメントは、「in」句でリストされたテーブル全体で、クエリウィンドウに表示されるクエリ時間範囲内のレコードを検索する方法を示しています。クエリ ウィンドウ内次のステートメントを入力し、「**実行**」を選択します。 

```KQL
search in (SecurityEvent,SecurityAlert,A*) "err"
```

6. 次のステートメントは、where演算子を使用したフィルターを示しています。クエリ ウィンドウ内次のステートメントを入力し、「**実行**」を選択します。 

> **注:** 以下の各コードブロックからクエリを入力した後、「実行」する必要があります。

```KQL
SecurityEvent
| where TimeGenerated > ago(1d)
```

```KQL
SecurityEvent
| where TimeGenerated > ago(1h) and EventID == "4624"
```

```KQL
SecurityEvent
| where TimeGenerated > ago(1h)
| where EventID == 4624
| where AccountType =~ "user"
```

```KQL
SecurityEvent | where EventID in (4624, 4625)
```

7. 次のステートメントは、クエリウィンドウでextend演算子を使用してフィールドを作成する方法を示しています。次のステートメントを入力し、「**実行**」を選択します。 

```KQL
SecurityAlert
| where TimeGenerated > ago(7d)
| extend severityOrder = case (
    AlertSeverity == "High", 3,
    AlertSeverity == "Medium", 2, 
    AlertSeverity == "Low", 1,
    AlertSeverity == "Informational", 0,
    -1)
```

8. 次のステートメントは、orderby演算子を使用した結果の並べ替えを示しています。クエリ ウィンドウ内次のステートメントを入力し、「**実行**」を選択します。 

```KQL
SecurityAlert
| where TimeGenerated > ago(7d)
| extend severityOrder = case (
    AlertSeverity == "High", 3,
    AlertSeverity == "Medium", 2, 
    AlertSeverity == "Low", 1,
    AlertSeverity == "Informational", 0,
    -1)
| order by severityOrder desc
```

9. 次のステートメントは、プロジェクト演算子を使用して結果セットのフィールドを指定する方法を示しています。

    >**注:** 以下の各コードブロックからクエリを入力した後、「実行」する必要があります。

クエリ ウィンドウ内次のステートメントを入力し、「**実行**」を選択します。 

```KQL
SecurityEvent
| project Computer, Account
```

```KQL
SecurityAlert
| where TimeGenerated > ago(7d)
| extend severityOrder = case (
    AlertSeverity == "High", 3,
    AlertSeverity == "Medium", 2, 
    AlertSeverity == "Low", 1,
    AlertSeverity == "Informational", 0,
    -1)
| order by severityOrder
| project-away severityOrder
```


### タスク 3: Summarize演算子を使用してKQLで結果を分析する

このタスクでは、データを準備するためのKQLステートメントを作成します

1. 次のステートメントは、count関数を示しています。クエリ ウィンドウ内次のステートメントを入力し、「**実行**」を選択します。 

```KQL
SecurityEvent
| where EventID == "4688"
| summarize count() by Process, Computer
```

2. 次のステートメントは、count関数を示しています。クエリ ウィンドウ内次のステートメントを入力し、「**実行**」を選択します。 

```KQL
SecurityEvent
| where TimeGenerated > ago(1h)
| where EventID == 4624
| summarize cnt=count() by AccountType, Computer
```

3. 次のステートメントは、dcount関数を示しています。クエリ ウィンドウ内次のステートメントを入力し、「**実行**」を選択します。 

```KQL
SecurityEvent
| summarize dcount(IpAddress)
```

4. 次のステートメントは、arg_max 関数を示しています。

次のステートメントはSQL12.NA.contosohotels.com コンピューターの SecurityEvent テーブルから最新の行を返します。  arg_max 関数の*でその行のすべての列を要求します。クエリ ウィンドウ内次のステートメントを入力し、「**実行**」を選択します。 

```KQL
SecurityEvent 
| where Computer == "SQL12.na.contosohotels.com"
| summarize arg_max(TimeGenerated,*) by Computer
```

5. 次のステートメントは、arg_min 関数を示しています。

このステートメントでは、SQL12.NA.contosohotels.com コンピューターの最も古い SecurityEvent を結果セットとして返します。クエリ ウィンドウ内次のステートメントを入力し、「**実行**」を選択します。 

```KQL
SecurityEvent 
| where Computer == "SQL12.na.contosohotels.com"
| summarize arg_min(TimeGenerated,*) by Computer
```

6. 次のステートメントは、パイプの順序に基づいて結果を理解することの重要性を示しています。|"クエリ ウィンドウ内次のクエリを入力し、それぞれを個別に実行します。 

**Query 1** には、最後のアクティビティがログインだった Account が含まれます。まず、SecurityEvent テーブルが集計され、各 Account の最新行を返します。  その後、EventID が 4624 (ログイン) に等しい行だけ返します。

```KQL
SecurityEvent
| summarize arg_max(TimeGenerated, *) by Account
| where EventID == "4624"
```

**Query 2** には、ログインしたアカウントの最新のログインが含まれます。 SecurityEvent テーブルは、EventID = 4624 のみを含むようにフィルター処理されます。これらの結果は、Account ごとに最新のログイン行に対して集計されます。

```KQL
SecurityEvent
| where EventID == "4624"
| summarize arg_max(TimeGenerated, *) by Account
```

>**注:**  「完了」バーを選択して「合計 CPU」と「処理されたクエリに使用されたデータ」を確認し、両方のステートメント間のデータを比較することができます。

7. 次のステートメントは、make_list 関数を示しています。

make_list 関数では、グループ内の式のすべての値の動的な (JSON) 配列を返します。この KQL クエリでは、まず where 演算子を使用して EventID をフィルター処理します。  次に、各コンピューターについて、結果がアカウントの JSON 配列になります。結果として得られる JSON 配列には、重複するアカウントが含まれます。

クエリ ウィンドウ内次のステートメントを入力し、「**実行**」を選択します。 

```KQL
SecurityEvent
| where EventID == "4624"
| summarize make_list(Account) by Computer
```

8. 次のステートメントは、make_set 関数を示しています。

make_set　関数は、Expression がグループ内で取る*個別の*値を含む動的 （JSON） 配列を返します。この KQL クエリでは、まず where 演算子を使用して EventID をフィルター処理します。  次に、各 Computer について、結果が一意の Account の JSON 配列になります。クエリ ウィンドウ内次のステートメントを入力し、「**実行**」を選択します。 

```KQL
SecurityEvent
| where EventID == "4624"
| summarize make_set(Account) by Computer
```


### タスク 4: レンダー演算子を使用してKQLでビジュアライゼーションを作成します

このタスクでは,KQLステートメントを使用した視覚化の生成を使用します

1. 次のステートメントは、棒グラフを使用して結果を視覚化するレンダリング関数を示しています。クエリ ウィンドウ内次のステートメントを入力し、「**実行**」を選択します。 

```KQL
SecurityEvent 
| summarize count() by Account
| render barchart
```

2. 次のステートメントは、時系列で結果を視覚化するレンダリング関数を示しています。

bin() 関数では、指定のビン サイズの整数の倍数になるように値を切り捨てます。  summarize by ... と組み合わせてよく使用されます。値のセットが分散している場合、その値は特定の値の小さなセットにグループ化されます。  生成された時系列と render 演算子へのパイプを timechart の種類と結合することで、時系列を視覚化できます。クエリ ウィンドウ内次のステートメントを入力し、「**実行**」を選択します。 

```KQL
SecurityEvent 
| summarize count() by bin(TimeGenerated, 1h) 
| render timechart
```


### タスク 5: KQLでマルチテーブルステートメントを作成する

このタスクでは、マルチテーブルKQLステートメントを作成します。

1. 次のステートメントは、2つ以上のテーブルを取得し、それらすべての行を返すunion演算子を示しています。結果を渡す方法、およびパイプ文字によってどのような影響があるかを理解することは重要です。クエリ ウィンドウ内次のステートメントを入力し、それぞれに対し、「**実行**」を選択して、結果を確認します。 

**Query 1** で SecurityEvent のすべての行と SecurityAlert のすべての行が返されます

```KQL
SecurityEvent 
| union SecurityAlert  
```

**Query 2** で SecurityEvent のすべての行数と SecurityAlert のすべての行数である 1 つの行と列が返されます

```KQL
SecurityEvent 
| union SecurityAlert  
| summarize count() 
| project count_
```

**Query 3** で SecurityEvent のすべての行と SecurityAlert のすべての 1 つの行が返されます  SecurityAlert の行は、SecurityAlert の行数です。

```KQL
SecurityEvent 
| union (SecurityAlert  | summarize count()) 
| project count_
```

2. 次のステートメントは、複数のテーブルを結合するためのワイルドカードのunion演算子のサポートを示しています。クエリ ウィンドウ内次のステートメントを入力し、「**実行**」を選択します。 

```KQL
union Security* 
| summarize count() by Type
```

3. 次のステートメントは、各テーブルから指定された列の値を照合することにより、2つのテーブルの行をマージして新しいテーブルを形成するunion演算子を示しています。クエリ ウィンドウ内次のステートメントを入力し、「**実行**」を選択します。 

```KQL
SecurityEvent 
| where EventID == "4624" 
| summarize LogOnCount=count() by EventID, Account 
| project LogOnCount, Account 
| join kind = inner (
     SecurityEvent 
     | where EventID == "4634" 
     | summarize LogOffCount=count() by EventID, Account 
     | project LogOffCount, Account 
) on Account
```

結合で指定した最初のテーブルが左テーブルと見なされます。  join キーワードの後のテーブルが右テーブルです。  テーブルの列を操作する場合、$ left.Columnnameと$ right.Column nameは、参照されるテーブルの列を区別するためのものです。 


### タスク 6: KQLで文字列データを操作する

このタスクでは、KQLステートメントを使用して構造化および非構造化文字列フィールドを操作します。

1. 次のステートメントは、extract 関数を示しています。  extract では、テキスト文字列から正規表現との一致を抽出します。抽出されたサブ文字列を指定された型に変換するオプションがあります。クエリ ウィンドウ内次のステートメントを入力し、「**実行**」を選択します。 

```KQL
print extract("x=([0-9.]+)", 1, "hello x=45.6|wo") == "45.6"
```

2. 次のステートメントでは、extract 関数を使用して、SecurityEvent テーブルの Account フィールドから Account Name を取得します。クエリ ウィンドウ内次のステートメントを入力し、「**実行**」を選択します。 

```KQL
let top3 = SecurityEvent
| where TimeGenerated > ago(1h)
| where AccountType == 'User'
| extend Account_Name = extract(@"^(.*\\)?([^@]*)(@.*)?$", 2, tolower(Account))
| summarize Attempts = count() by Account_Name
| where Account_Name != ""
| top 3 by Attempts 
| summarize make_list(Account_Name);
SecurityEvent
| where TimeGenerated > ago(1h)
| where AccountType == 'User'
| extend Name = extract(@"^(.*\\)?([^@]*)(@.*)?$", 2, tolower(Account))
| extend Account_Name = iff(Name in (top3), Name, "Other")
| where Account_Name != ""
| summarize Attempts = count() by Account_Name
| sort by Attempts
```

3. 次のステートメントは、parse 関数を示しています。parse 文字列式が評価され、その値が 1 つまたは複数の計算列に解析されます。解析に失敗した文字列の計算列には null が含まれます。

```KQL
let Traces = datatable(EventText:string)
[
"Event: NotifySliceRelease (resourceName=PipelineScheduler, totalSlices=27, sliceNumber=23, lockTime=02/17/2016 08:40:01, releaseTime=02/17/2016 08:40:01, previousLockTime=02/17/2016 08:39:01)",
"Event: NotifySliceRelease (resourceName=PipelineScheduler, totalSlices=27, sliceNumber=15, lockTime=02/17/2016 08:40:00, releaseTime=02/17/2016 08:40:00, previousLockTime=02/17/2016 08:39:00)",
"Event: NotifySliceRelease (resourceName=PipelineScheduler, totalSlices=27, sliceNumber=20, lockTime=02/17/2016 08:40:01, releaseTime=02/17/2016 08:40:01, previousLockTime=02/17/2016 08:39:01)",
"Event: NotifySliceRelease (resourceName=PipelineScheduler, totalSlices=27, sliceNumber=22, lockTime=02/17/2016 08:41:01, releaseTime=02/17/2016 08:41:00, previousLockTime=02/17/2016 08:40:01)",
"Event: NotifySliceRelease (resourceName=PipelineScheduler, totalSlices=27, sliceNumber=16, lockTime=02/17/2016 08:41:00, releaseTime=02/17/2016 08:41:00, previousLockTime=02/17/2016 08:40:00)"
];
Traces  
| parse EventText with * "resourceName=" resourceName ", totalSlices=" totalSlices:long * "sliceNumber=" sliceNumber:long * "lockTime=" lockTime ", releaseTime=" releaseTime:date "," * "previousLockTime=" previousLockTime:date ")" *  
| project resourceName, totalSlices, sliceNumber, lockTime, releaseTime, previousLockTime
```

4. 次のステートメントは、動的フィールドの操作を示しています

Log Analyticsテーブル内には、動的として定義されたフィールドタイプがあります。動的フィールドには、キーと値のペアが含まれます。

動的フィールド内の文字列にアクセスするには、ドット表記を使用します。AppAvailabilityResults テーブルの Properties フィールドの型は動的です。この例では、Properties.SyntheticMonitorId というフィールド名を使用して SyntheticMonitorId にアクセスできます。

クエリ ウィンドウ内次のステートメントを入力し、**実行します**。 

```KQL
AppAvailabilityResults
| project Properties.SyntheticMonitorId
```

5. 次のステートメントは、文字列フィールドに格納されているJSONを操作する関数を示しています。多くのログでは JSON 形式でデータを送信します。そのため、JSON データをクエリ可能なフィールドに変換する方法を知る必要があります。 

クエリ ウィンドウ内次のステートメントをそれぞれ入力し、「**実行**」を選択します。 

```KQL
SecurityAlert
| extend ExtendedProperties = todynamic(ExtendedProperties) 
| extend ActionTaken = ExtendedProperties.ActionTaken
| extend AttackerIP = ExtendedProperties["Attacker IP"]
```
mv-expand 演算子が、複数の値のある動的配列またはプロパティ バッグを複数のレコードに展開します。

```KQL
SecurityAlert
| mv-expand entity = todynamic(Entities)
```
mv-apply 演算子が、サブクエリを各レコードに適用してすべてのサブクエリの結果集合体を返します。

```KQL
SecurityAlert
| where TimeGenerated >= ago(7d)
| mv-apply entity = todynamic(Entities) on 
( where entity.Type == "account" | extend account = strcat (entity.NTDomain, "\\", entity.Name))
```

6. 関数を作成するには：

> **注:** このラボのデータに使用されるラデモ環境ではこれを行うことはできませんが、これは、環境で使用する重要な概念です。 

クエリを実行した後、「**保存**」ボタンを選択してから、ドロップダウンから、「**Save As function**」 (関数として保存) を選択します。希望の名前を入力します。たとえば、「**関数名**」ボックスに「*MailboxForward*」と入力し、「**凡例カテゴリ**」に「*General*」などを入力して、「**保存**」を選択します。

この関数は、関数エイリアスを使用して KQL で使用できます。

```KQL
MailboxForward
```

## これでラボは完了です。
