---
title: ボリューム – スムーズに移行する方法のヒント
description: 電子メールの配信数は、肯定的なレピュテーションを確立する上で重要です。 スムーズに移行するために何ができるかを解説します。
topics: Deliverability
jira: KT-7055
thumbnail: kt7055.jpg
doc-type: article
activity: understand
role: Admin,User
level: Beginner
team: ACS
exl-id: 1bc56061-0c64-4033-b49c-66618916bca6
TQID: https://experienceleague.adobe.com/piIfp9yQkAa1F1bkO9zM7PcOConZhTrwARo4Y8wtMsQ
product_v2: id: b27e5950-9033-45ac-9f86-eb22e567f615id: d0a3eab4-7b10-4d96-a71e-6c0f8e7b7c87id: dfc56824-e8b9-499e-85d4-21aedb507314
feature_v2: id: e64968b2-4ee5-47f9-8cae-0588f184b9ebid: f71e690b-4480-4b67-9ef5-88f42f9cdfdb
role_v2: id: b69b2659-1057-424e-8fc5-ed9e016dc554id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
level_v2: id: e8ccd51f-da0d-4e3b-939b-e30d5ebb1ea5
source-git-commit: 75df8537199680e5f1fc4b98cefdb05220fee7bf
workflow-type: tm+mt
source-wordcount: 600
ht-degree: 4%

---

# ボリューム

電子メールの配信数は、肯定的なレピュテーションを確立する上で重要です。 ISPは、未知の送信者から大量のトラフィックが流入すると警戒します。 膨大な電子メールをすぐに送信するのはリスクが高く、多くの場合、解決が困難なレピュテーションの問題を引き起こします。 レピュテーションの低下だけでなく、バルク指定やブロックの問題に対処することは、多くの時間、コスト、労力を要します。

配信数のしきい値は、ISPや平均エンゲージメント指標によって異なります。 徐々に時間をかけて配信数を増やす必要がある送信者もいれば、配信数の急増に対応できる送信者もいるでしょう。 Adobeの配信品質コンサルタントなどの専門家と協力して、カスタマイズされたプランを作成することをお勧めします。

移行をスムーズに行うためのヒントとヒントを以下に示します。

* **権限**&#x200B;は、成功したメールプログラムの基盤です。
* **低速および低速** – 低い送信量から開始し、送信者としてのレピュテーションを確立してから増量します。
* **タンデムメール配信戦略**&#x200B;を使用すると、メールカレンダーを中断することなく、現在のESPの運用を縮小しながら、Campaignの配信数を増やすことができます。
* **エンゲージメントが重要** – 電子メールを定期的に開いてクリックする購読者から始めます。
* **計画に従う** – アドビの提案は、何百人ものCampaign クライアントがメールプログラムを正常に展開するのに役立ちました。
* **返信電子メールアカウントを監視**。 お客様がnoreply@xyz.comを使用したり、応答しなかったりすることは、悪いエクスペリエンスです。
* 非アクティブなアドレスは、配信品質に悪影響を与える可能性があります。 **新しいIPではなく、現在のプラットフォーム**&#x200B;で再アクティブ化して再権限を付与します。
* **ドメイン** – 企業の実際のドメインのサブドメインである送信ドメインを使用します
   * 例えば、会社のドメインがxyz.comの場合、email.xyz.comはxyzemail.comよりもISPに対する信頼性が高くなります
* **透明性** – 電子メールドメインの登録の詳細は公開する必要があります。非公開にしないでください。

多くの場合、トランザクションメールは、従来のプロモーションウォーミングアプローチに従っていません。 トランザクションメールはその性質上、ボリュームを制御するのは明らかに困難です。通常、メールのタッチをトリガーするにはユーザーの操作が必要です。 場合によっては、トランザクションメールは正式な計画がなくても送信できます。 それ以外の場合、それぞれのメッセージタイプを時間をかけて送信し、ゆっくりとボリュームを増やす方がよいこともあります。 例えば、次のように送信できます。

1. 購入確認 – 一般的に高いエンゲージメント
2. カートの放棄 – 中～高程度のエンゲージメントを提供
3. ウェルカムメール – 高いエンゲージメント。ただし、リストの収集方法によっては不正なアドレスが含まれる場合があります
4. 顧客再獲得メール – 一般的にエンゲージメントが低い

## 製品固有のリソース

**Campaign**

* Adobe Campaignで新しいプラットフォームを開始する際の配信品質の管理について詳しくは、[この節](/help/additional-resources/ac-starting-new-platform.md)を参照してください。
* Adobe Campaign Classicで複数のウェーブを使用して送信する方法については、[この節](https://experienceleague.adobe.com/docs/campaign-classic/using/sending-messages/key-steps-when-creating-a-delivery/steps-sending-the-delivery.html?lang=ja#sending-using-multiple-waves)を参照してください。
* サブドメインをAdobe Campaign ClassicまたはStandardに完全にデリゲートする方法については、[この節](/help/additional-resources/ac-domain-name-setup.md)を参照してください。
* [Campaign コントロールパネル：完全なサブドメインのデリゲーション（チュートリアル） ](https://experienceleague.adobe.com/docs/campaign-classic-learn/control-panel/subdomains-and-certificates/subdomain-delegation.html) - *サブドメインをAdobe Campaign Classicに完全にデリゲートする方法を説明します。*
* [Campaign コントロールパネル：完全なサブドメインのデリゲーション（チュートリアル） ](https://experienceleague.adobe.com/docs/campaign-standard-learn/control-panel/subdomains-and-certificates/subdomain-delegation.html) - *サブドメインをAdobe Campaign Standardに完全にデリゲートする方法を説明します。*

## その他のリソース

* IP ウォーミングによる電子メールのレピュテーションの向上について詳しくは、[この節](/help/additional-resources/increase-reputation-with-ip-warming.md)を参照してください。
