---
title: ボリューム — スムーズな移行方法のヒント
description: 送信するメールの量は、肯定的な評判を確立する上で重要です。 スムーズに移行するために実行できる操作を学習します。
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
source-wordcount: '573'
ht-degree: 2%

---

# ボリューム

送信するメールの量は、肯定的な評判を確立する上で重要です。 ISP の立場に立ってみましょう。知らない人から大量のトラフィックを見つけ始めると、警告を受けます。 すぐに大量のメールを送信することはリスクが高く、解決が困難な評判の問題を引き起こすことになります。 評判の悪さから自分を掘り出し、大量の送信が早すぎることに起因する問題を強制し、ブロックすることは、苛立たしく、時間がかかり、コストがかかる場合があります。

ボリュームのしきい値は、ISP によって異なり、平均エンゲージメント指標によって異なる場合があります。 一部の送信者は非常に低く遅いボリュームのランプを必要としますが、他の送信者はボリュームの急なランプを許可します。 カスタマイズしたボリュームプランの作成には、Adobe配信品質コンサルタントなどのエキスパートと協力することをお勧めします。

スムーズに移行する方法に関するヒントとヒントを次に示します。

* **権限** は、成功した電子メールプログラムの基盤です。
* **低速および遅い**  — 送信量が少ない状態から始め、送信者の評判を高めるにつれて増加します。
* A **タンデム郵送戦略** を使用すると、E メールカレンダーを中断することなく、現在の ESP を使用して巻き下げながら、Campaign のボリュームを増やすことができます。
* **エンゲージメントの問題**  — 電子メールを定期的に開封し、クリックする購読者から始めます。
* **計画に従う**  — アドビの推奨事項は、数百人の Campaign クライアントが電子メールプログラムを強化するのに役立ちました。
* **返信メールアカウントを監視する**. noreply@xyz.comを使用したり応答しなかったりするのは、お客様にとって悪い経験です。
* 非アクティブなアドレスは、配信品質に悪影響を与える可能性があります。 **現在のプラットフォームでの再アクティブ化と再権限設定**&#x200B;新しい IP ではなく、
* **ドメイン**  — 会社の実際のドメインのサブドメインである送信ドメインを使用します
   * 例えば、会社のドメインがxyz.comの場合、email.xyz.comはxyzemail.comよりも多くの信頼性を ISP に提供します
* **透明**  — メールドメインの登録の詳細は公開されている必要があり、非公開にする必要はありません。

多くの状況で、トランザクションメールは、従来のプロモーションウォーミングアプローチに従っていません。 トランザクションメールのボリュームを制御するのは、その性質上明らかに困難です。これは、通常、E メールのタッチをトリガーするユーザー操作が必要になるからです。 正式な計画を立てずに、トランザクションメールを簡単に移行できる場合もあります。 時間の経過と共に各メッセージタイプを移行し、ボリュームを徐々に増やす方が良い場合もあります。 例えば、次のように移行するとします。

1. 購入確認 — 高エンゲージメントの一般
2. 買い物かごの放棄 — 中 — 高エンゲージメントの一般
3. お知らせメール — エンゲージメントは高いものの、リスト収集方法に応じて不正なアドレスが含まれる場合があります
4. E メールの戻し — エンゲージメントの一般的な低下

## 製品固有のリソース

**Campaign**

* でAdobe Campaignを使用して新しいプラットフォームを開始する際の配信品質の管理の詳細 [この節](/help/additional-resources/ac-starting-new-platform.md).
* でAdobe Campaign Classicで複数のウェーブを使用して送信する方法を説明します。 [この節](https://experienceleague.adobe.com/docs/campaign-classic/using/sending-messages/key-steps-when-creating-a-delivery/steps-sending-the-delivery.html?lang=ja#sending-using-multiple-waves).
* でサブドメインをAdobe Campaign Classicまたは Standard に完全にデリゲートする方法を説明します。 [この節](/help/additional-resources/ac-domain-name-setup.md).
* [Campaign コントロールパネル：完全なサブドメインデリゲーション（チュートリアル）](https://experienceleague.adobe.com/docs/campaign-classic-learn/control-panel/subdomains-and-certificates/subdomain-delegation.html) - *サブドメインをAdobe Campaign Classicに完全にデリゲートする方法を説明します。*
* [Campaign コントロールパネル：完全なサブドメインデリゲーション（チュートリアル）](https://experienceleague.adobe.com/docs/campaign-standard-learn/control-panel/subdomains-and-certificates/subdomain-delegation.html) - *サブドメインをAdobe Campaign Standardに完全にデリゲートする方法を説明します。*

## その他のリソース

* IP ウォーミングを使用した E メールの評判の向上に関する詳細 [この節](/help/additional-resources/increase-reputation-with-ip-warming.md).
