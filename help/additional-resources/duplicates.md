---
title: 重複
description: 配信品質を向上させるために、重複を識別および制限する方法について説明します。
topics: Deliverability
kt: null
thumbnail: null
doc-type: article
activity: understand
team: ACS
exl-id: f89dbb38-a8d4-4294-b017-6fed72591593
source-git-commit: 68c403f915287e1a50cd276b67b3f48202f45446
workflow-type: tm+mt
source-wordcount: '386'
ht-degree: 61%

---

# 重複 {#duplicates}

重複した E メールアドレスがあると、以下のような複数の結果を招く可能性があります。

* 同じメッセージが複数回送信される。Adobeが送信前にデフォルトで重複排除処理を実行した場合でも、ターゲットが分割されたときに、同じコンテンツを持つ異なるアクションから同じメッセージが送信されるのを停止するものは何もありません。
* 購読解除リクエストが履行されない。受信者がメッセージを受信後に購読解除しても、重複したプロファイルではその後のメッセージの受信が解除されません。

オプトインでのこの問題に加え、ユーザーがメッセージをスパムであると見なし、ISP でのブロックリスト登録につながる可能性があります。

データベースを操作する場合は、特に慎重におこなう必要があります。

* インポートは、特に紐付けキーを選択する際に、細心の注意を払って設定する必要があります。
* 変更された E メールアドレスも、重複の元になる可能性があります。特に、異なるドメインを持つ2つのアドレスが、同じメールボックスにルーティングされる場合があります。例えば、会社が名前を変更し、特定の時間前のドメインを維持した場合などです。joe.doe@amce-co.comとjoe.doe@acme-rebranded.com。
* リストや他のデータベースのどちらから自動インポートを行う場合でも、プロファイルを管理する際に考慮すべき要素です。 プロファイルを削除したり別のパーティションに移動したりすると何が起こるでしょうか。例えば、発注書が配置された場合に、自動インポートによって最初のパーティションに再作成される可能性があります。
* 異なるフォルダーへのプロファイルの格納は、パーティションではなくビューを使用して実行できます。この方法では、表示および管理のための適切な権限が有効なまま、プロファイルは同じ物理パーティションにあります。

同様に、異なるパーティション間での重複が正常である場合があります。例えば、サードパーティや会社の別の組織に送信する場合、同じ人物が異なる理由で受信者になるのは、理にかなっています。しかし、同じパーディション内の重複が正常であることはまれです。

## 製品固有のリソース

アドレスの重複は、送信レピュテーションを保護し、適切な強制隔離管理をおこなうためのものです。詳しくは、次の製品ドキュメントの節を参照してください。

**Adobe Campaign Classic**

* [重複排除 — 重複アクティビティ](https://experienceleague.adobe.com/docs/campaign-classic/using/automating-with-workflows/targeting-activities/deduplication.html)
* [重複排除 — 重複アクティビティの結合機能の使用](https://experienceleague.adobe.com/docs/campaign-classic/using/automating-with-workflows/use-cases/data-management/deduplication-merge.html?lang=ja)

**Adobe Campaign Standard**

* [インポートされたファイルからのデータの重複排除](https://experienceleague.adobe.com/docs/campaign-standard/using/managing-processes-and-data/workflow-use-case/data-management/deduplicating-data-imported-file.html)
