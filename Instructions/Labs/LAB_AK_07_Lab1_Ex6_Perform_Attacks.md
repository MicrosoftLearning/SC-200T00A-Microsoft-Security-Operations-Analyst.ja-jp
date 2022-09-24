---
lab:
  title: 演習 6 - 攻撃の実施
  module: Module 7 - Create detections and perform investigations using Microsoft Sentinel
---

# <a name="module-7---lab-1---exercise-6---conduct-attacks"></a>モジュール 7 - ラボ 1 - 演習 6 - 攻撃の実施

## <a name="lab-scenario"></a>ラボのシナリオ

![ラボの概要。](../Media/SC-200-Lab_Diagrams_Mod7_L1_Ex5.png)

後で Microsoft Sentinel での検出と調査に使用する攻撃をシミュレートします。


### <a name="task-1-attack-windows-configured-with-defender-for-endpoint"></a>タスク 1:Defender for Endpoint で構成された Windows を攻撃する

このタスクでは、Microsoft Defender for Endpoint が構成されているホストに対して攻撃を実行します。

1. 管理者として WIN1 仮想マシンにログインします。パスワードは**Pa55w.rd**。  

1. In the search of the task bar, enter <bpt id="p1">*</bpt>Command<ept id="p1">*</ept>. Command Prompt will be displayed in the search results. Right-click on the Command Prompt and select <bpt id="p1">**</bpt>Run as Administrator<ept id="p1">**</ept>. Select <bpt id="p1">**</bpt>Yes<ept id="p1">**</ept> in the User Account Control window that appears to allow the app to run.

1. In the Command Prompt, create a Temp folder in the root directory. Remember to press Enter after the last row:

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

    ><bpt id="p1">**</bpt>Note:<ept id="p1">**</ept> Paste into the virtual machine might have a limited length. Make sure the script looks as it does in these instructions within the <bpt id="p1">*</bpt>c2.ps1<ept id="p1">*</ept> file.

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

    ><bpt id="p1">**</bpt>Note:<ept id="p1">**</ept> A new PowerShell window will open and you will see resolve errors. This is expected.

    ```CommandPrompt
    Start PowerShell.exe -file c2.ps1
    ```

><bpt id="p1">**</bpt>Important:<ept id="p1">**</ept> Do not close these windows. Let this PowerShell script run in the background. The command needs to generate log entries for some hours. You can proceed to the next task and next exercises while this script runs. The data created by this task will be used in the Threat Hunting lab later. This process will not create substantial amounts of data or processing.


### <a name="task-2-attack-windows-configured-with-microsoft-sentinel-connector"></a>タスク 2:Microsoft Sentinel コネクタを使って構成された Windows を攻撃する

このタスクでは、Microsoft Sentinel のセキュリティ イベント コネクタを使用したホストに対して攻撃を実行します。

><bpt id="p1">**</bpt>Important:<ept id="p1">**</ept> The next steps are done in a different machine than the one you were previously working. Look for the Virtual Machine name references.

1. 管理者として、次のパスワードを使用して WIN2 仮想マシンにログインします: **Pa55w.rd**。  

>**重要:** ラボの *[SAVE]* 機能により、Win2 が Azure Arc から切断される可能性があります。再起動によってこの問題を解決できます。  

1. Select <bpt id="p1">**</bpt>Start<ept id="p1">**</ept> in Windows. Then <bpt id="p1">**</bpt>Power<ept id="p1">**</ept>, next <bpt id="p2">**</bpt>Restart<ept id="p2">**</ept>
1. 手順に従って WIN2 にもう一度ログインします。


1. In the search of the task bar, enter <bpt id="p1">*</bpt>Command<ept id="p1">*</ept>. Command Prompt will be displayed in the search results. Right-click on the Command Prompt and select <bpt id="p1">**</bpt>Run as Administrator<ept id="p1">**</ept>. Select <bpt id="p1">**</bpt>Yes<ept id="p1">**</ept> in the User Account Control window that appears to allow the app to run. <bpt id="p1">**</bpt>Hint:<ept id="p1">**</ept> You might have a Command Prompt as Administrator open from a previous exercise.

1. In the Command Prompt, create a Temp folder in the root directory. Remember to press Enter after the last row:

    ```CommandPrompt
    cd \
    mkdir temp
    cd \temp
    ```

#### <a name="attack-2---user-add-and-elevate-privilege"></a>攻撃 2 - ユーザーが特権を追加および昇格

1. タスク バーの検索で、*Command* と入力します。

    ```CommandPrompt
    net user theusernametoadd /add
    net user theusernametoadd ThePassword1!
    net localgroup administrators theusernametoadd /add
    ```

## <a name="proceed-to-exercise-7"></a>演習 7 に進む
