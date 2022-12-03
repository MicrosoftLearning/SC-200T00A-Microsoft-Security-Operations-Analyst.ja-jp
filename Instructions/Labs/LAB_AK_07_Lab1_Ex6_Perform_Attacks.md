---
lab:
  title: 演習 6 - 攻撃の実施
  module: Learning Path 7 - Create detections and perform investigations using Microsoft Sentinel
---

# <a name="learning-path-7---lab-1---exercise-6---conduct-attacks"></a>ラーニング パス 7 - ラボ 1 - 演習 6 - 攻撃の実施

## <a name="lab-scenario"></a>ラボのシナリオ

![ラボの概要。](../Media/SC-200-Lab_Diagrams_Mod7_L1_Ex5.png)

後で Microsoft Sentinel での検出と調査に使用する攻撃をシミュレートします。


### <a name="task-1-attack-windows-configured-with-defender-for-endpoint"></a>タスク 1:Defender for Endpoint で構成された Windows を攻撃する

このタスクでは、Microsoft Defender for Endpoint が構成されているホストに対して攻撃を実行します。

1. 管理者として WIN1 仮想マシンにログインします。パスワードは**Pa55w.rd**。  

1. タスク バーの検索で、*Command* と入力します。 検索結果にコマンド プロンプトが表示されます。 コマンド プロンプトを右クリックして、 **[管理者として実行]** を選択します。 表示される [ユーザー アカウント制御] ウィンドウで **[はい]** を選択し、アプリを実行できるようにします。

1. コマンド プロンプトで、ルート ディレクトリに Temp フォルダーを作成します。 最後の行の後で忘れずに Enter キーを押してください。

    ```CommandPrompt
    cd \
    mkdir temp
    cd temp
    ```

#### <a name="attack-1---persistence-with-registry-key-add"></a>攻撃 1 - レジストリ キーの追加による永続性

1. 次のコマンドをコピーして実行し、プログラムの永続化をシミュレートします。

    ```CommandPrompt
    REG ADD "HKCU\SOFTWARE\Microsoft\Windows\CurrentVersion\Run" /V "SOC Test" /t REG_SZ /F /D "C:\temp\startup.bat"
    ```

#### <a name="attack-3---dns--c2"></a>攻撃 3 - DNS/C2 

1. 次のコマンドをコピーして実行し、C2 サーバーに対する DNS クエリをシミュレートするスクリプトを作成します。

    ```CommandPrompt
    notepad c2.ps1
    ```

1. **[はい]** を選択して新しいファイルを作成し、以下の PowerShell スクリプトを *c2.ps1* にコピーします。

    >**注:**  仮想マシンへの貼り付けには長さの制限がある場合があります。 スクリプトが *c2.ps1* ファイル内で次の手順のように見えることを確認してください。

    ```PowerShell
    param(
        [string]$Domain = "microsoft.com",
        [string]$Subdomain = "subdomain",
        [string]$Sub2domain = "sub2domain",
        [string]$Sub3domain = "sub3domain",
        [string]$QueryType = "TXT",
        [int]$C2Interval = 8,
        [int]$C2Jitter = 20,
        [int]$RunTime = 240
    )
    $RunStart = Get-Date
    $RunEnd = $RunStart.addminutes($RunTime)
    $x2 = 1
    $x3 = 1 
    Do {
        $TimeNow = Get-Date
        Resolve-DnsName -type $QueryType $Subdomain".$(Get-Random -Minimum 1 -Maximum 999999)."$Domain -QuickTimeout
        if ($x2 -eq 3 )
        {
            Resolve-DnsName -type $QueryType $Sub2domain".$(Get-Random -Minimum 1 -Maximum 999999)."$Domain -QuickTimeout
            $x2 = 1
        }
        else
        {
            $x2 = $x2 + 1
        }    
        if ($x3 -eq 7 )
        {
            Resolve-DnsName -type $QueryType $Sub3domain".$(Get-Random -Minimum 1 -Maximum 999999)."$Domain -QuickTimeout
            $x3 = 1
        }
        else
        {
            $x3 = $x3 + 1
        }
        $Jitter = ((Get-Random -Minimum -$C2Jitter -Maximum $C2Jitter) / 100 + 1) +$C2Interval
        Start-Sleep -Seconds $Jitter
    }
    Until ($TimeNow -ge $RunEnd)
    ```

1. メモ帳のメニューで、 **[ファイル]** 、 **[保存]** の順に選択します。 

1. コマンド プロンプト ウィンドウに戻り、次のコマンドを入力して Enter キーを押します。 

    >**注:**  新しい PowerShell ウィンドウが開き、解決エラーが表示されます。 これは予期されることです。

    ```CommandPrompt
    Start PowerShell.exe -file c2.ps1
    ```

>**重要:** これらのウィンドウを閉じないでください。 この PowerShell スクリプトをバックグラウンドで実行させておきます。 コマンドは、数時間ログエントリを生成する必要があります。 このスクリプトの実行中に次のタスクや次の演習に進むことができます。 このタスクで作成したデータは、後で脅威の捜索ラボで使用します。 このプロセスでは、大量のデータや処理を作成することはありません。


### <a name="task-2-attack-windows-configured-with-microsoft-sentinel-connector"></a>タスク 2:Microsoft Sentinel コネクタを使って構成された Windows を攻撃する

このタスクでは、Microsoft Sentinel のセキュリティ イベント コネクタを使用したホストに対して攻撃を実行します。

>**重要:** 次の手順は、以前に作業していたものとは異なるマシンで行います。 仮想マシン名の参照を探します。

1. 管理者として、次のパスワードを使用して WIN2 仮想マシンにログインします: **Pa55w.rd**。  

>**重要:** ラボの *[SAVE]* 機能により、Win2 が Azure Arc から切断される可能性があります。再起動によってこの問題を解決できます。  

1. Windows で **[開始]** を選択します。 次に、 **[電源]** 、 **[再起動]** の順に選択します。

1. 手順に従って WIN2 にもう一度ログインします。

1. タスク バーの検索で、*Command* と入力します。 検索結果にコマンド プロンプトが表示されます。 コマンド プロンプトを右クリックして、 **[管理者として実行]** を選択します。 表示される [ユーザー アカウント制御] ウィンドウで **[はい]** を選択し、アプリを実行できるようにします。

1. コマンド プロンプトで、ルート ディレクトリに Temp フォルダーを作成します。 最後の行の後で忘れずに Enter キーを押してください。

    ```CommandPrompt
    cd \
    mkdir temp
    cd \temp
    ```

#### <a name="attack-2---user-add-and-elevate-privilege"></a>攻撃 2 - ユーザーが特権を追加および昇格

1. このコマンドをコピーして実行し、管理者アカウントの作成をシミュレートします。 最後の行の後で忘れずに Enter キーを押してください。

    ```CommandPrompt
    net user theusernametoadd /add
    net user theusernametoadd ThePassword1!
    net localgroup administrators theusernametoadd /add
    ```

## <a name="proceed-to-exercise-7"></a>演習 7 に進む
