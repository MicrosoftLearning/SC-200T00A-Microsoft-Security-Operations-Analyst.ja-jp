---
lab:
  title: 演習 9 - ASIM パーサーを作成する
  module: Learning Path 7 - Create detections and perform investigations using Microsoft Sentinel
---

# ラーニング パス 7 - ラボ 1 - 演習 9 - ASIM パーサーをデプロイする

## ラボのシナリオ

![ラボの概要。](../Media/SC-200-Lab_Diagrams_Mod7_L1_Ex9.png)

あなたは、Microsoft Sentinel を実装した会社で働いているセキュリティ運用アナリストです。 特定の Windows レジストリ イベントに対して ASIM パーサーをモデル化する必要があります。 これらの簡略化されたパーサーは、[Advanced Security Information Model (ASIM) レジストリ イベント正規化スキーマのリファレンス](https://docs.microsoft.com/en-us/azure/sentinel/registry-event-normalization-schema)に従って、後で最終処理されます。

>**メモ:** このラボをご自分のペースでクリックして進めることができる、 **[ラボの対話型シミュレーション](https://mslabs.cloudguides.com/guides/SC-200%20Lab%20Simulation%20-%20Create%20Advanced%20Security%20Information%20Model%20Parsers)** が用意されています。 対話型シミュレーションとホストされたラボの間に若干の違いがある場合がありますが、示されている主要な概念とアイデアは同じです。 

### タスク 1:レジストリ スキーマ ASIM パーサーをデプロイする

このタスクでは、Microsoft Sentinel GitHub リポジトリからレジストリ スキーマ パーサーをデプロイします。

1. 管理者として WIN1 仮想マシンにログインします。パスワードは**Pa55w.rd**。  

1. Edge ブラウザーで、Azure portal (https://portal.azure.com ) に移動します。

1. **[サインイン]** ダイアログ ボックスで、ラボ ホスティング プロバイダーから提供された**テナントの電子メール** アカウントをコピーして貼り付け、 **[次へ]** を選択します。

1. **[パスワードの入力]** ダイアログ ボックスで、ラボ ホスティング プロバイダーから提供された**テナントのパスワード**をコピーして貼り付け、 **[サインイン]** を選択します。

1. Azure portal の検索バーに「*Sentinel*」と入力してから、**[Microsoft Sentinel]** を選択します。

1. 先ほど作成した Microsoft Sentinel ワークスペースを選択します。

1. Edge ブラウザーで、新しいタブを開き (Ctrl+T)、Microsoft Sentinel GitHub ASIM ページ (<https://github.com/Azure/Azure-Sentinel/tree/master/ASIM>) に移動します。

    <!--- 1. On the right pane, select the **Onboard community content** link. This will open a new tab in the Edge Browser for Microsoft Sentinel GitHub content. **Hint:** You might need to scroll right to see the link. Alternatively, follow this link instead: [Microsoft Sentinel on GitHub](https://github.com/Azure/Azure-Sentinel). --->

    >**注:**  **ASIM** フォルダーでは、すべての ASIM パーサーを含むテンプレートをデプロイできますが、ここではレジストリ スキーマにのみ焦点を当てます。

1. 下にスクロールし、 **[レジストリ]** の横にある **[Azure にデプロイ]** ボタンを選択します。

1. *[リソース グループ]* で、Sentinel ワークスペースが存在する **[RG-Defender]** を選択します。

1. *[ワークスペース]* に、*uniquenameDefender* などの Sentinel ワークスペース名を入力します。

1. 他の既定値はそのままにして、 **[確認と作成]** を選択します。

1. **[作成]** を選択してテンプレートをデプロイします。 さまざまなリソースの名前に注目してください。

1. デプロイが完了したら、*[Microsoft Sentinel]* タブに戻ります。

1. 左側のメニューの *[全般]* で、 **[ログ]** を選択します。

1. 必要に応じて **[>>]** を選択して、 *[スキーマとフィルター]* ブレードを開きます。

1. **[関数]** タブ ([テーブル] と [クエリ] タブの横にある) を選択します。 **ヒント:** タブを選択するには、省略記号アイコン **(...)** を選ぶ必要がある場合があります。

1. **[ワークスペース関数]** を展開します。 名前が、先ほどデプロイしたテンプレートに対応していることに注目してください。

1. **vimRegistryEventMicrosoftSecurityEvents** "ワークスペース パーサー" にカーソルを合わせてから、**[関数コードの読み込み]** を選択します。**

1. イベント ID 4657 を解析している KQL を確認し、Microsoft Sentinel ワークスペース内のデータの分析を簡略化します。

1. クエリを**実行**します。 これは検証のみを目的としているため、結果やエラーは表示されないはずです。

1. *[スキーマとフィルター]* ブレードに戻り、ここで **inRegistry** ''*統一パーサー*'' をポイントし、 **[関数コードの読み込み]** を選択します。

1. 統一パーサーでは ''*和集合*'' 演算子を使用して、すべてのワークスペース パーサーを一度に実行することに注目してください。 レジストリ スキーマ用のパーサーを開発する場合は、ここに追加する必要があります。

1. クエリを**実行**します。 結果やエラーは表示されないはずです。これは検証のみを目的としています。

1. この統一パーサーを、分析ルールまたはハンティング クエリに使用できるようになりました。

## 演習 10 に進む