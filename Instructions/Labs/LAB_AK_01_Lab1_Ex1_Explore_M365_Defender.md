---
lab:
  title: 演習 1 - Microsoft 365 Defender の確認
  module: Module 1 - Mitigate threats using Microsoft 365 Defender
---

# <a name="module-1---lab-1---exercise-1---explore-microsoft-365-defender"></a>モジュール 1 - ラボ 1 - 演習 1 - Microsoft 365 Defender の確認 

## <a name="lab-scenario"></a>ラボのシナリオ

![M365 Defender](../Media/SC-200-Lab_M1_L1_Ex1.png)

You are a Security Operations Analyst working at a company that is implementing Microsoft 365 Defender. You start by assigning preset security policies in EOP and Microsoft Defender for Office 365.


### <a name="task-1-obtain-your-microsoft-365-credentials"></a>タスク 1:Microsoft 365 資格情報の取得

Once you launch the lab, a free trial tenant will be made available to you to access in the Microsoft virtual Lab environment. This tenant will be automatically assigned a unique username and password. You must retrieve this username and password so that you can sign into Azure and Microsoft 365 within the Microsoft Virtual Lab environment. 

Because this course can be offered by learning partners using any one of several Authorized Lab Hosting (ALH) providers, the actual steps involved to retrieve the tenant ID associated with your tenant may vary by lab hosting provider. Therefore, your instructor will provide you with the necessary instructions for how to retrieve this information for your course. The information that you should note for later use includes:

- <bpt id="p1">**</bpt>Tenant suffix ID.<ept id="p1">**</ept> This ID is for the onmicrosoft.com accounts that you will use to sign into Microsoft 365 throughout the labs. This is in the format of <bpt id="p1">**</bpt>{username}<ph id="ph1">@ZZZZZZ.onmicrosoft.com</ph><ept id="p1">**</ept>, where ZZZZZZ is your unique tenant suffix ID provided by your lab hosting provider. Record this ZZZZZZ value for later use. When any of the lab steps direct you to sign into Microsoft 365 portals, you must enter the ZZZZZZ value that you obtained here.
- <bpt id="p1">**</bpt>Tenant password.<ept id="p1">**</ept> This is the password for the admin account provided by your lab hosting provider.


### <a name="task-2-apply-microsoft-defender-for-office-365-preset-security-policies"></a>タスク 2:Microsoft Defender for Office 365 の事前設定セキュリティ ポリシーを適用する

このタスクでは、Microsoft 365 セキュリティ ポータルで Exchange Online Protection (EOP) と Microsoft Defender for Office 365 の事前設定セキュリティ ポリシーを割り当てます。

1. 管理者として WIN1 仮想マシンにログインします。パスワードは**Pa55w.rd**。  

1. 新しい Microsoft Edge ブラウザーを起動します。

1. Edge ブラウザーで、 https://security.microsoft.com) の Microsoft 365 Defender ポータルに移動します。

1. **[サインイン]** ダイアログ ボックスで、ラボ ホスティング プロバイダーから提供された管理者ユーザー名のテナント電子メール アカウントをコピーして貼り付け、**[次へ]** を選択します。

1. **パスワードの入力**ダイアログ ボックスで、ラボ ホスティング プロバイダーの提供した管理者のテナント パスワードをコピーして貼り付け、**サインイン**します。

    >あなたは Microsoft 365 Defender を実装している企業で働くセキュリティ オペレーションアナリストです。  

1. 表示されている場合は、Microsoft 365 Defender クイック ツアーを閉じます。

1. ナビゲーション メニューの *[電子メールとコラボレーション]* 領域で、**[Policies & rules]\(ポリシーとルール\)** を選択します。

1. *[Policies & rules]\(ポリシーとルール\) * ダッシュボードで、**[Threat policies]\(脅威ポリシー\)** を選択します。

