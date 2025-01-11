---
lab:
  title: 演習 1 - Microsoft Defender for Endpoint のデプロイ
  module: Learning Path 4 - Mitigate threats using Microsoft Defender for Endpoint
---

# ラーニング パス 4: ラボ 1: 演習 1: Microsoft Defender for Endpoint のデプロイ

## ラボのシナリオ

![ラボの概要。](../Media/SC-200-Lab_Diagrams_Mod2_L1_Ex1.png)

あなたは Microsoft Defender for Endpoint を実装している企業で働いているセキュリティ運用アナリストです。 あなたの上司は、いくつかのデバイスをオンボードして、セキュリティ オペレーション (SecOps) チームの応答手順で必要な変更に関する情報を提供しようとしています。

最初に、Defender for Endpoint 環境を初期化します。 次に、デバイスでオンボード スクリプトを実行し、デプロイ対象の初期デバイスをオンボードします。 環境のセキュリティを構成します。 最後に、デバイス グループを作成し、適切なデバイスを割り当てます。

>**重要:** ラボの Virtual Machines は、さまざまなモジュールで使用されます。 仮想マシンを保存します。 保存せずにラボを終了する場合は、構成を再実行する必要があります。

>**注:** 最初のモジュールのタスク 3 の手順が正常に完了していることを確認します。

### このラボの推定所要時間: 30 分

### タスク 1:Microsoft Defender for Endpoint の初期化

このタスクでは、Microsoft Defender for Endpoint の初期化を行います。

1. 管理者として **WIN1** 仮想マシンにサインインします。パスワードは **Pa55w.rd** です。  

1. Microsoft Defender XDR ポータルにまだアクセスしていない場合は、Microsoft Edge ブラウザーを起動します。

