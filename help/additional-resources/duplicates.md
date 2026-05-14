---
title: 重複
description: 重複を特定して制限し、配信品質を向上させる方法について説明します。
topics: Deliverability
doc-type: article
activity: understand
team: ACS
exl-id: f89dbb38-a8d4-4294-b017-6fed72591593
TQID: https://experienceleague.adobe.com/7KlDe-wQmAih6L4bl4xrw-lVS35-wNzyyxneyFbSo0A
product_v2:
  - id: b27e5950-9033-45ac-9f86-eb22e567f615
  - id: d0a3eab4-7b10-4d96-a71e-6c0f8e7b7c87
  - id: dfc56824-e8b9-499e-85d4-21aedb507314
feature_v2:
  - id: b0bb9048-d951-48d8-8232-45cf248a7e27
  - id: c5f60233-d5ea-4453-a799-0ad258b4d399
  - id: f71e690b-4480-4b67-9ef5-88f42f9cdfdb
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
  - id: f8a45b24-4be7-4f1b-909b-60d06b483a20
level_v2:
  - id: e8ccd51f-da0d-4e3b-939b-e30d5ebb1ea5
source-git-commit: 75df8537199680e5f1fc4b98cefdb05220fee7bf
workflow-type: tm+mt
source-wordcount: 413
ht-degree: 60%

---

# 重複 {#duplicates}

重複したメールアドレスがあると、以下のような複数の結果を招く可能性があります。

* 同じメッセージが複数回送信される。 送信前にAdobeがデフォルトで重複排除プロシージャを実行していても、ターゲットを分割する際に、同じ内容を持つ異なるアクションによって同じメッセージが送信されるのを止める必要はありません。
* 購読解除リクエストが履行されない。 受信者がメッセージを受信後に購読解除しても、重複したプロファイルではその後のメッセージの受信が解除されません。

オプトインでのこの問題に加え、ユーザーがメッセージをスパムであると見なし、ISP でのブロックリスト登録をトリガーする可能性があります。

データベースを操作する場合は、特に慎重におこなう必要があります。

* インポートは、特に紐付けキーを選択する際に、細心の注意を払って設定する必要があります。
* 変更されたメールアドレスも、重複の元になる可能性があります。 特に、ドメインが異なる2つのアドレスが、同じメールボックスにルーティングされる場合があります。例えば、会社が名前を変更し、以前のドメインを一定期間維持している場合は、joe.doe@amce-co.comとjoe.doe@acme-rebranded.comです。
* リストまたは他のデータベースからの自動インポートは、プロファイルを管理する際に考慮する要素です。 プロファイルを削除したり別のパーティションに移動したりすると何が起こるでしょうか。 発注書が配置された場合など、自動読み込みによって、最初のパーティションで再作成される場合があります。
* 異なるフォルダーへのプロファイルの格納は、パーティションではなくビューを使用して実行できます。 この方法では、表示および管理のための適切な権限が有効なまま、プロファイルは同じ物理パーティションにあります。

同様に、異なるパーティション間での重複が正常である場合があります。 例えば、サードパーティや会社の別の組織に送信する場合、同じ人物が異なる理由で受信者になるのは、理にかなっています。 しかし、同じパーディション内の重複が正常であることはまれです。

## 製品固有のリソース

アドレスの重複は、送信レピュテーションを保護し、適切な強制隔離管理をおこなうためのものです。 詳しくは、次の製品ドキュメントの節を参照してください。

**Adobe Campaign Classic**

* [重複排除アクティビティ](https://experienceleague.adobe.com/docs/campaign-classic/using/automating-with-workflows/targeting-activities/deduplication.html)
* [重複排除アクティビティの結合機能の使用](https://experienceleague.adobe.com/docs/campaign-classic/using/automating-with-workflows/use-cases/data-management/deduplication-merge.html?lang=ja)

**Adobe Campaign Standard**

* [インポートされたファイルからのデータの重複排除](https://experienceleague.adobe.com/docs/campaign-standard/using/managing-processes-and-data/workflow-use-case/data-management/deduplicating-data-imported-file.html)
