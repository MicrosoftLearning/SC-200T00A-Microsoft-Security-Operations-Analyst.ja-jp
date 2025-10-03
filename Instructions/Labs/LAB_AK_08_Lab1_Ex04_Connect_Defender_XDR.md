---
lab:
  title: 演習 4 - データ コネクタを使用して Defender XDR を Microsoft Sentinel に接続する
  module: Learning Path 8 - Connect logs to Microsoft Sentinel
---

# ラーニング パス 8 - ラボ 1 - 演習 4 - データ コネクタを使用して Defender XDR を Microsoft Sentinel に接続する

## ラボのシナリオ

![ラボの概要。](../Media/SC-200-Lab_Diagrams_Mod8_L1_Ex4.png)

あなたは、Microsoft Defender XDR と Microsoft Sentinel の両方を展開した会社で働いているセキュリティ運用アナリストです。 Microsoft Sentinel を Defender XDR に接続する統合セキュリティ運用プラットフォームを準備する必要があります。 次の手順では、Defender XDR コンテンツ ハブ ソリューションをインストールし、Defender XDR データ コネクタを Microsoft Sentinel に展開します。

>**注:** この演習の環境は、製品から生成されたシミュレーションです。 シミュレーションには制限があるため、ページ上のリンクが有効にならない場合があり、指定されたスクリプトに該当しないテキストベースの入力はサポートされない場合があります。 "This feature is not available within the simulation" (この機能はシミュレーション内では使用できません) というポップアップ メッセージが表示されます。 これが発生したら、[OK] を選択し、演習の手順を続行してください。

![ポップアップ エラー メッセージ](../Media/simulation-pop-up-error.png)

### タスク 1:Defender XDR を接続する

このタスクでは、Microsoft Defender XDR コネクタを展開します。

1. 管理者として WIN1 仮想マシンにログインします。パスワードは**Pa55w.rd**。  

1. Microsoft Edge ブラウザーで、次のリンクを選択して、シミュレートされた環境を開きます: <https://app.highlights.guide/start/1c894b46-4b0a-40cb-b0f0-1e1c86c615f3?token=16d48b6c-eace-4a1f-8050-098d29d23a89>

    <!--- [Azure portal]( https://app.highlights.guide/start/1c894b46-4b0a-40cb-b0f0-1e1c86c615f3?token=16d48b6c-eace-4a1f-8050-098d29d23a89). --->

1. Azure portal の [ホーム] ページで、**[Microsoft Sentinel]** アイコンを選択します。**

1. [Microsoft Sentinel] ページで、ワークスペース **[Woodgrove-LogAnalyiticWorkspace]** を選択します。**

1. Microsoft Sentinel の左側のメニューで、 **[コンテンツ管理]** セクションまで下にスクロールし、 **[コンテンツ ハブ]** を選択します。

1. *[コンテンツ ハブ]* で、**Microsoft Defender XDR** ソリューションを検索し、リストから選択します。

1. *Microsoft Defender XDR* ソリューションの詳細ページで、**[インストール]** を選択します。

1. インストールが完了したら、**Microsoft Defender XDR** ソリューションを検索して選択します。

1. *Microsoft Defender XDR* ソリューションの詳細ページで、**[管理]** を選択します

1. *[Microsoft Defender XDR]* データ コネクタ チェック ボックスをオンにし、**[コネクタ ページを開く]** を選択します。

1. 接続が成功したことを示すメッセージが表示されるはずです。

### タスク 2:Microsoft Sentinel と Microsoft Defender XDR を接続する

このタスクでは、シミュレーションを続行し、Microsoft Sentinel ワークスペースを Microsoft Defender XDR に接続します。

1. Microsoft Sentinel の [コンテンツ ハブ] (ページ上部の "階層リンク" メニュー リンクを使用) に戻り、ナビゲーション メニューの [全般] セクションから **[概要 (プレビュー)]** を選択します。**

1. "SIEM と XDR を 1 か所にまとめましょう" というメッセージにある **[詳細情報]** ボタンを選択します。**

1. **[詳細情報]** ボタンを選択すると、*Microsoft Defender XDR* ポータルのブラウザーで新しいタブが開きます。

1. **[Defender Defender]** ポータルの **[ホーム]** 画面の上部に、"SIEM と XDR を 1 か所にまとめましょう" というメッセージがあるバナーが表示されます。** **[ワークスペースの接続]** ボタンを選択します。

1. [ワークスペースを選択する] ページで、Microsoft Sentinel ワークスペース **[woodgrove-loganalyiticsworkspace]** を選択します。**

1. **[次へ]** ボタンを選択します。

1. **[プライマリ ワークスペースを設定する]** ページで、ドロップダウン メニューに Microsoft Sentinel ワークスペース **[woodgrove-loganalyiticsworkspace]** が表示されます。 **[次へ]** ボタンを選択します。

1. [レビューして終了] ページで、[ワークスペース] の選択が正しいことを確認し、[ワークスペースが接続されたときに予測されること] セクションにある箇条書き項目を確認します。****** **関連付け**ボタンを選択します。

1. "ワークスペースを接続しようとしています" メッセージが表示されます。** **関連付け**ボタンを選択します。

1. これで、[ワークスペースの接続に成功] ページに移動します。**

1. **閉じる**ボタンを選択します。

1. **Defender XDR** ポータルの **[ホーム]** 画面の上部に、"統合された SIEM と XDR の準備ができました" というメッセージのバナーが表示されるはずです。** **[ハンティングの開始]** ボタンを選択します。

1. [高度な追求] に、"Microsoft Sentinel からコンテンツを探索する" というメッセージが表示されます。** [高度な追求] ナビゲーション メニューで、対応するタブの下に *Microsoft Sentinel* のテーブル、関数、クエリが表示されます。**

1. **[スキーマ]** タブで **[Microsoft Sentinel]** という見出しまで下にスクロールし、**[ThreatIntelligenceIndicator]** テーブルをダブルクリックします。

1. [クエリ] ペインに、脅威インテリジェンス インジケーターを返す (KQL) クエリが表示されます。** **[クエリを実行]** ボタンを選択します。

1. [結果] ペインに、返された結果が表示されます。**

1. 左側のメイン メニュー ペインが折りたたまれている場合はそれを展開し、新しい **Microsoft Sentinel** メニュー項目を展開します。 [検索]、[脅威の管理]、[コンテンツ管理]、[構成] の選択肢が表示されます。********

    >**注:**  Azure の Microsoft Sentinel ポータルと Microsoft Defender XDR 内の Sentinel には機能の違いがあることに注意してください **[ポータルの機能の違い](https://learn.microsoft.com/azure/sentinel/microsoft-sentinel-defender-portal#capability-differences-between-portals)**。

1. Microsoft Defender XDR の **[Microsoft Sentinel]** メニュー項目から、**[構成]**、**[データ コネクタ]** の順に選択します。

1. [データ コネクタ] ページに、**[Azure アクティビティ]** およびその他のデータ コネクタが **[接続済み]** の状態で表示されます。**

>**注:**  他の Microsoft Sentinel 機能を自由に探索して比較できます。ただし、これはシミュレーションであるため、Microsoft Defender ポータルで Microsoft Sentinel を探索する機能は制限されています。 実際の環境では、Microsoft Defender ポータルで Microsoft Sentinel の完全な機能を探索できます。

## ラボを完了しました。ラーニング パス 9 - ラボ 1 - 演習 1 - Microsoft セキュリティ規則を変更するに進んでください
