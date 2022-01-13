---
lab:
    title: '演習 1 - Microsoft Sentinel で脅威ハンティングを実行する'
    module: 'モジュール 8 – Microsoft Sentinel で脅威ハンティングを実行する'
---

# モジュール 8 - ラボ 1 - 演習 1 - Microsoft Sentinel で脅威ハンティングを実行する

## ラボ シナリオ

あなたは、Microsoft Sentinel を実装した会社で働いているセキュリティ オペレーションアナリストです。あなたはコマンドと制御 (C2 または C&C) テクニックについて脅威インテリジェンスを受け取りました。  その脅威に対して捜索とウォッチを実行する必要があります。

>**重要:** このラボで使用するログデータは、前のモジュールで作成したものです。演習 5 の WIN1 サーバーの**攻撃 3** を参照してください。

>**注:**  前のモジュールでデータを探索するプロセスをすでに経験しているため、ラボでは開始するための KQL ステートメントを提供しています。  


### タスク 1: ハンティング クエリの作成

このタスクでは、ハンティングクエリを作成し、結果をブックマークして、ライブ ストリームを作成します。

1. 管理者として WIN1 仮想マシンにログインします。パスワードは**Pa55w.rd** です。  

2. Microsoft Edge ブラウザーで Azure portal (https://portal.azure.com) に移動します。

3. **サインイン** ダイアログ ボックスで、ラボ ホスティング プロバイダーから提供された**テナントのメール** アカウントをコピーして貼り付け、「**次へ**」を選択します。

4. **パスワードの入力**ダイアログ ボックスで、ラボ ホスティング プロバイダーから提供された**テナントパスワード** をコピーして貼り付け、「**サインイン**」を選択します。

5. Azure portal の検索バーに「*Sentinel*」と入力し、「**Microsoft Sentinel**」を選択します。

6. Microsoft Sentinel ワークスペースを選択します。

7. 「**ログ**」を選択する 

8. 新規クエリ1のスペースに以下のKQLステートメントを入力します。

   >**重要:** どんな間違いも避けるために、どの KQL クエリも最初にメモ帳に貼り付け、次に、そこから *New Query 1* ログ ウィンドウにコピーしてください。

```KQL
let lookback = 2d;
DeviceEvents
| where TimeGenerated >= ago(lookback) 
| where ActionType == "DnsQueryResponse"
| extend c2 = substring(tostring(AdditionalFields.DnsQueryString),0,indexof(tostring(AdditionalFields.DnsQueryString),"."))
| where c2 startswith "sub"
| summarize count() by bin(TimeGenerated, 3m), c2
| where count_ > 5
| render timechart 
```

   ![スクリーンショット](../Media/SC200_hunting1.png)

9. このステートメントの目的は、C2 が一貫してビーコンを出しているかどうかを確認するための視覚化を提供することです。オペレーター概要などで、3m の設定を 30 秒以上に調整してください。count_ > 5 の設定を他のスレッショルド カウントに変更して、影響を確認します。

10. これで、C2 サーバーにビーコン送信されている DNS リクエストが特定できました。  次に、どのデバイスがビーコンになっているかを確認します。  次の KQL ステートメントを入力します。

```KQL
let lookback = 2d;
DeviceEvents
| where TimeGenerated >= ago(lookback) 
| where ActionType == "DnsQueryResponse"
| extend c2 = substring(tostring(AdditionalFields.DnsQueryString),0,indexof(tostring(AdditionalFields.DnsQueryString),"."))
| where c2 startswith "sub"
| summarize cnt=count() by bin(TimeGenerated, 5m), c2, DeviceName
| where cnt > 15
```

   ![スクリーンショット](../Media/SC200_hunting2.png)

   >**注:** 生成されるログ データは、1 つのデバイスからのみです。

11. ウィンドウの右上で「ｘ」を選択して「ログ」ウィンドウを閉じ、「**OK**」を選択して変更を破棄します。Microsoft Sentinel ワークスペースをもう一度選択し、「脅威管理」領域の下の「**ハンティング**」ページを選択します。

12. コマンド バーで「**+ 新しいクエリ**」を選択します。

13. **カスタム クエリ**には、次の KQL ステートメントを入力します。

```KQL
let lookback = 2d;
DeviceEvents
| where TimeGenerated >= ago(lookback) 
| where ActionType == "DnsQueryResponse"
| extend c2 = substring(tostring(AdditionalFields.DnsQueryString),0,indexof(tostring(AdditionalFields.DnsQueryString),"."))
| where c2 startswith "sub"
| summarize cnt=count() by bin(TimeGenerated, 5m), c2, DeviceName
| where cnt > 15
```

14. 名前には「*C2 Hunt*」と入力します。

15. **エンティティ マッピング (プレビュー)** で、以下を選択します。

    - 「*エンティティ タイプ*」ドロップダウン リストには「**ホスト**」を選択します。
    - 「*識別子*」ドロップダウン リストには「**ホスト名**」を選択します。
    - 「*値*」ドロップダウン リストには「**デバイス名**」を選択します。

16. **戦術と手法**で、「**Command and Control**」を選択します。「**作成**」を選択して、ハンティング クエリを作成します。

17. Microsoft Sentinel - ハンティング ブレードで、リストの　*C2 Hunt*　で、先ほど作成したクエリを検索します。

18. リストの中から「**C2 Hunt**」を選択します。

19. 画面の右側の「**クリエの実行**」ボタンを選択します。

20. 結果のカウントは、フライアウトの上部に表示されます。

21. 「**結果の表示**」ボタンを選択します。

22. 結果の最初の行を選択します。 

23. 「**ブックマークの追加**」ボタンを選択します。

24. **ブックマークの追加** ブレードで、「**作成**」 を選択します。

25. Microsoft Sentinel portal のハンティング ページに戻ります (ヒント: 左にスクロールします)。

26. 「**ブックマーク**」タブを選択します。

27. 結果一覧で作成したブックマークを選択します。

28. 「**調査**」 ボタンを選択します。

29. グラフを調査します。

30. Microsoft Sentinel portalの「ハンティング」ページに、右上の「ｘ」を選択してウィンドウを閉じることにより戻ります。

31. 「**クエリ**」タブを選択します

32. もう一度「**C2 ハント**」クエリを検索し、選択します。

33. 右側の行の最後にある **「...」** を選択して、コンテキスト メニューを開きます。

34. 「**ライブストリームに追加**」を選択します。

# 演習 2 に進みます。
