---
title: 重複
description: 重複を識別および制限して、配信品質を向上させる方法を説明します。
topics: Deliverability
doc-type: article
activity: understand
team: ACS
exl-id: f89dbb38-a8d4-4294-b017-6fed72591593
source-git-commit: d6094cd2ef0a8a7741e7d8aa4db15499fad08f90
workflow-type: tm+mt
source-wordcount: '363'
ht-degree: 60%

---

# 重複 {#duplicates}

重複したメールアドレスがあると、以下のような複数の結果を招く可能性があります。

* 同じメッセージが複数回送信される。Adobeが送信前にデフォルトで重複排除手順を実行した場合でも、ターゲットが分割されたときに、同じコンテンツを持つ別のアクションによって同じメッセージが送信されるのを停止するものは何もありません。
* 購読解除リクエストが履行されない。受信者がメッセージを受信後に購読解除しても、重複したプロファイルではその後のメッセージの受信が解除されません。

オプトインでのこの問題に加え、ユーザーがメッセージをスパムであると見なし、ISP でのブロックリスト登録につながる可能性があります。

データベースを操作する場合は、特に慎重におこなう必要があります。

* インポートは、特に紐付けキーを選択する際に、細心の注意を払って設定する必要があります。
* 変更されたメールアドレスも、重複の元になる可能性があります。特に、ドメインが異なる 2 つのアドレスが同じメールボックスにルーティングされる場合があります。例えば、会社の名前が変更され、以前のドメインが一定期間メンテナンスされている場合などです。例えば、joe.doe@amce-co.comとjoe.doe@acme-rebranded.comです。
* 自動インポートは、リストの場合も他のデータベースの場合も、プロファイルを管理する際に考慮する要素です。 プロファイルを削除したり別のパーティションに移動したりすると何が起こるでしょうか。発注が行われたときなどに、自動インポートによって最初のパーティションに再作成できます。
* 異なるフォルダーへのプロファイルの格納は、パーティションではなくビューを使用して実行できます。この方法では、表示および管理のための適切な権限が有効なまま、プロファイルは同じ物理パーティションにあります。

同様に、異なるパーティション間での重複が正常である場合があります。例えば、サードパーティや会社の別の組織に送信する場合、同じ人物が異なる理由で受信者になるのは、理にかなっています。しかし、同じパーディション内の重複が正常であることはまれです。

## 製品固有のリソース

アドレスの重複を排除すると、送信の評判が保護され、優れた強制隔離管理が確保されます。 詳しくは、次の製品ドキュメントの節を参照してください。

**Adobe Campaign Classic**

* [&#x200B; 「重複排除」アクティビティ &#x200B;](https://experienceleague.adobe.com/docs/campaign-classic/using/automating-with-workflows/targeting-activities/deduplication.html?lang=ja)
* [&#x200B; 重複排除アクティビティの結合機能の使用 &#x200B;](https://experienceleague.adobe.com/docs/campaign-classic/using/automating-with-workflows/use-cases/data-management/deduplication-merge.html?lang=ja)

**Adobe Campaign Standard**

* [インポートされたファイルからのデータの重複排除](https://experienceleague.adobe.com/docs/campaign-standard/using/managing-processes-and-data/workflow-use-case/data-management/deduplicating-data-imported-file.html?lang=ja)
