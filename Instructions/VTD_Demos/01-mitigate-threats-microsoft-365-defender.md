# <a name="module-1---mitigate-threats-using-microsoft-365-defender"></a>モジュール 1 - Microsoft 365 Defender を使用して脅威を軽減する

**注**: このデモを正常に完了するには、[前提条件ドキュメント](00-prerequisites.md)のすべての手順を完了する必要があります。 

## <a name="use-the-microsoft-365-defender-portal"></a>Microsoft 365 Defender ポータルを使う

このタスクでは、Microsoft 365 Defender ポータルの機能について理解します。

- ホーム (ダッシュボード)
- インシデントとアラート
- 検出
- アクション センター
- 脅威の分析
- セキュリティ スコア
- エンドポイント
- 脆弱性の管理
- 電子メールとコラボレーション
- クラウド アプリ
- Reports
- 設定
- アクセス許可

1. まだ、Microsoft Defender セキュリティ センターをブラウザーで開いていない場合は、Microsoft Defender セキュリティ センター (https://security.microsoft.com) に移動して、お使いになっているテナントの管理者としてログインします。

1. In the <bpt id="p1">**</bpt>Home<ept id="p1">**</ept> dashboard you can overall view of your secure status. You can customize the view by <bpt id="p1">**</bpt>Add cards<ept id="p1">**</ept> or removing cards. To remove a card, select the ellipsis (...) on a card.
1. Next select <bpt id="p1">**</bpt>Incidents &amp; Alerts<ept id="p1">**</ept>. This will expand the menu choices below. This is where investigations are performed.
1. **[詳細な捜索]** クエリ ページを開くには、 **[ハンティング]** で同じようにします。 
    1. ここで KQL クエリを実行できます。
1. **[Actions & Submissions]\(アクションと送信\)** を選ぶと、 **[アクション センター]** と **[表示]** が開きます
1. Select <bpt id="p1">**</bpt>Threat analytics<ept id="p1">**</ept>. This page provides insights into the Common Vulnerabilities and Exposures (CVE) you need to track
1. Select the <bpt id="p1">**</bpt>Secure Score<ept id="p1">**</ept> and explore the tabs. Take a look at <bpt id="p1">**</bpt>Recommendations<ept id="p1">**</ept> here.
1. Select <bpt id="p1">**</bpt>Endpoints<ept id="p1">**</ept> and <bpt id="p2">**</bpt>Device Inventory<ept id="p2">**</ept> options are available. You can onboard devices here or work with an existing inventory.
1. Also in the <bpt id="p1">**</bpt>Endpoints<ept id="p1">**</ept> section is <bpt id="p2">**</bpt>Vulnerability management<ept id="p2">**</ept>. Vulnerability management has a Dashboard where yu can look review your Exposure score.
1. Another capability within <bpt id="p1">**</bpt>Endpoints<ept id="p1">**</ept> is <bpt id="p2">**</bpt>Evaluations &amp; simulations<ept id="p2">**</ept>. The <bpt id="p1">**</bpt>Evaluation lab<ept id="p1">**</ept> allows you to setup isolated devices for exploring malware.
1. In the <bpt id="p1">**</bpt>Email &amp; collaboration<ept id="p1">**</ept> section are the Defender for Office 365 capabilities. <bpt id="p1">**</bpt>Investigations<ept id="p1">**</ept> is where you see results of Automated investigation and Response (AIR) threat investigations.
1. Also in <bpt id="p1">**</bpt>Email &amp; collaboration<ept id="p1">**</ept> are <bpt id="p2">**</bpt>Polices &amp; rules<ept id="p2">**</ept>. You will configure <bpt id="p1">**</bpt>Threat &amp; Alert<ept id="p1">**</ept> polices here.
1. Scroll down to <bpt id="p1">**</bpt>Cloud apps<ept id="p1">**</ept>. This the <bpt id="p1">**</bpt>Microsoft Defender for Cloud Apps<ept id="p1">**</ept> service section. Under <bpt id="p1">**</bpt>App governance<ept id="p1">**</ept> is where you set app policies.
1. 次のセクションには、Microsoft 365 Defender サービスの **[レポート]** 、管理者アクションの追跡を有効にすることができる **[監査]** 、 **[アクセス許可]** 、 **[設定]** があります。
1. **[アクセス許可]** では、**Azure AD** と**エンドポイント**のロールを構成できます。
1. **[設定]** では、タイムゾーンやメール通知などの一般的な構成と、エンドポイント、ID、デバイス検出の詳細な設定を入力します。
1. Select <bpt id="p1">**</bpt>Settings<ept id="p1">**</ept>, then <bpt id="p2">**</bpt>Endpoints<ept id="p2">**</ept>. You can view and add <bpt id="p1">**</bpt>Licenses<ept id="p1">**</ept> here. Next select <bpt id="p1">**</bpt>Advanced features<ept id="p1">**</ept>. Scroll thorough the list of features, but don't make any changes now.
1. Lastly, leave <bpt id="p1">**</bpt>Settings<ept id="p1">**</ept> and on the main, left menu list select <bpt id="p2">**</bpt>More resources<ept id="p2">**</ept>. You should see cards or tiles with links for <bpt id="p1">**</bpt>Microsoft Purview Compliance<ept id="p1">**</ept>, <bpt id="p2">**</bpt>Azure Active Directory<ept id="p2">**</ept> and other capabilities not directly part of <bpt id="p3">**</bpt>Microsoft 365 Defender<ept id="p3">**</ept>. Select the <bpt id="p1">**</bpt>Open<ept id="p1">**</ept> button for <bpt id="p2">**</bpt>Microsoft Purview Compliance<ept id="p2">**</ept>. This will open the compliance portal.

## <a name="you-have-completed-the-lab"></a>これでラボは完了です。