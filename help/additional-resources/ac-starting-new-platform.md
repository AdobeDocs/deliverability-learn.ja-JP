---
title: 新しいプラットフォームの開始
description: Adobe Campaignを利用して、配信品質を管理する方法については、こちらをご覧ください。
topics: Deliverability
doc-type: article
activity: understand
team: ACS
exl-id: 6c9ade01-3052-4311-af80-888294820024
TQID: https://experienceleague.adobe.com/cQa5nOTSJwxDGX-QkXGez5dpm5N-8I7QZ-LsEW0FRLo
product_v2: id: b27e5950-9033-45ac-9f86-eb22e567f615id: d0a3eab4-7b10-4d96-a71e-6c0f8e7b7c87id: dfc56824-e8b9-499e-85d4-21aedb507314
feature_v2: id: a075b2c1-7748-4328-b7f6-343aa314616aid: c5474392-5419-4296-9e41-f6f4ce4f6e9bid: c5f60233-d5ea-4453-a799-0ad258b4d399id: d1d0a9cd-295d-4976-8c39-ddae266f240eid: e2290edd-b061-4880-9d79-dee306cf5aa9id: f71e690b-4480-4b67-9ef5-88f42f9cdfdbid: fdbb8fc9-ffa3-4b86-88fe-aa4c5a3e1bc6
role_v2: id: b69b2659-1057-424e-8fc5-ed9e016dc554id: f8a45b24-4be7-4f1b-909b-60d06b483a20
level_v2: id: e8ccd51f-da0d-4e3b-939b-e30d5ebb1ea5
topic_v2: id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87cid: eddd9b14-83bd-4ff4-9072-54a4a484abb7
source-git-commit: 75df8537199680e5f1fc4b98cefdb05220fee7bf
workflow-type: tm+mt
source-wordcount: 680
ht-degree: 49%

---

# 新しいプラットフォームの開始 {#starting-new-platform}

Adobe Campaignで使用する新しいプラットフォームを設定する際には、ドメインとIP アドレスのレピュテーションを維持することが不可欠です。

## 機密性のあるステップ

新しいプラットフォームでメールを送信するときは、プラットフォームには使用履歴がなく、送信IPがこの目的に使用されたことがない場合はレピュテーションがないので、十分に注意する必要があります。

ISP は、当然ながら、メールを送信するのに使用したことがなく、突然、大量のメールトラフィックを送信し始める IP アドレスを疑います。 実際に、スパム送信者は通常、「不明な」IP アドレス（ブロックリストに記載されていないアドレス）を使用して、検出前に可能な限り大量のメッセージを送信します。

本番フェーズの初期の出力では、運用速度に達することは期待できません。 さらに、ISP によって送信アドレスがブロックされ、残りの開始フェーズに大きく影響することになるので、このままでメッセージを送信しようとしてはいけません。

## 主な原則

新しいプラットフォームを立ち上げる際に従うべき主な原則を以下に示します。

* Adobeから送信されるメールキャンペーンに固有の専用サブドメインを設定します。

* この情報がある場合、**無効なアドレスを強制隔離テーブルにインポート**します。
プラットフォームの開始は、多くの場合、アドレスのリストを初めて使用するときや、アドレスが完全修飾でない可能性があるときに発生します。 無効なアドレスまたはハニーポットアドレスに送信すると、プラットフォームのレピュテーション低下の一因となります。

   * 無効なアドレスのリストがある場合は、最初に送信する前に強制隔離テーブルに読み込むことが最善の利益となります。 強制隔離テーブルは、**[!UICONTROL 管理/Campaign Management/配信不能管理/配信不能件数とアドレス]** （Campaign Classic）および&#x200B;**[!UICONTROL 管理/チャネル/強制隔離/アドレス]** （Campaign Standard）メニューから利用できます。

   * 同様に、無効なアドレスを再評価する場合は、時間と共に不適切なアドレスの使用を減らすために、プラットフォームのレピュテーションが確立されたらおこない、少しずつ時間をかけて再評価することを強くお勧めします。

* mtachilds の数を制限して、**スループット率を制限**&#x200B;します。 このような技術的な設定の調整について詳しくは、Adobe Campaign の管理者にお問い合わせください。

* スパムとしてマークされないように、**送信されるボリュームを順次増やします**。 最初からデータベース全体をターゲットにするのではなく、送信するたびにリストの余分な部分を追加します。 これにより、無効なアドレスの全体的な割合を減らしながら、各ステップでボリュームを増やすことができます。 スタートアップ段階のスムーズな開発を確実にするために、波を使用することができます。

* **定期的に送信**。 ある程度は、大規模なキャンペーンを散発的に実施するのではなく、定期的に小規模なキャンペーンを実施する方が良いでしょう。
* **配信レポートに細心の注意を払う**。 エラー指標が高い場合は、技術的な設定が適切に設定されていない可能性があります。

## その他のリソース

上記の原則とAdobe Campaignでの実装について詳しくは、次の節を参照してください。

* [IP ウォーミングによる電子メールの評判の向上](../../help/additional-resources/increase-reputation-with-ip-warming.md)
* [スパムトラップに関するすべて](../../help/additional-resources/all-about-spam-traps.md)

**Adobe Campaign Classic**

* [強制隔離による配信の最適化](https://experienceleague.adobe.com/docs/campaign-classic/using/sending-messages/monitoring-deliveries/understanding-quarantine-management.html#optimizing-your-delivery-through-quarantines)
* [プラットフォーム全体で強制隔離されたアドレスを特定](https://experienceleague.adobe.com/docs/campaign-classic/using/sending-messages/monitoring-deliveries/understanding-quarantine-management.html#identifying-quarantined-addresses-for-the-entire-platform)
* [複数のウェーブを使用した送信](https://experienceleague.adobe.com/docs/campaign-classic/using/sending-messages/key-steps-when-creating-a-delivery/steps-sending-the-delivery.html?lang=ja#sending-using-multiple-waves)
* [配信の監視](https://experienceleague.adobe.com/docs/campaign-classic/using/sending-messages/monitoring-deliveries/about-delivery-monitoring.html?lang=ja#sending-messages)

**Adobe Campaign Standard**

* [強制隔離による配信の最適化](https://experienceleague.adobe.com/docs/campaign-standard/using/testing-and-sending/monitoring-messages/understanding-quarantine-management.html#optimizing-your-delivery-through-quarantines)
* [プラットフォーム全体で強制隔離されたアドレスを特定](https://experienceleague.adobe.com/docs/campaign-standard/using/testing-and-sending/monitoring-messages/understanding-quarantine-management.html?lang=ja)
* [配信の監視](https://experienceleague.adobe.com/docs/campaign-standard/using/testing-and-sending/monitoring-messages/monitoring-a-delivery.html?lang=ja)
