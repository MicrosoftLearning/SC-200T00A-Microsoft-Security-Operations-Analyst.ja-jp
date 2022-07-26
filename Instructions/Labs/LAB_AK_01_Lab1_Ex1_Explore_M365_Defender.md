---
lab:
  title: 演習 1 - Microsoft 365 Defender の確認
  module: Module 1 - Mitigate threats using Microsoft 365 Defender
ms.openlocfilehash: dc37672bc32d41439aec72056ed1530196cbcfc6
ms.sourcegitcommit: a90325f86a3497319b3dc15ccf49e0396c4bf749
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/07/2022
ms.locfileid: "141493836"
---
# <a name="module-1---lab-1---exercise-1---explore-microsoft-365-defender"></a>モジュール 1 - ラボ 1 - 演習 1 - Microsoft 365 Defender の確認 

## <a name="lab-scenario"></a>ラボのシナリオ

![M365 Defender](../Media/SC-200-Lab_M1_L1_Ex1.png)

あなたは Microsoft 365 Defender を実装している企業で働くセキュリティ オペレーションアナリストです。 まず、EOP と Microsoft Defender for Office 365 で事前設定されたセキュリティ ポリシーを割り当てます。


### <a name="task-1-obtain-your-microsoft-365-credentials"></a>タスク 1:Microsoft 365 資格情報の取得

ラボを起動すると、無料のトライアル テナントを利用して Microsoft Virtual Lab 環境にアクセスできるようになります。 このテナントには自動的に一意のユーザー名とパスワードが割り当てられます。 Microsoft Virtual Lab 環境で Azure と Microsoft 365 にサインインするには、このユーザー名とパスワードを取得する必要があります。 

このコースは、学習パートナーが複数の認証済みラボ ホスティング プロバイダーのいずれかを使用して実施することもあり、お使いになっているテナントに関連のあるテナント ID を取得する実際の手順はラボ ホスティング プロバイダーに応じて異なります。 このため、コース内での当該情報の取得方法については、講師が必要な指示を行います。 後ほど使用できるよう以下の情報に留意してください。

- **テナント サフィックス ID。** この ID は、ラボ全体で Microsoft 365 にサインインする際に使用する onmicrosoft.com アカウント用です。 これは **{username}@ZZZZZZ.onmicrosoft.com** の形式です。ここで、ZZZZZZ はラボ ホスティング プロバイダーから提供される一意のテナント サフィックス ID です。 後で使用できるよう、この ZZZZZZ を記録しておきます。 ラボの手順で Microsoft 365 ポータルにサインインするよう指示されたら、ここで取得した ZZZZZZ の値を入力してください。
- **テナント パスワード:** これは、ラボ ホスティング プロバイダーの提供する管理者アカウント向けのパスワードです。


### <a name="task-2-apply-microsoft-defender-for-office-365-preset-security-policies"></a>タスク 2:Microsoft Defender for Office 365 の事前設定セキュリティ ポリシーを適用する

このタスクでは、Microsoft 365 セキュリティ ポータルで EOP と Microsoft Defender for Office 365 の事前設定セキュリティ ポリシーを割り当てる必要があります。

1. 管理者として WIN1 仮想マシンにログインします。パスワードは **Pa55w.rd**。  

1. 新しい Microsoft Edge ブラウザーを起動します。

1. Edge ブラウザーで、 https://security.microsoft.com の Microsoft 365 Defender ポータルに移動します。

1. **サインイン** ダイアログ ボックスで、ラボ ホスティング プロバイダーの提供した管理者ユーザー名のテナント電子メール アカウントをコピーして貼り付け、「**次へ**」を選択します。

1. **パスワードの入力** ダイアログ ボックスで、ラボ ホスティング プロバイダーの提供した管理者のテナント パスワードをコピーして貼り付け、**サインイン** します。

    >**注:** "このセクションにアクセスできません" というメッセージが表示されたら、 5 分間待ち、再試行してください。 アクセス ルールがテナントを伝播する必要がある場合があり、これには数分かかる場合があります。  

1. 表示されている場合は、Microsoft 365 Defender クイック ツアーを閉じます。

