---
title: ボリューム — スムーズな移行方法のヒント
description: 送信するメールの量は、肯定的な評判を確立する上で重要です。 スムーズな移行に役立つ機能を学習します。
topics: Deliverability
kt: 7055
thumbnail: kt7055.jpg
doc-type: article
activity: understand
team: ACS
exl-id: 1bc56061-0c64-4033-b49c-66618916bca6
source-git-commit: 68c403f915287e1a50cd276b67b3f48202f45446
workflow-type: tm+mt
source-wordcount: '573'
ht-degree: 1%

---

# ボリューム

送信するメールの量は、肯定的な評判を確立する上で重要です。 Put yourself in an ISPs shoes — if you start seeing a ton of traffic from someone you don’t know, it would be alarming. すぐに大量のメールを送信することはリスクが高く、解決が困難な評判の問題を引き起こすことになります。 It can be frustrating, time consuming, and costly to dig yourself out of poor reputation and bulking and blocking issues resulting from sending too much too soon.

ボリュームのしきい値は、ISP によって異なり、平均エンゲージメント指標によって異なる場合もあります。 Some senders require a very low and slow ramp of volume, whereas others may allow for a steeper ramp in volume. カスタマイズされたボリュームプランを作成するには、Adobe配信品質コンサルタントなどのエキスパートと協力することをお勧めします。

Here’s a list of hints and tips for how to transition smoothly:

* **** 権限は、成功した電子メールプログラムの基盤です。
* **低速**  — 送信量が少ない状態から始め、送信者の評判を高めるにつれて増加します。
* **連携メーリング戦略** を使用すると、E メールカレンダーを中断することなく、現在の ESP を使用しながら Campaign のボリュームを増やすことができます。
* **エンゲージメントが重要** ：まず、E メールを定期的に開封し、クリックする購読者から始めます。
* **Follow the plan** — our recommendations have helped hundreds of Campaign clients successfully ramp up their email programs.
* **Monitor your reply email account**. It’s a bad experience for your customer to use noreply@xyz.com or to not respond.
* 非アクティブなアドレスは、配信品質に悪影響を与える可能性があります。 **新しい IP ではなく、現在のプラットフォーム**&#x200B;を再アクティブ化して再権限を設定します。
* **Domains** — use a sending domain that’s a subdomain of your company’s actual domain
   * 例えば、会社のドメインが xyz.com の場合、email.xyz.com は xyzemail.com よりも ISP に対する信頼性を高めます
* **透明性**  - E メールドメインの登録詳細は公開されている必要があり、非公開にすべきではありません。

多くの状況で、トランザクションメールは従来のプロモーションウォーミングアプローチに従っていません。 It’s obviously difficult to control volume in transactional mail due to its nature, since it generally requires a user interaction to trigger the email touch. 正式な計画を立てずに、トランザクションメールを簡単に移行できる場合もあります。 時間の経過と共に各メッセージ・タイプを移行し、ボリュームを徐々に増やす方が良い場合もあります。 例えば、次のように移行することができます。

1. 購入確認 — 高いエンゲージメントは一般的に
2. Cart abandon—medium - high engagement generally
3. お知らせメール — エンゲージメントは高いものの、リスト収集方法に応じて不正なアドレスを含む可能性がある
4. Winback emails — lower engagement generally

## 製品固有のリソース

**Campaign**

* Adobe Campaignで新しいプラットフォームを開始する際の配信品質の管理について詳しくは、[ この節 ](/help/additional-resources/ac-starting-new-platform.md) を参照してください。
* [ この節 ](https://experienceleague.adobe.com/docs/campaign-classic/using/sending-messages/key-steps-when-creating-a-delivery/steps-sending-the-delivery.html#sending-using-multiple-waves) で、Adobe Campaign Classicで複数のウェーブを使用して送信する方法を説明します。
* [ この節 ](/help/additional-resources/ac-domain-name-setup.md) で、サブドメインをAdobe Campaign Classicまたは Standard に完全にデリゲートする方法を説明します。
* [Campaign コントロールパネル:完全なサブドメインデリゲーション ( チュート](https://experienceleague.adobe.com/docs/campaign-classic-learn/control-panel/subdomains-and-certificates/subdomain-delegation.html) リアル )  *— サブドメインをAdobe Campaign Classicに完全にデリゲートする方法を説明します。*
* [Campaign コントロールパネル:完全なサブドメインデリゲーション ( チュート](https://experienceleague.adobe.com/docs/campaign-standard-learn/control-panel/subdomains-and-certificates/subdomain-delegation.html) リアル )  *— サブドメインをAdobe Campaign Standardに完全にデリゲートする方法を説明します。*

## その他のリソース

* [ この節 ](/help/additional-resources/increase-reputation-with-ip-warming.md) で IP ウォーミングで E メールの評判を高める方法について詳しく説明します。
