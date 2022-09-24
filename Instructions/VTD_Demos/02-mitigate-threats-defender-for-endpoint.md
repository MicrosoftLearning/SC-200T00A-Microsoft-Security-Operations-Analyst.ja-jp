# <a name="module-2-demo---mitigate-attacks-with-microsoft-defender-for-endpoint"></a>モジュール 2 デモ - Microsoft Defender for Endpoint を使用した攻撃の軽減



**注**: このデモを正常に完了するには、[前提条件ドキュメント](00-prerequisites.md)のすべての手順を完了する必要があります。 

## <a name="simulated-attacks"></a>シミュレーション攻撃

このタスクでは、シミュレーション攻撃を 1 回行って、Microsoft Defender for Endpoint の機能を確認します。

1. まだ、Microsoft Defender セキュリティ センターをブラウザーで開いていない場合は、Microsoft Defender セキュリティ センター (https://security.microsoft.com) に移動して、お使いになっているテナントの管理者としてログインします。

1. メニューから、 **[エンドポイント]** の下で、 **[評価とチュートリアル]** を選択し、左側から **[チュートリアルとシミュレーション]** を選択します。

1. **[チュートリアル]** タブを選択します。

1. Under <bpt id="p1">*</bpt>Automated investigation (backdoor)<ept id="p1">*</ept> you will see a message describing the scenario. Below this paragraph, click <bpt id="p1">**</bpt>Read the walkthrough<ept id="p1">**</ept>. A new browser tab opens which includes instructions to perform the simulation.

1. In the new browser tab, locate the section named <bpt id="p1">**</bpt>Run the simulation<ept id="p1">**</ept> (page 5, starting at step 2) and follow the steps to run the attack. <bpt id="p1">**</bpt>Hint:<ept id="p1">**</ept> The simulation file <bpt id="p2">*</bpt>RS4_WinATP-Intro-Invoice.docm<ept id="p2">*</ept> can be found back in portal, just below the <bpt id="p3">**</bpt>Read the walkthrough<ept id="p3">**</ept> you selected in the previous step by selecting the <bpt id="p4">**</bpt>Get simulation file<ept id="p4">**</ept> button.

    1. <bpt id="p1">**</bpt>Note:<ept id="p1">**</ept> After executing the file with the  exploit, you can return to the <bpt id="p2">[</bpt>Microsoft 365 Defender Security Center<ept id="p2">](https://security.microsoft.com)</ept> and click on the <bpt id="p3">**</bpt>Incidents<ept id="p3">**</ept> tab to see the alerts. The guide incorrectly references the <bpt id="p1">*</bpt>Microsoft Defender ATP portal<ept id="p1">*</ept> which has been migrated and rebranded.
    1. Open the incident page and click <bpt id="p1">**</bpt>Manage Incident<ept id="p1">**</ept>. Click <bpt id="p1">**</bpt>Resolve incident<ept id="p1">**</ept> to resolve all of the active alerts.


## <a name="you-have-completed-the-demo"></a>デモが完了しました。