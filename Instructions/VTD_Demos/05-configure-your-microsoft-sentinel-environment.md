---
ms.openlocfilehash: 8b5dbb31b0de6f493d9eb51a4a2e998aa248ce46
ms.sourcegitcommit: c026d30237cf9a0efdc6e7bbc58a395ecbc9e250
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/03/2022
ms.locfileid: "147449886"
---
# <a name="module-5-configure-your-microsoft-sentinel-environment"></a>モジュール 5 Microsoft Sentinel 環境を構成する

**注**: このデモを正常に完了するには、[前提条件ドキュメント](00-prerequisites.md)のすべての手順を完了する必要があります。 

## <a name="explore-the-microsoft-sentinel-interface"></a>Microsoft Sentinel インターフェイスを調べる

1. [前提条件のセクション](00-prerequisites.md#deploy-azure-sentinel-workspace-for-demo-in-module-4)を完了したときに以前に作成した Microsoft Sentinel インスタンスに戻ります。

1. 新しく作成された Microsoft Sentinel ワークスペースをナビゲートして、ユーザーインターフェイスオプションに慣れてください。

## <a name="create-a-watchlist"></a>ウォッチリストを作成する。

このタスクでは、ウォッチリストを作成します。

1. 画面下部の検索ボックスに「`Notepad`」と入力します。  結果から、**[Notepad]** を選択します。

1. 「`Hostname`」と入力し、新しい行を入力します。

1. 行 2 ～ 6 に、次のホスト名を追加します。
    ```
    Host1
    Host2
    Host3
    Host4
    Host5
    ```

1. メニューから **[ファイル] - [名前を付けて保存]** を選択し、ファイルに「`HighValue.csv`」という名前を付けます。  その後、ファイル タイプを **[すべてのファイル( *.* )]** に変更します。  次に、 **[保存]** を選択します。

1. メモ帳を閉じます。

1. Microsoft Sentinel で、 **[マイ ウォッチリスト]** 領域の **[ウォッチリスト]** オプションを選択します。

1. コマンド バーから **[新規追加]** を選択します。

1. ウォッチリスト ウィザードで、次のように入力します。名前: HighValueHosts  [説明]:High Value Hosts  [Watchlist alias]\(ウォッチリストのエイリアス\):HighValueHosts

1. **[次へ:ソース >]** を選択します。

1. 先ほど作成したファイル `HighValue.csv` を参照します。 

1. CSV ファイルが読み込まれたら、**[検索キー フィールド]** ドロップダウンボックスから **[ホスト名]** を選択します。

1. **[次へ: 確認と作成 >]** を選択します。

1. **［作成］** を選択します

1. 画面がウォッチリストリストに戻ります。

1. 新しいウォッチリストを選択します。  右側のタブで、**[ログ分析で表示]** を選択します。

1. 次のKQLステートメントが自動的に実行され、結果が表示されます。

```KQL
_GetWatchlist('HighValueHosts')
```
**注** 完了するまで少し時間がかかります。

独自のKQLステートメントで_GetWatchlist（ 'HighValueHosts'）を使用して、リストにアクセスできるようになりました。 参照する列は *Hostname* になります。

## <a name="create-a-threat-indicator"></a>脅威インジケーターを作成する。

このタスクでは、インジケーターを作成します。

1. Microsoft Sentinel で、 **[脅威の管理]** 領域の **[脅威インテリジェンス]** オプションを選択します。

1. コマンド バーから **[新規追加]** を選択します。

1. タイプドロップダウンで使用可能なさまざまなインジケータータイプを確認します。  そして、**[domain-name]** を選択します。 ドメインボックスにイニシャルを入力します。 たとえば、fmg.com.などです。

1. 脅威の種類については、 **[+ 追加]** を選択し、**悪意のあるアクティビティ** をコピーしてフィールドに貼り付けます。

1. 名前には、ドメインに使用されているのと同じものを入力します。 たとえば、fmg.com.などです。

1. **[有効開始日]** フィールドを今日の日付に設定します。

1. **[適用]** を選択します。

**注** インジケーターが表示されるまで少し時間がかかる場合があります。

1. 一般領域で **[ログ]** オプションを選択します。  クエリウィンドウを表示するには、[常にクエリを表示する]オプションを無効にする必要がある場合があります。

1. 以下の KQL ステートメントを実行します。

```KQL
ThreatIntelligenceIndicator 
```
結果を右にスクロールして、DomainName 列を表示します。 次の KQL ステートメントを実行して、DomainName 列だけを表示することもできます。  

```KQL
ThreatIntelligenceIndicator 
| project DomainName
```
## <a name="you-have-completed-the-demo"></a>デモが完了しました。