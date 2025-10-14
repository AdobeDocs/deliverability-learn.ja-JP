---
title: ボリューム – スムーズに移行するためのヒント
description: 送信するメールの量は、肯定的な評判を確立するために重要です。 スムーズに移行するために実行できる操作について説明します。
topics: Deliverability
jira: KT-7055
thumbnail: kt7055.jpg
doc-type: article
activity: understand
role: Admin,User
level: Beginner
team: ACS
exl-id: 1bc56061-0c64-4033-b49c-66618916bca6
source-git-commit: 6b312cdbba496818337c97ec4f42962aea757901
workflow-type: tm+mt
source-wordcount: '553'
ht-degree: 1%

---

# ボリューム

送信するメールの量は、肯定的な評判を確立するために重要です。 自分を ISP の立場に置く – 知らない人から大量のトラフィックが来るようになると、驚くべきことでしょう。 大量のメールをすぐに送信するのはリスクが高く、多くの場合、解決が困難な評判の問題を引き起こします。 あまりにも早く送信しすぎることで生じる評判の低下やバルク化およびブロッキングの問題から自分自身を掘り下げることは、イライラし、時間がかかり、コストがかかる可能性があります。

ボリュームしきい値は、ISP によって異なり、また平均エンゲージメント指標によって異なる場合があります。 一部の送信者はボリュームの非常に低く、遅いランプを必要としますが、他の送信者はボリュームの急峻なランプを可能にする場合があります。 Adobe配信品質コンサルタントなどのエキスパートと協力して、カスタマイズされたボリュームプランを作成することをお勧めします。

移行をスムーズに行うためのヒントとヒントを以下に示します。

* **権限** は、成功するメールプログラムの基盤です。
* **低く、低速** – 最初は送信量が少なくなりますが、送信者の評判を確立するにつれて増加します。
* **タンデム送信戦略** を使用すると、メールカレンダーを中断することなく、現在の ESP で処理を完了しながら、Campaign の量を増やすことができます。
* **エンゲージメントに関する問題** - メールを定期的に開いてクリックする購読者から始めます。
* **計画に従う** – 当社の推奨事項により、何百人もの Campaign クライアントがメールプログラムを正常に立ち上げるのに役立ちました。
* **返信メールアカウントを監視** します。 顧客がnoreply@xyz.comを使用したり、応答したりするのは良くないエクスペリエンスです。
* 非アクティブなアドレスは、配信品質に悪影響を与える可能性があります。 **新しい IP ではなく、現在のプラットフォームで再アクティブ化して再権限を付与します**。
* **ドメイン** – 会社の実際のドメインのサブドメインである送信ドメインを使用します
   * 例えば、会社のドメインがxyz.comの場合、email.xyz.comはxyzemail.comよりも ISP に信頼性を提供します
* **透明性** - メールドメインの登録詳細は、公開する必要があり、非公開にしないでください。

多くの場合、トランザクションメールは、従来のプロモーションウォーミングアプローチに従いません。 トランザクションメールは通常、メールのタッチをトリガーするためのユーザーインタラクションが必要なので、その性質上、ボリュームを制御するのは明らかに難しいです。 場合によっては、トランザクションメールを正式なプランなしで簡単に移行できます。 他の場合は、各メッセージタイプを時間の経過と共に移行して、ボリュームを徐々に増やす方が良い場合もあります。 例えば、次のようなトランジションが必要な場合があります。

1. 購入確認 – 一般的に高いエンゲージメント
2. 買い物かごの放棄（通常は中程度、エンゲージメントは高い）
3. ウェルカムメール – 高いエンゲージメントですが、リスト収集方法によっては不正なアドレスが含まれる場合があります
4. Winback Emails – 一般的にエンゲージメントを低下

## 製品固有のリソース

**Campaign**

* Adobe Campaignで新しいプラットフォームを開始する際の配信品質の管理について詳しくは、[&#x200B; この節 &#x200B;](/help/additional-resources/ac-starting-new-platform.md) を参照してください。
* Adobe Campaign Classicで複数のウェーブを使用して送信する方法については、[&#x200B; この節 &#x200B;](https://experienceleague.adobe.com/docs/campaign-classic/using/sending-messages/key-steps-when-creating-a-delivery/steps-sending-the-delivery.html?lang=ja#sending-using-multiple-waves) を参照してください。
* サブドメインをAdobe Campaign Classicまたは Standard に完全にデリゲートする方法については、[&#x200B; この節 &#x200B;](/help/additional-resources/ac-domain-name-setup.md) を参照してください。
* [Campaign コントロールパネル：完全なサブドメインデリゲーション（チュートリアル） &#x200B;](https://experienceleague.adobe.com/docs/campaign-classic-learn/control-panel/subdomains-and-certificates/subdomain-delegation.html?lang=ja) - *サブドメインをAdobe Campaign Classicに完全にデリゲートする方法を説明します*。
* [Campaign コントロールパネル：完全なサブドメインデリゲーション（チュートリアル） &#x200B;](https://experienceleague.adobe.com/docs/campaign-standard-learn/control-panel/subdomains-and-certificates/subdomain-delegation.html?lang=ja) - *サブドメインをAdobe Campaign Standardに完全にデリゲートする方法を説明します*。

## その他のリソース

* IP ウォーミングを使用してメールの評判を高める方法について詳しくは、[&#x200B; この節 &#x200B;](/help/additional-resources/increase-reputation-with-ip-warming.md) を参照してください。
