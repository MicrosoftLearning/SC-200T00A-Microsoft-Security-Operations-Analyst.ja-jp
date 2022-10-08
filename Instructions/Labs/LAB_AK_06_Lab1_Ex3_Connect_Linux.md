---
lab:
  title: 演習 3 - データ コネクタを使用して Microsoft Sentinel に Linux ホストを接続する
  module: Module 6 - Connect logs to Microsoft Sentinel
---

# <a name="module-6---lab-1---exercise-3---connect-linux-hosts-to-microsoft-sentinel-using-data-connectors"></a>モジュール 6 - ラボ 1 - 演習 3 - データ コネクタを使用して Microsoft Sentinel に Linux ホストを接続する

## <a name="lab-scenario"></a>ラボのシナリオ

![ラボの概要。](../Media/SC-200-Lab_Diagrams_Mod6_L1_Ex3.png)

You are a Security Operations Analyst working at a company that implemented Microsoft Sentinel. You must learn how to connect log data from the many data sources in your organization. The next source of data are Linux virtual machines using the Common Event Formatting (CEF) and Syslog connectors.


><bpt id="p1">**</bpt>Important:<ept id="p1">**</ept> There are steps within the next Tasks that are done in different virtual machines. Look for the Virtual Machine name references.

### <a name="task-1-access-the-microsoft-sentinel-workspace"></a>タスク 1:Microsoft Sentinel ワークスペースにアクセスする

このタスクでは、Microsoft Sentinel ワークスペースにアクセスします。

1. 管理者として **WIN1** 仮想マシンにログインします。パスワードは **Pa55w.rd** です。  

1. 新しい Microsoft Edge ブラウザーを起動します。