1. *[Threat policies]\(脅威ポリシー\)]* ダッシュボードで、**[Preset Security Policies] (事前設定セキュリティ ポリシー)** を選択します。

    >まず、EOP と Microsoft Defender for Office 365 で事前設定されたセキュリティ ポリシーを割り当てます。

    ><bpt id="p1">**</bpt>Note:<ept id="p1">**</ept> If you receive the message <bpt id="p2">*</bpt>"Client Error - An error occurred when retrieving preset security policies. Please try again later."<ept id="p2">*</ept> select <bpt id="p1">**</bpt>OK<ept id="p1">**</ept> to continue. Refresh your browser using <bpt id="p1">**</bpt>Ctrl+F5<ept id="p1">**</ept>.

1. Under <bpt id="p1">*</bpt>Standard protection<ept id="p1">*</ept>, select <bpt id="p2">**</bpt>Manage protection settings<ept id="p2">**</ept>. <bpt id="p1">**</bpt>Hint:<ept id="p1">**</ept> If you see this option grayed out, refresh your browser using <bpt id="p2">**</bpt>Ctrl+F5<ept id="p2">**</ept>.

1. ラボを起動すると、無料のトライアル テナントを利用して Microsoft Virtual Lab 環境にアクセスできるようになります。 

1. このテナントには自動的に一意のユーザー名とパスワードが割り当てられます。

1. *[偽装保護]* セクションで、 **[次へ]** を 4 回 (4x) 選択して続行します。

1. *[ポリシー モード]* セクションで、 **[Turn on the policy after I finish]\(完了したらポリシーを有効にする\)** ラジオ ボタンが選択されていることを確認し、 **[次へ]** を選択します。

1. *[変更のレビューと確認]* の内容を読み、 **[確認]** を選択して変更を適用してから、 **[完了]** を選択して完了します。

    >Microsoft Virtual Lab 環境で Azure と Microsoft 365 にサインインするには、このユーザー名とパスワードを取得する必要があります。

1. Under <bpt id="p1">*</bpt>Strict protection<ept id="p1">*</ept>, select <bpt id="p2">**</bpt>Manage protection settings<ept id="p2">**</ept>. <bpt id="p1">**</bpt>Hint:<ept id="p1">**</ept> <bpt id="p2">*</bpt>Strict protection<ept id="p2">*</ept> is found under "Email &amp; Collaboration - Policies &amp; rules - Threat policies - Preset security policies".

1. このコースは、学習パートナーが複数の認証済みラボ ホスティング プロバイダーのいずれかを使用して実施することもあり、お使いになっているテナントに関連のあるテナント ID を取得する実際の手順はラボ ホスティング プロバイダーに応じて異なります。

1. このため、コース内での当該情報の取得方法については、講師が必要な指示を行います。

1. *[偽装保護]* セクションで、 **[次へ]** を 4 回 (4x) 選択して続行します。

1. *[ポリシー モード]* セクションで、 **[Turn on the policy after I finish]\(完了したらポリシーを有効にする\)** ラジオ ボタンが選択されていることを確認し、 **[次へ]** を選択します。

1. *[変更のレビューと確認]* の内容を読み、 **[確認]** を選択して変更を適用してから、 **[完了]** を選択して完了します。

    >後ほど使用できるよう以下の情報に留意してください。

1. **[Microsoft 365 Defender]** ポータルのナビゲーション メニューで、左側の **[設定]** を選択します。

1. On the <bpt id="p1">**</bpt>Settings<ept id="p1">**</ept> page select <bpt id="p2">**</bpt>Microsoft 365 Defender<ept id="p2">**</ept>. You are going to see an image of a coffee mug and a message that reads: "Hang on! We're preparing new spaces for your data and connecting them". It will take several minutes to finish, so leave the page open until the next lab. 

    >**テナント サフィックス ID。**

1. 新しいスペースが正常に完了すると、アカウント、電子メール通知、プレビュー機能、ストリーミング API の Microsoft 365 Defender 設定が表示されます。

## <a name="you-have-completed-the-lab"></a>これでラボは完了です。