1. Microsoft Edge ブラウザーで、(<https://security.microsoft.com>) の Microsoft Defender XDR ポータルに移動します。

1. **サインイン** ダイアログ ボックスで、ラボ ホスティング プロバイダーの提供した管理者ユーザー名のテナント電子メール アカウントをコピーして貼り付け、**[次へ]** を選択します。

1. **パスワードの入力**ダイアログ ボックスで、ラボ ホスティング プロバイダーの提供した管理者のテナント パスワードをコピーして貼り付け、**サインイン**します。

    >**ヒント:** 管理者のテナントのメール アカウントとパスワードは、[リソース] タブで確認できます。

1. **Defender XDR** ポータルで、左側のナビゲーション メニューから下にスクロールし、**[システム]** セクションを展開し、**[設定]** を選択します。

    >**注:** ポータルの一部のバージョンでは、**[システム]** セクションの下に **[設定]** オプションがない場合があります。 **[設定]** は、*[レポート]* と *[監査]* でグループ化できます。

1. [設定] ページで、 **[デバイス検出]** を選択します。

    >**注:**  **[設定]** の下に **[デバイス検出]** オプションが表示されない場合は、ご自分のアカウントのイニシャルが表示された右上の円をクリックしてログアウトし、 **[サインアウト]** をクリックします。試すことのできるもう 1 つのオプションは、Ctrl + F5 キーを使用してページを更新するか、InPrivate ページを開くことです。 **テナントの電子メール**資格情報を使用して再度ログインします。

1. [検出] 設定で、**[Standard discovery (recommended)] (標準検出 (推奨))** が選択されていることを確認します。 

    >**ヒント:** オプションが表示されない場合は、ページを更新してください。

### タスク 2: デバイスのオンボード

このタスクでは、オンボード スクリプトを使用してデバイスを Microsoft Defender for Endpoint にオンボードします。

1. **Defender XDR** ポータルで、左側のナビゲーション メニューから下にスクロルし、**[システム]** セクションを展開して **[設定]** を選択した後、[設定] ページから **[エンドポイント]** を選択します。

1. デバイス管理セクションで **[オンボーディング]** を選択します。

    >**メモ:** 左側のメニュー バーの **[アセット]** セクションからデバイスのオンボードを実行することもできます。 [アセット] を展開し、[デバイス] を選択します。 [デバイス インベントリ] ページで、[コンピューター] と [モバイル] が選択された状態で、 **[デバイスのオンボード]** まで下にスクロールします。 そうすると、 **[設定] > [エンドポイント]** ページが表示されます。

1. [1. オンボード デバイス] 領域で、デプロイ方法ドロップダウンにローカル スクリプト (最大 10 デバイス) が表示されていることを確認し、**[オンボーディング パッケージのダウンロード]** ボタンを選択します。

1. *[ダウンロード]* ポップアップで、マウスを使用して "WindowsDefenderATPOnboardingPackage.zip" ファイルを強調表示し、フォルダー アイコン **[フォルダーに表示]** を選択します。 **ヒント:** 表示されない場合は、ファイルを c:\users\admin\downloads ディレクトリに配置してください。

    >**ヒント:** ブラウザーでダウンロードがブロックされた場合は、ブラウザーで許可するように対処してください。 Microsoft Edge ブラウザーで、"*WindowsDefenderATPOnboardingPackage.zip は通常ダウンロードされません。... を信頼済みであることを確認してください*" というメッセージが表示されることがあります。必要に応じて省略記号ボタン (...) を選択し、 **[保持]** を選びます。 Microsoft Edge では、2 つ目のポップアップが "*開く前に、WindowsDefenderATPOnboardingPackage.zip を信頼済みであることを確認してください*" というメッセージと共に表示されます。 **[詳細を表示]** を選んで選択内容を展開し、 **[そのまま保持]** を選択します。

1. ダウンロードした zip ファイルを右クリックし、 **[すべて展開]** を選択し、 *[完了時に展開されたファイルを表示する]* チェックボックスがオンになっていることを確認し、 **[抽出]** を選択します。

1. 抽出されたファイル "WindowsDefenderATPLocalOnboardingScript.cmd" を右クリックし、**[プロパティ]** を選択します。 [プロパティ] ウィンドウの右下にある **[ブロック解除]** チェックボックスをオンにして、**[OK]** を選択します。

1. 抽出されたファイル "WindowsDefenderATPLocalOnboardingScript.cmd" を右クリックし、 **[管理者として実行]** を選択します。  **ヒント:** Windows SmartScreen ウィンドウが表示されたら、 **[詳細情報]** を選択し、 **[実行]** を選択します。

1. [ユーザー アカウント制御] ウィンドウが表示されたら、 **[はい]** を選択してスクリプトの実行を許可し、スクリプトによって示される質問に **Y** と回答して、**Enter** キーを押します。 完了したら、コマンド画面に "マシンの Microsoft Defender for Endpoint へのオンボードに成功しました" という内容のメッセージが表示されます。**

1. 任意のキーを押して続行します。 これで、コマンド プロンプト ウィンドウが閉じます。

### タスク 3:ロールの構成

このタスクでは、デバイス グループで使用するロールを設定します。

1. Microsoft Defender XDR ポータルの左側のメニュー バーで、**[システム]** セクションを展開して **[設定]** を選択した後、**[エンドポイント]** を選択します。

1. [アクセス許可] 領域で、**[ロール]** を選択します。

1. **[ロールをオンにする]** ボタンを選択します。

1. **[+ ロールの追加]** を選択します。

1. [ロールの追加] ダイアログで、以下を入力します。

    |全般設定|値|
    |---|---|
    |ロール名|**第一層サポート**|
    |アクセス許可|ライブ応答機能 - 詳細設定|

1. [**次へ**] を選択します。

1. **[割り当てられたユーザー グループ]** ページで、*フィルター ユーザー グループ* フォームに「**sg-IT**」と入力し、**[選択したグループを追加する]** を選択します。 これが *[Azure AD user groups with this role](このロールを持つ Azure AD ユーザー グループ)* の下に表示されることを確認します。

1. **[送信]** を選び、完了したら **[完了]** を選択します。

    >**注:** "*UserAuthEnforcementMode は Rbac であるため、ユーザーはこのアクションを実行できません。このアクションには RbacV2 のいずれかが必要です*" というエラーが表示された場合は、 **[ OK]** を選択してもう一度やり直してください。

### タスク 4:デバイス グループの構成

このタスクでは、アクセスの制御と自動化の構成が可能なデバイス グループを構成します。

1. Microsoft Defender XDR ポータルの左側のメニュー バーで、**[システム]** セクションを展開して **[設定]** を選択した後、**[エンドポイント]** を選択します。

1. アクセス許可領域で **[デバイス グループ]** を選択します。

1. **[デバイス グループの追加]** アイコンを選択します。

1. 全般 タブに次の情報を入力します。

    |全般設定|値|
    |---|---|
    |デバイス グループ名|**Regular**|
    |修復レベル|Full - remediate threats automatically (完全 - 脅威を自動的に修復する)|

1. **[次へ]** を選択します。

1. [デバイス] タブの OS 条件で、**[Windows 10]** を選択し、**[次へ]** を選択します。

    >**注:** 一部のラボ ホスティング プロバイダーでは、WIN1 に *Windows 11* イメージが構成されている場合があります。 いずれかまたは両方を選択できます。

1. [デバイスのプレビュー] タブで、 *[プレビューを表示]* ボタンを使用して、WIN1 仮想マシンを表示できますが、ほとんどの場合、データはまだ設定されていません。 **[次へ]** を選択して続行します。

1. ユーザー アクセス タブで **[sg-IT]** を選択し、**[選択したグループを追加]** ボタンを選択します。 これが *[Azure AD user groups with access to this device group](このデバイス グループへのアクセス権を持つ Azure AD ユーザー グループ)* の下に表示されることを確認します。

1. **[送信]** を選び、完了したら **[完了]** を選択します。

1. これでデバイス グループの構成が変わりました。 **[変更を適用]** を選択して、一致を確認し、グループ化を再計算します。

1. これで、作成した "Regular" と "グループに属していないデバイス (既定)" という 2 つのデバイス グループが同じ修復レベルで表示されます。

## 演習 2 に進みます。