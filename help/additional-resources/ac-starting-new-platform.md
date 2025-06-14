---
title: 新しいプラットフォームの開始
description: Adobe Campaignで新しいプラットフォームを開始する際の配信品質の管理について詳しく説明します。
topics: Deliverability
doc-type: article
activity: understand
team: ACS
exl-id: 6c9ade01-3052-4311-af80-888294820024
source-git-commit: d6094cd2ef0a8a7741e7d8aa4db15499fad08f90
workflow-type: tm+mt
source-wordcount: '563'
ht-degree: 56%

---

# 新しいプラットフォームの開始 {#starting-new-platform}

Adobe Campaignで使用する新しいプラットフォームを設定する際には、ドメインと IP アドレスのレピュテーションの維持が不可欠です。

## 繊細な手順

新しいプラットフォームでメールの送信を開始する際は、非常に注意する必要があります。プラットフォームには使用履歴がなく、送信 IP がこの目的で使用されたことがない場合は評判がないからです。

ISP は、当然ながら、メールを送信するのに使用したことがなく、突然、大量のメールトラフィックを送信し始める IP アドレスを疑います。実際に、スパム送信者は通常、「不明な」IP アドレス（ブロックリストに記載されていないアドレス）を使用して、検出前に可能な限り大量のメッセージを送信します。

本番フェーズの初期の出力では、運用速度に達することは期待できません。さらに、ISP によって送信アドレスがブロックされ、残りの開始フェーズに大きく影響することになるので、このままでメッセージを送信しようとしてはいけません。

## 主な原則

以下に、新しいプラットフォームを開始する際に従う必要がある主な原則を示します。

* Adobeから送信されるメールキャンペーンに固有の専用サブドメインを設定します。

* この情報がある場合、**無効なアドレスを強制隔離テーブルにインポート**&#x200B;します。
プラットフォームの開始は、多くの場合、アドレスのリストを初めて使用するときや、アドレスが完全修飾でない可能性があるときに発生します。無効なアドレスまたはハニーポットアドレスに送信すると、プラットフォームのレピュテーション低下の一因となります。

   * 無効なアドレスのリストがある場合は、最初に送信する前に強制隔離テーブルにインポートするのが最善の利益です。 強制隔離テーブルには、（管理 **[!UICONTROL Campaign Management/配信不能件数の管理/配信不能件数およびアドレス]** （Campaign Classic）および **[!UICONTROL 管理/チャネル/強制隔離/アドレス]** （Campaign Standard）メニューが用意されています。

   * 同様に、無効なアドレスを再評価する場合は、時間と共に不適切なアドレスの使用を減らすために、プラットフォームのレピュテーションが確立されたらおこない、少しずつ時間をかけて再評価することを強くお勧めします。

* mtachilds の数を制限して、**スループット率を制限**&#x200B;します。このような技術的な設定の調整について詳しくは、Adobe Campaign の管理者にお問い合わせください。

* スパムとしてマークされないように、**送信されるボリュームを順次増やします**。最初からデータベース全体をターゲットにせず、送信するたびにリストの少量を追加します。これにより、無効なアドレスの全体的な割合を減らしながら各ステップで量を増やすことができます。起動段階をスムーズに開発するために、ウェーブを使用できます。

* **定期的に送信**。ある程度までは、大規模なキャンペーンを散発的に行うよりも、小さなショットを定期的に送信する方が良いでしょう。
* **配信レポートに細心の注意を払う**。エラー指標が高い場合は、技術的な設定が正しく構成されていない可能性があります。

## その他のリソース

上記の原則とAdobe Campaignでの実装について詳しくは、次の節を参照してください。

* [IP ウォーミングによる電子メールの評判の向上](../../help/additional-resources/increase-reputation-with-ip-warming.md)
* [スパムトラップに関するすべて](../../help/additional-resources/all-about-spam-traps.md)

**Adobe Campaign Classic**

* [ 強制隔離による配信の最適化 ](https://experienceleague.adobe.com/docs/campaign-classic/using/sending-messages/monitoring-deliveries/understanding-quarantine-management.html?lang=ja#optimizing-your-delivery-through-quarantines)
* [ プラットフォーム全体の強制隔離アドレスを識別 ](https://experienceleague.adobe.com/docs/campaign-classic/using/sending-messages/monitoring-deliveries/understanding-quarantine-management.html?lang=ja#identifying-quarantined-addresses-for-the-entire-platform)
* [ 複数のウェーブを使用した送信 ](https://experienceleague.adobe.com/docs/campaign-classic/using/sending-messages/key-steps-when-creating-a-delivery/steps-sending-the-delivery.html?lang=ja#sending-using-multiple-waves)
* [配信の監視](https://experienceleague.adobe.com/docs/campaign-classic/using/sending-messages/monitoring-deliveries/about-delivery-monitoring.html?lang=ja#sending-messages)

**Adobe Campaign Standard**

* [ 強制隔離による配信の最適化 ](https://experienceleague.adobe.com/docs/campaign-standard/using/testing-and-sending/monitoring-messages/understanding-quarantine-management.html?lang=ja#optimizing-your-delivery-through-quarantines)
* [ プラットフォーム全体の強制隔離アドレスを識別 ](https://experienceleague.adobe.com/docs/campaign-standard/using/testing-and-sending/monitoring-messages/understanding-quarantine-management.html?lang=ja)
* [配信の監視](https://experienceleague.adobe.com/docs/campaign-standard/using/testing-and-sending/monitoring-messages/monitoring-a-delivery.html?lang=ja)
