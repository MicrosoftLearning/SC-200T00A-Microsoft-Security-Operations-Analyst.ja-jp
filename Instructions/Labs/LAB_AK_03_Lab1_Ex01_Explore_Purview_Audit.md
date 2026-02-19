---
lab:
  title: 演習 1 - Microsoft Purview 監査ログについて調べる
  module: Learning Path 3 - Mitigate threats using Microsoft Purview
---

# ラーニング パス 3 - ラボ 1 - 演習 1 - Microsoft Purview 監査ログについて調べる

## ラボのシナリオ

あなたは、Microsoft Defender XDR と Microsoft Purview を実装している会社で働いているセキュリティ運用アナリストです。 あなたは、It コンプライアンス チームの同僚が Purview 監査 (Standard) と Purview 監査 (Premium) の両方を構成するのを支援しています。 同僚の目的は、医療施設ネットワークに存在する患者データへのあらゆるアクセスと変更が正確にログに記録されて、健康データ保護規則を確実に満たすようにすることです。

>[警告] エラー メッセージが表示され、この演習で監査記録を開始できない場合は、次の手順を回避策として使用してください。
>
>1. Windows 検索フォームに「*PowerShell*」と入力して管理者特権の PowerShell セッションを開いてから、**[管理者として実行]** を選択します。
>1. `Install-Module -Name ExchangeOnlineManagement` を実行して ExchangeOnlineManagement モジュールをインストールします
>1. `Connect-ExchangeOnline` を実行して ExchangeOnlineManagement に接続します
>1. メッセージが表示されたら、ラボ ホスティング プロバイダーから管理者のユーザー名とパスワードを入力してログインします。
>1. 監査が有効になっているかどうかを確認するには、`Get-AdminAuditLogConfig | FL UnifiedAuditLogIngestionEnabled` を実行します
>1. false の場合、監査ログはオフになります。
>1. 監査を有効にするには、`Set-AdminAuditLogConfig -UnifiedAuditLogIngestionEnabled $true` を実行します
>1. 組織内でスクリプトを実行できないというエラーが表示された場合は、`Enable-OrganizationCustomization` を実行します
>1. もう一度 `Set-AdminAuditLogConfig -UnifiedAuditLogIngestionEnabled $true` の実行をお試しください
>1. 監査が有効になっていることを確認するには、`Get-AdminAuditLogConfig | FL UnifiedAuditLogIngestionEnabled` を実行します
>1. 完了したら、`Disconnect-ExchangeOnline` を実行してセッションを終了します

### このラボの推定所要時間: 15 分

### タスク 1: Purview 監査ログを有効にする

このタスクでは、Microsoft 365 セキュリティ ポータルで Exchange Online Protection (EOP) と Microsoft Defender for Office 365 の事前設定セキュリティ ポリシーを割り当てます。

1. 管理者として WIN1 仮想マシンにログインします。パスワードは**Pa55w.rd**。  

1. 新しい Microsoft Edge ブラウザーを起動します。

1. Microsoft Edge ブラウザーで、Microsoft Defender XDR ポータル (<https://security.microsoft.com>) にアクセスします。

1. **サインイン** ダイアログ ボックスで、ラボ ホスティング プロバイダーの提供した管理者ユーザー名のテナント電子メール アカウントをコピーして貼り付け、**[次へ]** を選択します。

1. **パスワードの入力**ダイアログ ボックスで、ラボ ホスティング プロバイダーの提供した管理者のテナント パスワードをコピーして貼り付け、**サインイン**します。

1. ナビゲーション メニューから **[その他のリソース]** を選択します。

1. **[その他のリソース]** ペインで、*[Microsoft Purview ポータル]* タイルの **[開く]** ボタンを選択します。

1. Microsoft Purview ポータルが開くと、*コンプライアンス ポータルが廃止された*ことを示すメッセージが表示されます。 このメッセージはタイムアウトになり、新しい *Microsoft Purview ポータル*にリダイレクトされます。

1. *"新しい Microsoft Purview ポータルへようこそ"* というメッセージで、データ フロー開示の条件とプライバシーに関する声明に同意する選択肢を選択し、**[今すぐ試す]** を選択します。

    ![[ようこそ新しい Microsoft Purview ポータルへ] 画面のスクリーンショット。](../Media/welcome-purview-portal.png)

1. 左側のサイド バーから **[ソリューション]** を選択し、**[監査]** を選択します。

1. **[検索]** ページで、青色の **[ユーザーと管理者のアクティビティの記録を開始する]** バーを選択して監査ログを有効にします。

    ![[ユーザーと管理者のアクティビティの記録を開始する] ボタンを示すスクリーンショット。](../Media/enable-audit-button.png)

1. このオプションを選択すると、このページに青いバーが表示されなくなるはずです。

    >**注:** アクティビティの記録が開始されるまで、60 分かかる場合があります。

## これでラボは完了です