1. ナビゲーション メニューの **[Email & Collaboration/電子メールとコラボレーション]** 領域で、 **[Policies & rules]\(ポリシーとルール\)** を選択します。

1. *[Policies & rules]\(ポリシーとルール\)*  ダッシュボードで、 **[Threat policies]\(脅威ポリシー\)** を選択します。

1. *Threat policies\(脅威ポリシー\)* ダッシュボードで、**Preset Security Policies (事前設定セキュリティ ポリシー)** を選択します。

    >**注:**  "クライアント エラー - bip ルールの取得時にエラーが発生しました" というメッセージが表示された場合は、 **[OK]** を選択して続行します。 このエラーは、既定では有効になっていない Office 365 のテナントのハイドレーション状態が原因です。

1. [Standard Protection/標準的な保護] の **[Manage/管理]** を選択します。

1. *[EOP protections apply to]\(EOP 保護の適用先\)* セクションの **[Domain/ドメイン]** で、テナントのドメイン名を記述し、 **[Next/次へ]** を選択します。 **ヒント:** テナントのドメイン名は、管理者アカウントのドメイン名と同じです。例: *WWLx######.onmicrosoft.com*。 この構成では、**スパム対策、送信スパム フィルター、マルウェア対策、フィッシング対策**のポリシーが適用されます。 

1. **[Defender for Office 365 protections apply to]\(Defender for Office 365 保護の適用先\)** セクションで、前の手順と同じ構成を適用し、 *[次へ]* を選択します。 この構成は、**フィッシング対策、安全な添付ファイル、安全なリンクのポリシー** に対して適用されることに注意してください。

1. *[Review and confirm your changes]\(確認と変更の確認\)* の内容を読み、 **[Confirm/確認]** を選択して変更を適用し、 **[Done/完了]** を選択して完了します。

1. *[Strict protection/厳密な保護]* で **[Manage/管理]** を選択します。 **ヒント:** *[厳密な保護]* は、"[電子メールとコラボレーション] - [Policies & rules]\(ポリシーとルール\) - [Threat policies]\(脅威ポリシー\) - [Preset Security Policies] (事前設定セキュリティ ポリシー)" の下に表示されます。

1. *[EOP protections apply to]\(EOP 保護の適用先\)* の **[グループ]** で、 **Leadership** と記述し、それを選択して **[次へ]** を選択します。 この構成では、スパム対策、送信スパム フィルター、マルウェア対策、フィッシング対策のポリシーが適用されます。

1. **[Defender for Office 365 protections apply to]\(Defender for Office 365 保護の適用先\)** セクションで、前の手順と同じ構成を適用し、 *[次へ]* を選択します。 この構成は、フィッシング対策、安全な添付ファイル、安全なリンクのポリシーに対して適用されることに注意してください。

1. *[Review and confirm your changes]\(確認と変更の確認\)* の内容を読み、 **[確認]** を選択して変更を適用し、 **[完了]** を選択して完了します。

1. 上部の中央のメニューで **[Threat policies]\(脅威ポリシー\)** を選択して戻り、 *[ポリシー]* の下にある **[安全な添付ファイル]** を選択します。 両方の事前設定ポリシーがここに表示され、[状態] が [オン] であることに注意してください。

1. メニューで、 **[グローバル設定]** の **歯車** アイコンを選択します。

1. 使用可能な統合オプションを読み、 **[キャンセル]** を選択して戻ります。

1. **[Microsoft 365 Defender]** ポータルのナビゲーション メニューで、左側の **[設定]** を選択します。

1. **[設定]** ページで、 **[Microsoft 365 Defender]** を選択します。 コーヒー カップの画像と、次のメッセージが表示されます。"お待ちください。 データ用の新しいスペースを準備し、それらを接続しています。" 完了するまで数分かかるので、次のラボまでページを開いたままにしてください。 

    >**注:**  "失敗するつもりはありませんでしたが、問題が発生しました" というエラー メッセージが表示された場合は、 後で手順を再試行するか、次のラボの前に実行します。

1. 新しいスペースが正常に完了すると、アカウント、電子メール通知、プレビュー機能、ストリーミング API の Microsoft 365 Defender 設定が表示されます。

## <a name="you-have-completed-the-lab"></a>これでラボは完了です。
