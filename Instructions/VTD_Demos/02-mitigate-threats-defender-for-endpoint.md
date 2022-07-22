---
ms.openlocfilehash: 2fd744791ec4df2757b90424801e90101dee6382
ms.sourcegitcommit: 6934bbcd5d9774aa44dd949cf9523e8a43a505d1
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/18/2022
ms.locfileid: "147168448"
---
# <a name="module-1-demo---mitigate-attacks-with-microsoft-defender-for-endpoint"></a>モジュール 1 デモ - Microsoft Defender for Endpoint を使用した攻撃の軽減



**注**: このデモを正常に完了するには、[前提条件ドキュメント](00-prerequisites.md)のすべての手順を完了する必要があります。 

## <a name="simulated-attacks"></a>シミュレーション攻撃

このタスクでは、シミュレーション攻撃を 1 回行って、Microsoft Defender for Endpoint の機能を確認します。

1. まだ、Microsoft Defender セキュリティ センターをブラウザーで開いていない場合は、Microsoft Defender セキュリティ センター (https://security.microsoft.com) に移動して、お使いになっているテナントの管理者としてログインします。

2. メニューから **[評価とチュートリアル]** を選択し、左側で **[シミュレーションとチュートリアル]** を選びます。

3. シナリオ 1 を完了します。 これには、悪意のあるペイロードを含む Microsoft Word ドキュメントのダウンロードと実行が含まれます。 ポータルで提供されたチュートリアルで指示に従います。 
    1. **[Review generated alerts]\(生成されたアラートを確認する\)** の最初のサブセクション **[Alert:PowerShell dropped a suspicious file on the machine]\(アラート: PowerShell によって疑わしいファイルがマシンにドロップされました\)** で停止します。
    1. **注:** エクスプロイトを使用してファイルを実行した後、[Microsoft 365 Defender セキュリティ センター](https://security.microsoft.com)に戻り、**[インシデント]** タブをクリックしてアラートを表示できます。 このガイドでは、移行およびブランド変更された *Microsoft Defender ATP ポータル* を誤って参照しています。
    1. [インシデント] ページを開き、**[インシデントの管理]** をクリックします。 **[インシデントの解決]** をクリックして、アクティブなアラートをすべて解決します。


## <a name="you-have-completed-the-demo"></a>デモが完了しました。