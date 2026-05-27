---
title: インフラストラクチャ
description: 電子メールインフラストラクチャの適切な構築に必要な要件について説明します。
topics: Deliverability
jira: KT-7052
thumbnail: kt7052.jpg
doc-type: article
activity: understand
role: Admin, Leader
level: Beginner
team: ACS
exl-id: 4025d95c-cc77-4e0c-9904-aaf60019b18c
TQID: https://experienceleague.adobe.com/FWlVtNGACEM6dKsnYQJU-z04mP902M5EXZmxxsKDyqU
product_v2:
  - id: b27e5950-9033-45ac-9f86-eb22e567f615
  - id: d0a3eab4-7b10-4d96-a71e-6c0f8e7b7c87
  - id: dfc56824-e8b9-499e-85d4-21aedb507314
feature_v2:
  - id: b0bb9048-d951-48d8-8232-45cf248a7e27
  - id: c5f60233-d5ea-4453-a799-0ad258b4d399
  - id: e2290edd-b061-4880-9d79-dee306cf5aa9
  - id: ea90ebee-5c84-42d9-8b21-006bdabc95a3
  - id: f71e690b-4480-4b67-9ef5-88f42f9cdfdb
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
  - id: f8a45b24-4be7-4f1b-909b-60d06b483a20
level_v2:
  - id: e8ccd51f-da0d-4e3b-939b-e30d5ebb1ea5
topic_v2:
  - id: aa2f3246-cb95-4b30-8899-fdf7d73550cc
  - id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
source-git-commit: 75df8537199680e5f1fc4b98cefdb05220fee7bf
workflow-type: tm+mt
source-wordcount: 923
ht-degree: 2%

---

# インフラストラクチャ

配信品質の成功は、優れた基盤の存在にかかっています。 メール基盤は中核的な要素です。 適切に構築されたメール基盤は、複数の要素（ドメインとIP アドレス）で構成されています。 これらの要素は、メール送信プロセスを構成し、多くの場合、送信レピュテーションを大きく左右します。 配信コンサルタントは、実装中にこれらの要素が適切に設定されていることを確認します。ただし、レピュテーションに影響を与えるため、次の基本的な理解を得ることが重要です。

## ドメインの設定と戦略 {#domain-setup-and-strategy}

時代は変わり、一部のISP （GmailやYahooなど）では、電子メールのレピュテーションを送信者に添付する際に、追加のポイントとして「ドメインのレピュテーション」が組み込まれるようになりました。 ドメインのレピュテーションは、IP アドレスではなく送信ドメインに基づいています。 つまり、ISP フィルタリングの決定においては、IP アドレスではなく企業が優先されます。

Adobeプラットフォームにおける新規送信者のオンボーディングプロセスでは、送信ドメインを設定し、インフラストラクチャが適切に確立されていることを確認します。 長期的に使用する予定のドメインについては、専門家の協力を得る必要があります。 適切なドメイン戦略を策定するためのヒントを以下に示します。

* 迷惑メールとして判定されないようにするために、選択したドメインにブランディングを明確に反映させます。 例えば、newsletter.foo.comやreceipts.foo.comなどがあります。
* 親ドメインや会社ドメインは使用しないでください。自社からISPへのメール配信に影響を与える可能性があります。
* 送信ドメインが正当なものであると認識されるようにするために、親ドメインのサブドメインの使用を検討してください。
* トランザクションメッセージとマーケティングメッセージのサブドメインを分離します。 これにより、ISPがこの送信方法を検討するため、より信頼性の高いメールトラフィックが流入できるようになります。これは、メールのベストプラクティスとして知られており、強くお勧めします。

## IP 戦略 {#ip-strategy}

適切に策定されたIP戦略により、肯定的なレピュテーションを確立することが重要です。 IPの数や設定の内容は、ビジネスモデルとマーケティング目標によって異なります。 専門家と連携し、明確な戦略を策定しましょう。 次の点を考慮することが重要です。

