---
title: ボリューム — スムーズな移行方法のヒント
description: 送信するメールの量は、肯定的な評判を確立する上で重要です。 スムーズに移行するために実行できる操作を説明します。
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

送信するメールの量は、肯定的な評判を確立する上で重要です。 ISPの立場に立ってみると、知らない人から大量のトラフィックを見つけ始めると、警告が出る。 すぐに大量のメールを送信することは危険で、解決が困難な評判の問題を引き起こすことになります。 悪い評判を自分自身に押し付け、大量に送信するのが早すぎることから生じる問題を強引にし、ブロックするのは、苛立たしく、時間がかかり、コストがかかる場合があります。

ボリュームのしきい値は、ISPによって異なり、平均エンゲージメント指標によって異なる場合もあります。 一部の送り手は、非常に低く遅いボリュームの傾きを必要としますが、他の送り手は、ボリュームの急な傾きを許容します。 カスタマイズしたボリュームプランの作成は、Adobe配信品質コンサルタントなどのエキスパートと協力してお勧めします。

スムーズに移行する方法に関するヒントとヒントを次に示します。

* **** 権限は、成功した電子メールプログラムの基盤です。
* **低速**  — 送信量が少なくなり、送信者のレピュテーションを確立するにつれて増加します。
* **連携メーリング戦略**&#x200B;を使用すると、Eメールカレンダーを中断することなく、現在のESPを巻き込みながら、Campaignのボリュームを増やすことができます。
* **エンゲージメントが重要** ：まず、Eメールを定期的に開いてクリックする購読者から始めます。
* **プランに従う** ：アドビの推奨事項は、数百人のCampaignクライアントがEメールプログラムを正常に強化するのに役立ちました。
* **返信電子メールアカウントを監視します**。顧客がnoreply@xyz.comを使用したり応答しなかったりするのは、悪い経験です。
* 非アクティブなアドレスは、配信品質に悪影響を与える可能性があります。 **新しいIPではなく、現在のプラットフォーム**&#x200B;を再アクティブ化して再権限を設定します。
* **ドメイン**  — 会社の実際のドメインのサブドメインである送信ドメインを使用します
   * 例えば、会社のドメインがxyz.comの場合、email.xyz.comはxyzemail.comよりもISPに対する信頼性が高くなります
* **透明性**  - Eメールドメインの登録詳細は公開されている必要があり、非公開にすべきではありません。

多くの状況で、トランザクションメールは従来のプロモーションウォーミングアプローチに従っていません。 トランザクションメールのボリュームを制御するのは、Eメールのタッチをトリガーするユーザー操作が一般的に必要なので、明らかに困難です。 正式な計画を立てずに、トランザクションメールを簡単に移行できる場合もあります。 時間の経過と共に各メッセージタイプを移行し、ボリュームを徐々に増やす方が良い場合もあります。 例えば、次のように切り替えることができます。

1. 購入の確認 — 高いエンゲージメントは一般的に
2. 買い物かごの放棄 — 中 — 高エンゲージメントの一般
3. お知らせメール — エンゲージメントは高いものの、リストの収集方法によっては不正なアドレスが含まれる場合があります
4. Winback Eメール：通常はエンゲージメントの低下

## 製品固有のリソース

**Campaign**

* Adobe Campaignで新しいプラットフォームを開始する際の配信品質の管理について詳しくは、[この節](/help/additional-resources/ac-starting-new-platform.md)を参照してください。
* [この節](https://experienceleague.adobe.com/docs/campaign-classic/using/sending-messages/key-steps-when-creating-a-delivery/steps-sending-the-delivery.html#sending-using-multiple-waves)では、Adobe Campaign Classicで複数のウェーブを使用して送信する方法を説明します。
* [この節](/help/additional-resources/ac-domain-name-setup.md)で、サブドメインをAdobe Campaign ClassicまたはStandardに完全にデリゲートする方法を説明します。
* [Campaign コントロールパネル:完全なサブドメインデリゲーション(チュート](https://experienceleague.adobe.com/docs/campaign-classic-learn/control-panel/subdomains-and-certificates/subdomain-delegation.html)  *リアル) — サブドメインをAdobe Campaign Classicに完全にデリゲートする方法を説明します。*
* [Campaign コントロールパネル:完全なサブドメインデリゲーション(チュート](https://experienceleague.adobe.com/docs/campaign-standard-learn/control-panel/subdomains-and-certificates/subdomain-delegation.html)  *リアル) — サブドメインをAdobe Campaign Standardに完全にデリゲートする方法を説明します。*

## その他のリソース

* [この節](/help/additional-resources/increase-reputation-with-ip-warming.md)でIPウォーミングを使用してEメールの評判を高める方法について詳しく説明します。
