---
lab:
  title: 演習 2 - Microsoft Defender for Endpoint を使用した攻撃の軽減
  module: Module 2 - Mitigate threats using Microsoft Defender for Endpoint
ms.openlocfilehash: 0f79ef27e27b989481d50b9ff617c21ba6770705
ms.sourcegitcommit: 175df7de88c9a609f8caf39840664bf992c5b6dc
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/05/2022
ms.locfileid: "138025412"
---
# <a name="module-2---lab-1---exercise-2---mitigate-attacks-with-microsoft-defender-for-endpoint"></a>モジュール 2 - ラボ 1 - 演習 2 - Microsoft Defender for Endpoint を使用した攻撃の軽減

## <a name="lab-scenario"></a>ラボのシナリオ

あなたは Microsoft Defender for Endpoint を実装している企業で働いているセキュリティ運用アナリストです。 あなたの上司は、いくつかのデバイスをオンボードして、セキュリティ オペレーション (SecOps) チームの応答手順で必要な変更に関する情報を提供しようとしています。

Defender for Endpoint の攻撃緩和機能を確認するため、シミュレーション攻撃を 2 回行います。


### <a name="task-1-simulated-attacks"></a>タスク 1:シミュレーション攻撃

このタスクでは、シミュレーション攻撃を 2 回行って、Microsoft Defender for Endpoint の機能を確認します。

1. Microsoft Edge ブラウザーの Microsoft 365 Defender ポータルにまだアクセスしていない場合は、(https://security.microsoft.com) に移動し、テナントの Admin としてログインします。

1. メニューから、 **[エンドポイント]** の下で、 **[評価とチュートリアル]** を選択し、左側から **[チュートリアルとシミュレーション]** を選択します。

1. **[チュートリアル]** タブを選択します。

1. **[Automated investigation (backdoor)]\(自動調査 (バックドア)\)** に、シナリオを説明するメッセージが表示されます。 この段落の下にある **[Read the walkthrough]\(チュートリアルの読み取り\)** をクリックします。 シミュレーションを実行する手順を含む新しいブラウザー タブが開きます。

1. 新しいブラウザー タブで、 **[Run the simulation]** という名前のセクションを見つけ、 手順 2 から攻撃を実行します。 **ヒント:** シミュレーション ファイル *RS4_WinATP-Intro-Invoice.docm* は、**[Get simulation file]\(シミュレーション ファイルの取得\)** ボタンを選択してダウンロードすることができます。 

1. 次に、同様にして *[Automated investigation (fileless attack)]\(自動調査 (ファイルレス攻撃)\)* を実行します。攻撃を実行するには、**シミュレーションスクリプトのコピー**をクリックし、コピーされたスクリプトを**管理者で起動したPowerShell** で実行します。

1. 攻撃によって、Windows 10 上の Defender が脅威を検出するため、右下に脅威を示すポップアップが表示されます。 

1. Microsoft 365 Defender ポータルで、左側のメニュー バーから **[インシデントとアラート]** を選択し、 **[インシデント]** を選択します。

1. "Multi-stage Incident..." という新しいインシデントが、右側のペインに表示されます。 インシデントが表示されるまでに 5 分程度かかります。 インシデント名をクリックして詳細を読み込みます。

1. **[インシデントの管理]** ボタンを選択すると、新しいウィンドウ ブレードが表示されます。 

1. **[Incident tags]\(インシデント タグ\)** に「Tutorial」と入力し、 **[Tutorial (Create new)]\(チュートリアル (新規作成)\)** を選択して新しいタグを作成します。 

1. **割り当て先** で **[自分に割り当て]** トグルを選択して、インシデントの所有者として自分のユーザー アカウントを追加します。 

1. **[分類]** で、ドロップダウン メニューの **セキュリティテスト** を選択します。 

1. **[決定]** で、ドロップダウン メニューの **[Security test]\(セキュリティ テスト\)** を選択します。 

1. 必要に応じてコメントを追加し、 **[保存]** をクリックして終了します。

1. [アラート]、[デバイス]、[ユーザー]、[調査]、[Evidence and Response]\(証拠と応答\)、[グラフ] タブの内容を確認します。 **ヒント:** 一部のタブは、ディスプレイのサイズが原因で非表示になる場合があります。 省略記号タブ (...) を選択して表示します。

>**警告:** ここでのシミュレーションとチュートリアルは、実践を通して学ぶための優れた情報源です。  シミュレーションとチュートリアルは、ポータルで定期的に追加および編集されています。  ただし、これらのシミュレーションとチュートリアルの一部は、このトレーニングコース用に設計されたラボのパフォーマンスを妨げる可能性があります。  コースで提供される Azure テナントを使用する場合は、このラボで提供されている手順で推奨されているシミュレーションとチュートリアルのみを実行してください。  このテナントでこのトレーニング コースが完了した *後*、他のシミュレーションやチュートリアルを実行できます。

## <a name="you-have-completed-the-lab"></a>これでラボは完了です。