* **IP**&#x200B;が多すぎると、レピュテーションの問題がトリガーされる可能性があります。これは、**スノーシュー**&#x200B;に対するスパム送信者の一般的な戦術であり、スパム メールの配信を最大化するために、多くのIPにトラフィックが分散しているスパム送信者が使用する戦術です。 実際には迷惑メール送信者ではなくても、多くのIP アドレスを使用し、それらのIP アドレスでトラフィックが検出されない場合、迷惑メール送信者とみなされることがあります。
* **IP数が少なすぎると、スループットの問題やトリガーレピュテーションの問題が発生する可能性があります。**&#x200B;スループットはISPによって異なります。 ISPが受け入れる可能性と速度は、通常、メール基盤と送信レピュテーションのしきい値に基づいています。
* メッセージの種類ごとにトラフィックを分離することが重要です。 少なくとも、マーケティングメールとトランザクションメールを個別のIP プールに分離することが重要です。
* メール戦略によっては、レピュテーションが大きく異なる場合は、IP プールごとに異なる製品やマーケティングストリームを分離することをお勧めします。 一部のマーケターは、IP アドレスを地域ごとにセグメント化しています。 レピュテーションが低いトラフィックにIPを分離しても、レピュテーションの問題は修正されません。しかし、「良好な」レピュテーションメール配信に関する問題を回避できます。 リスクの高いオーディエンスのために、優良なオーディエンスを犠牲にしないようにする必要があります。

## フィードバックループ {#feedback-loops}

Adobeのソリューションは、バウンス、苦情、登録解除などのデータをバックグラウンドで処理しています。 これらのフィードバックループの設定は、配信品質における重要な要素です。 苦情によってレピュテーションが低下する可能性があるので、ターゲットオーディエンスから苦情が寄せられた場合、該当するメールアドレスを登録する必要があります。 ただし、Gmailはこのデータを提供しません。 多くの顧客がGmailを利用している場合、リスト登録解除ヘッダーとエンゲージメントフィルタリングを活用することが特に重要となります。

## 認証 {#authentication}

認証とは、ISPが送信者の身元を検証するために使用するプロセスです。 最も一般的な2つの認証プロトコルは、[!DNL Sender Policy Framework] （SPF）と[!DNL DomainKeys Identified Mail] （DKIM）です。 これらは、エンドユーザー側からは見えませんが、ISPが検証済みの送信者の電子メールをフィルタリングするのに役立ちます。[!DNL Domain-based Message Authentication Reporting and Conformance] （DMARC）は人気を博していますが、そのポリシーは、すべてのISPがレピュテーションシステムに組み込まれているわけではありません。

### SPF

[!DNL Sender Policy Framework] （SPF）は、ドメイン所有者が、そのドメインからメールを送信するために使用するメールサーバーを指定できる認証方法です。

### DKIM

[!DNL Domain Keys Identified Mail] （DKIM）は、偽装された送信者アドレス （一般的にスプーフィングと呼ばれます）の検出に使用される認証方法です。 DKIMが有効になっている場合、送信者がそのドメインからメールを送信する権限を持っているかどうかを受信者が確認できます。

### DMARC

[!DNL Domain-based Message Authentication, Reporting and Conformance] （DMARC）は、ドメイン所有者がドメインを不正使用から保護できるようにする認証方法です。 DMARCでは、SPF、DKIM、またはその両方を使用して、ドメイン所有者が、認証に失敗したメールの処理（配信、強制隔離、拒否）を制御できるようにします。

## 製品固有のリソース

**Campaign**

* サブドメインをAdobe Campaign ClassicまたはStandardに完全にデリゲートする方法については、[この節](/help/additional-resources/ac-domain-name-setup.md)を参照してください。
* [Campaign コントロールパネル：完全なサブドメインのデリゲーション（チュートリアル） &#x200B;](https://experienceleague.adobe.com/docs/campaign-classic-learn/control-panel/subdomains-and-certificates/subdomain-delegation.html?lang=ja) - *サブドメインをAdobe Campaign Classicに完全にデリゲートする方法を説明します。*
* [Campaign コントロールパネル：完全なサブドメインのデリゲーション（チュートリアル） &#x200B;](https://experienceleague.adobe.com/docs/campaign-standard-learn/control-panel/subdomains-and-certificates/subdomain-delegation.html?lang=ja) - *サブドメインをAdobe Campaign Standardに完全にデリゲートする方法を説明します。*
* Campaign Classic インスタンスに対するフィードバックループの実装について詳しくは、[この節](/help/additional-resources/acc-technical-recommendations.md#feedback-loop-acc)を参照してください。

## その他のリソース

* SPF、DKIM、DMARCの認証方法について詳しくは、[この節](/help/additional-resources/authentication.md)を参照してください。
* IP ウォーミングによる電子メールのレピュテーションの向上について詳しくは、[この節](/help/additional-resources/increase-reputation-with-ip-warming.md)を参照してください。
