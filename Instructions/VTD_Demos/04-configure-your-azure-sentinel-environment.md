---
ms.openlocfilehash: 806a6762c79381662bd14b22c9de74229270949b
ms.sourcegitcommit: 20cbc7b52187d61fca294ac2c00146c2c7c6d337
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/13/2022
ms.locfileid: "137899221"
---
# <a name="module-4-create-queries-for-azure-sentinel-using-kusto-query-language-kql"></a>モジュール 4 Kusto クエリ言語 (KQL) を使用した Azure Sentinel 用のクエリの作成

**注**: このデモを正常に完了するには、[前提条件ドキュメント](00-prerequisites.md)のすべての手順を完了する必要があります。 

## <a name="explore-the-azure-sentinel-interface"></a>Azure Sentinel インターフェイスを探索する

1. [前提条件のセクション](00-prerequisites.md#deploy-azure-sentinel-workspace-for-demo-in-module-4)を完了したときに以前に作成した　Azure　Sentinel　インスタンスに戻ります。

1. 新しく作成された Azure Sentinel ワークスペースをナビゲートして、ユーザーインターフェイスオプションに慣れてください。

## <a name="create-a-watchlist"></a>ウォッチリストを作成する。

このタスクでは、Watchlist を作成します。

1. 画面下部の検索ボックスに「`Notepad`」と入力します。  結果から、**[Notepad]** を選択します。

2. 「`Hostname`」と入力し、新しい行を入力します。

3. 行 2 ～ 6 に、次のホスト名を追加します。
    ```
    Host1
    Host2
    Host3
    Host4
    Host5
    ```

4. メニューから **[ファイル] - [名前を付けて保存]** を選択し、ファイルに「`HighValue.csv`」という名前を付けます。  その後、ファイル タイプを **[すべてのファイル( *.* )]** に変更します。  次に、 **[保存]** を選択します。

5. メモ帳を閉じます。

6. Azure Sentinel で、**[構成]** 領域の **[ウォッチリスト]** オプションを選択します。

7. コマンド バーから **[新規追加]** を選択します。

8. ウォッチリスト ウィザードで、次のように入力します。名前: HighValueHosts  [説明]:High Value Hosts  [Watchlist alias]\(ウォッチリストのエイリアス\):HighValueHosts

9. **[次へ:ソース >]** を選択します。

10. 先ほど作成したファイル `HighValue.csv` を参照します。 

1. CSV ファイルが読み込まれたら、**[検索キー フィールド]** ドロップダウンボックスから **[ホスト名]** を選択します。

11. **[次へ: 確認と作成 >]** を選択します。

12. **［作成］** を選択します

13. 画面がウォッチリストリストに戻ります。

14. 新しいウォッチリストを選択します。  右側のタブで、**[ログ分析で表示]** を選択します。

15. 次のKQLステートメントが自動的に実行され、結果が表示されます。

```KQL
_GetWatchlist('HighValueHosts')
```
**注** 完了するまで少し時間がかかります。

独自のKQLステートメントで_GetWatchlist（ 'HighValueHosts'）を使用して、リストにアクセスできるようになりました。 参照する列は *Hostname* になります。

## <a name="create-a-threat-indicator"></a>脅威インジケーターを作成する。

このタスクでは、インジケーターを作成します。

1. Azure Sentinel で、**[脅威管理]** 領域の **[脅威インテリジェンス]** オプションを選択します。

2. コマンド バーから **[新規追加]** を選択します。

3. タイプドロップダウンで使用可能なさまざまなインジケータータイプを確認します。  そして、**[domain-name]** を選択します。 ドメインボックスにイニシャルを入力します。 たとえば、fmg.com.などです。

4. 脅威の種類として、**[悪意のあるアクティビティ]** を選択します。

5. 名前には、ドメインに使用されているのと同じものを入力します。 たとえば、fmg.com.などです。

6. **[有効開始日]** フィールドを今日の日付に設定します。

7. **[適用]** を選択します。

**注** インジケーターが表示されるまで少し時間がかかる場合があります。

8. 一般領域で **[ログ]** オプションを選択します。  クエリウィンドウを表示するには、[常にクエリを表示する]オプションを無効にする必要がある場合があります。

9. 以下の KQL ステートメントを実行します。

```KQL
ThreatIntelligenceIndicator 
```
結果を右にスクロールして、DomainName 列を表示します。 次の KQL ステートメントを実行して、DomainName 列だけを表示することもできます。  

```KQL
ThreatIntelligenceIndicator 
| project DomainName
```
## <a name="you-have-completed-the-demo"></a>デモが完了しました。