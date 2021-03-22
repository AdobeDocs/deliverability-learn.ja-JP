---
title: 新しいプラットフォームの開始
description: Adobe Campaignを使用して新しいプラットフォームを開始する際の配信品質の管理についての詳細。
feature: 実際に使う
topics: Deliverability
kt: null
thumbnail: null
doc-type: article
activity: understand
team: ACS
translation-type: tm+mt
source-git-commit: 96ed84da391faaabd3001ddd6a411ddc1f46b033
workflow-type: tm+mt
source-wordcount: '607'
ht-degree: 55%

---


# 新しいプラットフォームの開始 {#starting-new-platform}

Adobe Campaignで使用する新しいプラットフォームを設定する場合は、ドメインとIPアドレスの評判を維持することが不可欠です。

## 微妙な段階

新しいプラットフォームで電子メールの送信を開始する際は、十分に注意する必要があります。これは、プラットフォームには使用履歴がなく、送信側IPがこの目的で使用されたことが一度もない場合には評判がないからです。

ISP は、当然ながら、E メールを送信するのに使用したことがなく、突然、大量の E メールトラフィックを送信し始める IP アドレスを疑います。実際に、スパム送信者は通常、「不明な」IP アドレス（ブロックリストに記載されていないアドレス）を使用して、検出前に可能な限り大量のメッセージを送信します。

本番フェーズの初期の出力では、運用速度に達することは期待できません。さらに、ISP によって送信アドレスがブロックされ、残りの開始フェーズに大きく影響することになるので、このままでメッセージを送信しようとしてはいけません。

## 主な原則

新しいプラットフォームを立ち上げる際に従うべき主な原則を以下に示します。

* Adobeから送信される電子メールキャンペーンに固有の専用サブドメインを設定します。

* この情報がある場合、**無効なアドレスを強制隔離テーブルにインポート**します。
プラットフォームの開始は、多くの場合、アドレスのリストを初めて使用するときや、アドレスが完全修飾でない可能性があるときに発生します。無効なアドレスまたはハニーポットアドレスに送信すると、プラットフォームのレピュテーション低下の一因となります。

   * 無効なアドレスのリストがある場合は、最初に送信する前に、強制隔離テーブルに無効なアドレスをインポートすることをお勧めします。 強制隔離テーブルは、**[!UICONTROL Administration > Campaign Management > Non deliverables Management > Non deliverables and addresses]**(Campaign Classic)メニューと&#x200B;**[!UICONTROL Administration > Channels > Quarantines > Addresses]**(Campaign Standard)メニューから利用できます。

   * 同様に、無効なアドレスを再評価する場合は、時間と共に不適切なアドレスの使用を減らすために、プラットフォームのレピュテーションが確立されたらおこない、少しずつ時間をかけて再評価することを強くお勧めします。

* mtachilds の数を制限して、**スループット率を制限**&#x200B;します。このような技術的な設定の調整について詳しくは、Adobe Campaign の管理者にお問い合わせください。

* スパムとしてマークされないように、**送信されるボリュームを順次増やします**。最初からデータベース全体をターゲットにせず、送信するたびにリストの少量を追加します。これにより、無効なアドレスの全体的な割合を減らしながら各ステップで量を増やすことができます。開始アップ段階を円滑に開発するために、ウェーブを使用できます。

* **定期的に送信**。ある程度は、大きなキャンペーンを散発的に送るよりも、小さな写真を定期的に送る方が良い。
* **配信レポートに細心の注意を払う**。エラー指標の数が多い場合は、技術的な設定が正しく設定されていない可能性があります。

## その他のリソース

上記の原則とAdobe Campaignを使用した実装について詳しくは、次の節を参照してください。

* [IP ウォーミングによる E メールの評判の向上](../../help/additional-resources/increase-reputation-with-ip-warming.md)
* [スパムトラップに関するすべて](../../help/additional-resources/all-about-spam-traps.md)

**Adobe Campaign Classic**

* [強制隔離を通じて配信を最適化する](https://experienceleague.adobe.com/docs/campaign-classic/using/sending-messages/monitoring-deliveries/understanding-quarantine-management.html#optimizing-your-delivery-through-quarantines)
* [プラットフォーム全体の検疫済みアドレスの識別](https://experienceleague.adobe.com/docs/campaign-classic/using/sending-messages/monitoring-deliveries/understanding-quarantine-management.html#identifying-quarantined-addresses-for-the-entire-platform)
* [複数のウェーブを使用した送信](https://experienceleague.adobe.com/docs/campaign-classic/using/sending-messages/key-steps-when-creating-a-delivery/steps-sending-the-delivery.html#sending-using-multiple-waves)
* [配信監視](https://experienceleague.adobe.com/docs/campaign-classic/using/sending-messages/monitoring-deliveries/about-delivery-monitoring.html#sending-messages)

**Adobe Campaign Standard**

* [強制隔離を通じて配信を最適化する](https://experienceleague.adobe.com/docs/campaign-standard/using/testing-and-sending/monitoring-messages/understanding-quarantine-management.html#optimizing-your-delivery-through-quarantines)
* [プラットフォーム全体の検疫済みアドレスの識別](https://experienceleague.adobe.com/docs/campaign-standard/using/testing-and-sending/monitoring-messages/understanding-quarantine-management.html)
* [配信の監視](https://experienceleague.adobe.com/docs/campaign-standard/using/testing-and-sending/monitoring-messages/monitoring-a-delivery.html)