1. Edge ブラウザーで、Azure portal (https://portal.azure.com ) に移動します。

1. **サインイン** ダイアログ ボックスで、ラボ ホスティング プロバイダーから提供された**テナントの電子メール** アカウントをコピーして貼り付け、**[次へ]** を選択します。

1. **[パスワードの入力]** ダイアログ ボックスで、ラボ ホスティング プロバイダーから提供された**テナント パスワード**をコピーして貼り付け、**[サインイン]** を選択します。

1. Azure portal の検索バーに「*Sentinel*」と入力してから、**[Microsoft Sentinel]** を選択します。

1. 前のラボで作成した Microsoft Sentinel ワークスペースを選択します。


### <a name="task-2-connect-a-linux-host-using-the-common-event-format-connector"></a>タスク 2:共通イベント形式のコネクタを使用して Linux ホストを接続する

このタスクでは、共通イベント形式 (CEF) コネクタを使用して Linux ホストを Microsoft Sentinel に接続します。

1. Select <bpt id="p1">**</bpt>Data connectors<ept id="p1">**</ept> from the Configuration area in Microsoft Sentinel. From the Data Connectors tab, search for the <bpt id="p1">**</bpt>Common Event Format (CEF)<ept id="p1">**</ept> connector and select it from the list.

1. コネクタ情報ブレードで **[コネクタページを開く]** を選択します。

1. *[構成]* で、「*1.2 Linux マシンへの CEF コレクターのインストール*」に示されているコマンドをクリップボードにコピーします。

1. Launch your <bpt id="p1">**</bpt>LIN1<ept id="p1">**</ept> virtual machine. Login with the username and password provided by your lab hoster. <bpt id="p1">**</bpt>Hint:<ept id="p1">**</ept> You might need to press the Enter key to see the login prompt. 

1. Note the IP address for your LIN1 server. See the screenshot below as an example:

    ![Linux ログイン](../Media/LinuxLoginExample.png)

1. あなたは、Microsoft Sentinel を実装した会社で働いているセキュリティ運用アナリストです。

1. 次の PowerShell コマンドを入力し、特定の Linux サーバー情報に合わせて調整し、Enter キーを押します。

    ```PowerShell
    ssh insert-your-linux-IP-address-here -l insert-linux-user-name-here
    ```

1. 組織内の多くのデータ ソースからのログ データを接続する方法について学習する必要があります。

    ![Linux ログイン](../Media/PSconnectLinux.png)

1. 次のデータソースは、共通イベント形式 (CEF) と Syslog コネクタを使用した Linux 仮想マシンです。 

1. 貼り付けてから Enter キーを押す前に、次に示すように、文字 **3** を *python* という単語に追加します。

    ![ConnectorScript](../Media/ConnectorScript.png)


1. Once the script is adjusted press Enter. The script will run against your Linux server remotely. When the script processes properly it should look like this screen:

    ![ConnectorScript](../Media/LinuxConnected.png)

1. 「**exit**」と入力して、LIN1 へのリモート シェル接続を閉じます。


### <a name="task-3-connect-a-linux-host-using-the-syslog-connector"></a>タスク 3:Syslog コネクタを使用して Linux ホストを接続する

このタスクでは、Linux ホストを Syslog コネクタを使用して Microsoft Sentinel に接続します。

1. Microsoft Sentinel ポータルが開いている Edge ブラウザーに戻り、右上隅にある [x] を選択して [共通イベント形式 (CEF)] データ コネクタ ページを閉じます。 

1. [データ コネクタ] タブで、一覧から **Syslog** コネクタを探して選択します。

1. コネクタ情報ブレードで **[コネクタページを開く]** を選択します。

1. *[構成]* で、 **[Azure 以外の Linux マシンにエージェントをインストールする]** セクションを開きます。

1. **非 Azure Linux マシン用のエージェントをダウンロードしてインストールする**リンクを選択します。 

    >**重要:** 別の仮想マシンで実行される次のタスク内の手順があります。

1. **[Linux サーバー]** のタブを選択します。

    >仮想マシン名の参照を探します。

1. *Linux 用のダウンロードおよびオンボード エージェント*領域のコマンドをクリップボードにコピーします。

1. Launch your LIN2 virtual machine. Login with the username as password provided by your lab hoster. <bpt id="p1">**</bpt>Hint:<ept id="p1">**</ept> You might need to press the Enter key to see the login prompt.

1. Note the IP address for your LIN2 server. See the screenshot below as an example:

    ![Linux ログイン](../Media/LinuxLoginExample.png)

1. Go back to the <bpt id="p1">**</bpt>WIN1<ept id="p1">**</ept> virtual machine. Select the Windows PowerShell used in the previous task.

1. 次の PowerShell コマンドを入力し、特定の Linux サーバー情報に合わせて調整し、Enter キーを押します。

    ```PowerShell
    ssh insert-your-linux-IP-address-here -l insert-linux-user-name-here
    ```

1. Enter <bpt id="p1">*</bpt>yes<ept id="p1">*</ept> to confirm the connection and then type the user's password and press enter. Your screen should look something like this:

    ![Linux ログイン](../Media/PSconnectLinux.png)

1. You are now ready to paste the <bpt id="p1">*</bpt>Download and onboard agent for Linux<ept id="p1">*</ept> command from the earlier step. Make sure that script is in the clipboard. In PowerShell right-click the top bar and choose <bpt id="p1">**</bpt>Edit<ept id="p1">**</ept> and then <bpt id="p2">**</bpt>Paste<ept id="p2">**</ept>.

1. Once the script is pasted, press Enter. The script will run against your Linux server remotely. Wait

1. 終了したら、「**exit**」と入力して、LIN2 へのリモート シェル接続を閉じます。


### <a name="task-4-configure-the-facilities-you-want-to-collect-and-their-severities-for-the-syslog-connector"></a>タスク 4:収集する設備とその重大度を Syslog コネクタ用に設定する

このタスクでは、Syslog収集機能を構成します。

1. Microsoft Sentinel ポータルが開いている Edge ブラウザーに戻り、右上隅にある [x] を 2 回選択して [Log Analytics ワークスペース] ページと [Syslog] データ コネクタ ページを閉じます。

1. Microsoft Sentinel ポータルで、 *[構成]* の下の **[設定]** を選択し、 **[ワークスペースの設定]** タブをクリックします。

1. **[設定]** 領域で、 **[レガシ エージェントの管理]** を選びます。

1. **[Syslog]** タブを選択します。

1. **[+ 設備の追加]** ボタンを選択します。

1. *[施設名]* ドロップダウン メニューから [**認証]** を選択します。

1. **[+ 設備の追加]** ボタンをもう一度選択します。

1. *[施設名]* ドロップダウン メニューから **[authpriv]** を選択します。

1. **[適用]** を選択して変更を保存します。

## <a name="proceed-to-exercise-4"></a>演習 4 に進む
