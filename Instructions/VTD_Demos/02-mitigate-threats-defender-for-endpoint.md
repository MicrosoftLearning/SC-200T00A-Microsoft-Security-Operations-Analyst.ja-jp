---
ms.openlocfilehash: 86305aa8496c6b5cd7852460cdec9bf407547788
ms.sourcegitcommit: d725cbb2e789fb88a947d532396f79897a9d3088
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/08/2022
ms.locfileid: "147521740"
---
# <a name="module-2-demo---mitigate-attacks-with-microsoft-defender-for-endpoint"></a>モジュール 2 デモ - Microsoft Defender for Endpoint を使用した攻撃の軽減



**注**: このデモを正常に完了するには、[前提条件ドキュメント](00-prerequisites.md)のすべての手順を完了する必要があります。 

## <a name="simulated-attacks"></a>シミュレーション攻撃

このタスクでは、シミュレーション攻撃を 1 回行って、Microsoft Defender for Endpoint の機能を確認します。

1. まだ、Microsoft Defender セキュリティ センターをブラウザーで開いていない場合は、Microsoft Defender セキュリティ センター (https://security.microsoft.com) に移動して、お使いになっているテナントの管理者としてログインします。

1. メニューから、 **[エンドポイント]** の下で、 **[評価とチュートリアル]** を選択し、左側から **[チュートリアルとシミュレーション]** を選択します。

1. **[チュートリアル]** タブを選択します。

1. *[Automated investigation (backdoor)]\(自動調査 (バックドア)\)* に、シナリオを説明するメッセージが表示されます。 この段落の下にある **[Read the walkthrough]\(チュートリアルの読み取り\)** をクリックします。 シミュレーションを実行する手順を含む新しいブラウザー タブが開きます。

1. 新しいブラウザー タブで、 **[シミュレーションの実行]** という名前のセクション (5 ページの手順 2 から) を見つけ、次の手順に従って攻撃を実行します。 **ヒント:** シミュレーション ファイル *RS4_WinATP-Intro-Invoice.docm* は、ポータルに戻り、 **[Get simulation file]\(シミュレーション ファイルの取得\)** ボタンを選択して、前の手順で選択した **[Read the walkthrough]\(チュートリアルを読み取る\)** の下に表示されます。

    1. **注:** エクスプロイトを使用してファイルを実行した後、[Microsoft 365 Defender セキュリティ センター](https://security.microsoft.com)に戻り、**[インシデント]** タブをクリックしてアラートを表示できます。 このガイドでは、移行およびブランド変更された *Microsoft Defender ATP ポータル* を誤って参照しています。
    1. [インシデント] ページを開き、**[インシデントの管理]** をクリックします。 **[インシデントの解決]** をクリックして、アクティブなアラートをすべて解決します。


## <a name="you-have-completed-the-demo"></a>デモが完了しました。