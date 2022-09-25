---
lab:
  title: 演習 1 - Microsoft Sentinel 環境を構成する
  module: Module 5 - Configure your Microsoft Sentinel environment
---

# <a name="module-5---lab-1---exercise-1---configure-your-microsoft-sentinel-environment"></a>モジュール 5 - ラボ 1 - 演習 1 - Microsoft Sentinel 環境を構成する

## <a name="lab-scenario"></a>ラボのシナリオ

![ラボの概要。](../Media/SC-200-Lab_Diagrams_Mod5_L1_Ex1.png)

You are a Security Operations Analyst working at a company that is implementing Microsoft Sentinel. You are responsible for setting up the Microsoft Sentinel environment to meet the company requirement to minimize cost, meet compliance regulations, and provide the most manageable environment for your security team to perform their daily job responsibilities.


### <a name="task-1-initialize-the-microsoft-sentinel-workspace"></a>タスク 1:Microsoft Azure Sentinel ワークスペースを初期化する

このタスクでは、Microsoft Sentinel ワークスペースを作成します。

1. 管理者として **WIN1** 仮想マシンにログインします。パスワードは **Pa55w.rd** です。  

1. Microsoft Edge ブラウザーを開きます。

1. Edge ブラウザーで、Azure portal (https://portal.azure.com ) に移動します。

1. **[サインイン]** ダイアログ ボックスで、ラボ ホスティング プロバイダーから提供された**テナントの電子メール** アカウントをコピーして貼り付け、 **[次へ]** を選択します。

1. **[パスワードの入力]** ダイアログ ボックスで、ラボ ホスティング プロバイダーから提供された**テナントのパスワード**をコピーして貼り付け、 **[サインイン]** を選択します。

1. Azure portal の検索バーに「*Sentinel*」と入力し、**[Microsoft Sentinel]** を選択します。

1. **[+ 作成]** を選択します。

1. Next, select the Log Analytics workspace you created earlier, for example <bpt id="p1">*</bpt>uniquenameDefender<ept id="p1">*</ept> and select <bpt id="p2">**</bpt>Add<ept id="p2">**</ept>. The activation could take a few minutes.

    >**注:**  ここに Log Analytics ワークスペースが表示されない場合は、モジュール 3、演習 1、タスク 2 を参照して作成してください。

1. 新しく作成された Microsoft Sentinel ワークスペースをナビゲートして、ユーザーインターフェイスオプションに慣れてください。


### <a name="task-2-create-a-watchlist"></a>タスク 2:ウォッチリストを作成する

このタスクでは、Microsoft Sentinel でウォッチリストを作成します。

1. In the search box at the bottom of the Windows 10 screen, enter <bpt id="p1">*</bpt>Notepad<ept id="p1">*</ept>. Select <bpt id="p1">**</bpt>Notepad<ept id="p1">**</ept> from the results.

1. *Hostname* と入力し、新しい行を入力します。

1. メモ帳の 2 行目から、次のホスト名を 1 行に 1 つずつコピーします。

    ```Notepad
    Host1
    Host2
    Host3
    Host4
    Host5
    ```

1. From the menu select, <bpt id="p1">**</bpt>File - Save As<ept id="p1">**</ept>, Name the file <bpt id="p2">*</bpt>HighValue.csv<ept id="p2">*</ept>, change the file type to <bpt id="p3">**</bpt>All files(<bpt id="p4">*</bpt>.<ept id="p4">*</ept>)<ept id="p3">**</ept> and select <bpt id="p5">**</bpt>Save<ept id="p5">**</ept>. <bpt id="p1">**</bpt>Hint:<ept id="p1">**</ept> The file can be saved in the <bpt id="p2">*</bpt>Documents<ept id="p2">*</ept> folder.

1. メモ帳を閉じます。

1. Microsoft Sentinel で、[構成] 領域の **[ウォッチリスト]** オプションを選択します。

1. コマンド バーから **[+ 新規追加]** を選択します。

1. ウォッチリスト ウィザードで、次のように入力します。

    |全般設定|値|
    |---|---|
    |名前|**HighValueHosts**|
    |説明|**High Value Hosts**|
    |ウォッチリスト エイリアス|**HighValueHosts**|

1. **[次へ: ソース >]** を選択します。

1. *[ファイルのアップロード]* で **[ファイルを参照]** を選択し、作成した *HighValue.csv* ファイルを参照します。

1. *[検索キー]* フィールドで、 **[ホスト名]** を選択します。

1. **[次へ: 確認と作成 >]** を選択します。

1. 入力した設定を確認し、 **[作成]** を選びます。

1. 画面が [ウォッチリスト] ページに戻ります。

1. *HighValueHosts* ウォッチリストを選択し、右側のタブで **[ログに表示]** を選択します。

    ><bpt id="p1">**</bpt>Important:<ept id="p1">**</ept> It could take some time for the watchlist to appear. <bpt id="p1">**</bpt>Please continue to with the following task and run this command on the next lab<ept id="p1">**</ept>.
    
    >あなたは、Microsoft Sentinel を実装しようとしている会社で働いているセキュリティ運用アナリストです。

1. 右上にある [x] を選択して *[ログ]* ウィンドウを閉じ、 **[OK]** を選択して保存されていない変更を破棄します。


### <a name="task-3-create-a-threat-indicator"></a>タスク 3:脅威インジケーターを作成する

このタスクでは、Microsoft Sentinel でインジケーターを作成します。

1. Microsoft Sentinel で、[脅威の管理] 領域の **[脅威インテリジェンス]** オプションを選択します。

1. コマンド バーから **[+ 新規追加]** を選択します。

1. コストを最小限に抑え、コンプライアンス規制を満たし、セキュリティ チームが日常の職務を遂行するのに最も管理しやすい環境を提供するという会社の要件を満たすように、Microsoft Sentinel 環境を設定する責任があります。

1. *[脅威の種類]* として、**[悪意のあるアクティビティ]** を選択します。

1. For the <bpt id="p1">*</bpt>Name<ept id="p1">*</ept>, enter the same value used for the Domain. An example would be <bpt id="p1">*</bpt>fmg.com<ept id="p1">*</ept>.

1. *[有効開始日]* フィールドを今日の日付に設定します。

1. **[適用]** を選びます。

1. Select the <bpt id="p1">**</bpt>Logs<ept id="p1">**</ept> option under the General area. You might want to disable the "Always show queries" option and close the <bpt id="p1">*</bpt>Queries<ept id="p1">*</ept> window to run the KQL statements.

1. 以下の KQL ステートメントを実行します。

    ```KQL
    ThreatIntelligenceIndicator
    ```

    >**注:**  インジケーターが表示されるまで、数分かかる場合があります。

1. Scroll the results to the right to see the DomainName column. You can also run the following KQL statement to just see the DomainName column. 

    ```KQL
    ThreatIntelligenceIndicator | project DomainName
    ```

### <a name="task-4-configure-log-retention"></a>タスク 4:ログ保持期間の構成

このタスクでは、SecurityEvent テーブルの保持期間を変更します。

1. Microsoft Sentinel で、 **[構成]** 領域の *[設定]* オプションを選択します。
1. **[ワークスペースの設定]** を選択します。
1. Log Analytics ワークスペースの、 *[設定]* 領域で **[テーブル (プレビュー)]** オプションを選択します。
1. テーブル名 **[SecurityEvent]** 、 **[...]** の順に選択します。
1. **[テーブルの管理]** を選択します。
1. Select <bpt id="p1">**</bpt>180 days<ept id="p1">**</ept> for <bpt id="p2">*</bpt>Total retention period<ept id="p2">*</ept>. Then <bpt id="p1">**</bpt>Save<ept id="p1">**</ept>.


## <a name="you-have-completed-the-lab"></a>これでラボは完了です。
