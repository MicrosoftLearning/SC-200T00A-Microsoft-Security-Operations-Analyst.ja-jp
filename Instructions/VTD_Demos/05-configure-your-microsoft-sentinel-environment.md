# <a name="module-5-configure-your-microsoft-sentinel-environment"></a>モジュール 5 Microsoft Sentinel 環境を構成する

**注**: このデモを正常に完了するには、[前提条件ドキュメント](00-prerequisites.md)のすべての手順を完了する必要があります。 

## <a name="explore-the-microsoft-sentinel-interface"></a>Microsoft Sentinel インターフェイスを調べる

1. [前提条件のセクション](00-prerequisites.md#deploy-azure-sentinel-workspace-for-demo-in-module-4)を完了したときに以前に作成した Microsoft Sentinel インスタンスに戻ります。

1. 新しく作成された Microsoft Sentinel ワークスペースをナビゲートして、ユーザーインターフェイスオプションに慣れてください。

## <a name="create-a-watchlist"></a>ウォッチリストを作成する。

このタスクでは、ウォッチリストを作成します。

1. In the search box at the bottom of the screen, enter <ph id="ph1">`Notepad`</ph>.  Select <bpt id="p1">**</bpt>Notepad<ept id="p1">**</ept> from the results.

1. 「`Hostname`」と入力し、新しい行を入力します。

1. 行 2 ～ 6 に、次のホスト名を追加します。
    ```
    Host1
    Host2
    Host3
    Host4
    Host5
    ```

1. From the menu select, <bpt id="p1">**</bpt>File - Save As<ept id="p1">**</ept>, Name the file <ph id="ph1">`HighValue.csv`</ph>.  Then change the file type to <bpt id="p1">**</bpt>All files(<bpt id="p2">*</bpt>.<ept id="p2">*</ept>)<ept id="p1">**</ept>.  Then select <bpt id="p1">**</bpt>Save<ept id="p1">**</ept>.

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

1. Select your new watchlist.  On the right tab, select <bpt id="p1">**</bpt>View in Log Analytics<ept id="p1">**</ept>.

1. 次のKQLステートメントが自動的に実行され、結果が表示されます。

```KQL
_GetWatchlist('HighValueHosts')
```
**注**完了するまで少し時間がかかります。

You can now use the _GetWatchlist('HighValueHosts') in your own KQL statements to access the list. The column to reference would be <bpt id="p1">*</bpt>Hostname<ept id="p1">*</ept>.

## <a name="create-a-threat-indicator"></a>脅威インジケーターを作成する。

このタスクでは、インジケーターを作成します。

1. Microsoft Sentinel で、 **[脅威の管理]** 領域の **[脅威インテリジェンス]** オプションを選択します。

1. コマンド バーから **[新規追加]** を選択します。

1. Review the different indicator types available in the Types dropdown.  Then select <bpt id="p1">**</bpt>domain-name<ept id="p1">**</ept>. Enter your initials in the Domain box. An example would be fmg.com.

1. 脅威の種類については、 **[+ 追加]** を選択し、**悪意のあるアクティビティ**をコピーしてフィールドに貼り付けます。

1. For the name, enter the same value used for the Domain. An example would be fmg.com.

1. **[有効開始日]** フィールドを今日の日付に設定します。

1. **[適用]** を選択します。

**注**インジケーターが表示されるまで少し時間がかかる場合があります。

1. Select <bpt id="p1">**</bpt>Logs<ept id="p1">**</ept> option in the General area.  You may have to disable the "Always show queries" option to get to the query window.

1. 以下の KQL ステートメントを実行します。

```KQL
ThreatIntelligenceIndicator 
```
Scroll the results to the right to see the DomainName column. You can also run the following KQL statement to just see the DomainName column.  

```KQL
ThreatIntelligenceIndicator 
| project DomainName
```
## <a name="you-have-completed-the-demo"></a>デモが完了しました。