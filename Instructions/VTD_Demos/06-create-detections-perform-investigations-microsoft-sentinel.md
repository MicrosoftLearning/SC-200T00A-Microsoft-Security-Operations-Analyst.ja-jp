# モジュール 6 Microsoft Sentinel を使用して検出を作成し、調査を実行する

**注**: このデモを正常に完了するには、[前提条件ドキュメント](00-prerequisites.md)のすべての手順を完了する必要があります。 

## Azure Monitor エージェント (AMA) で構成された攻撃の検出 Windows

このタスクでは、次のことを行います。 

1. 管理者として WIN1 仮想マシンにログインします。パスワードは**Pa55w.rd**。  

1. Edge ブラウザーで、Azure portal (https://portal.azure.com ) に移動します。

1. **サインイン** ダイアログ ボックスで、ラボのホスティングプロバイダーから提供された管理者用の**テナント電子メール** アカウントをコピーして貼り付け、 **[次へ]** を選択します。

1. **パスワードの入力**ダイアログ ボックスで、ラボ ホスティング プロバイダーから提供された管理者用の**テナントパスワード**をコピーして貼り付け、 **[サインイン]** を選択します。

1. Azure portal の検索バーに「*Sentinel*」と入力してから、**[Microsoft Sentinel]** を選択します。

1. 先ほど作成した Microsoft Sentinel ワークスペースを選択します。

1. `Microsoft Sentinel` で、`Threat management` メニュー セクションに移動し、 **[インシデント]** を選択します

1. 作成した `NRT` ルールで構成した `Severity` と `Title` に一致するインシデントが表示されます

1. `Incident` を選択すると、`detail` ウィンドウが開きます

1. `Owner` 割り当ては **Operator1** で、`Automation rule` から作成され、`Tactics and techniques` は (`NRT` ルールからの) **特権エスカレーション** である必要があります

1. **[完全な詳細の表示]** を選択して、すべての `Incident management` 機能と `Incident actions` を表示します

## デモが完了しました
