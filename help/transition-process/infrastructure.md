---
title: インフラ
description: '電子メールインフラストラクチャを適切に構築するために必要な要件を学びます。 '
feature: トランジションプロセス
topics: Deliverability
kt: 7052
thumbnail: kt7052.jpg
doc-type: article
activity: understand
team: ACS
translation-type: tm+mt
source-git-commit: 1e539b5df54250a5927701009e7a9c84e5d73fae
workflow-type: tm+mt
source-wordcount: '912'
ht-degree: 0%

---


# インフラ

配信品質の成功は、強力な基盤に左右されます。 電子メールインフラストラクチャは中核的な要素です。 適切に構成された電子メールインフラストラクチャには、ドメインとIPアドレスの複数のコンポーネントが含まれます。 これらの部品は送信する電子メールの背後にある機械のようなもので、よく評判を送るアンカーになります。 配信品質コンサルタントは、導入時にこれらの要素が適切に設定されることを確認しますが、評判の要素が原因で、この基本的な理解を持つことが重要です。

## ドメインの設定と方法{#domain-setup-and-strategy}

時代が変わり、一部のISP（GmailやYahooなど）は、送信者に電子メールの評判を付ける際に、ドメインの評判を追加のポイントとして組み込んでいます。 ドメインの評価は、IPアドレスではなく、送信側ドメインに基づいています。 これは、ISPのフィルタリング決定に関しては、ブランドが優先されることを意味します。

Adobeプラットフォームの新しい送信者に対するオンボーディングプロセスには、送信ドメインの設定、およびインフラストラクチャの正しい確立が含まれます。 長期的に使用する予定のドメインについては、専門家に相談する必要があります。 次に、良いドメイン戦略を形成するヒントを示します。

* ユーザーがメールをスパムと誤認しないように、選択したドメインでのブランドの明確性と反映をできるだけ明確にしてください。 例えば、newsletter.foo.com、receipts.foo.comなどがあります。
* 親ドメインや会社ドメインは、組織からISPへのメールの配信に影響を与える可能性があるので、使用しないでください。
* 親ドメインのサブドメインを使用して、送信ドメインを正当化することを検討します。
* トランザクションメッセージドメインとマーケティングメッセージカテゴリ用にサブドメインを分けます。 これは、ISPがこの送信方法を探すので、電子メールトラフィックの流れをより信頼性の高いものにします。これは既知の電子メールのベストプラクティスであり、非常に推奨されています。

## IP戦略{#ip-strategy}

肯定的な評判を確立するのに役立つように、適切に構成されたIP戦略を策定することが重要です。 IPの数と設定は、ビジネスモデルとマーケティングの目標に応じて異なります。 専門家と協力して、適切に開始するための明確な戦略を策定します。 注意が必要な点を次に示します。

* **IPscan** トリガーの評判の問題が多すぎるのは、スマーから **スノーシューへの共通の戦術なのです**。これは、スパムメールの配信を最大限に高めるために、トラフィックが多数のIPにまたがるスパマーが使用する戦術です。スパム業者ではないにもかかわらず、IPが多すぎる場合、特にこれらのIPに以前のトラフィックがない場合は、IPが多すぎる場合に1つに見えることがあります。
* **IPscanの数が少なすぎると、スループットの問題が発生し、トリガーの評判の問題が発生する可能性があり** ます。スループットは、ISPによって異なります。 ISPが受け入れる時間と時間は、通常、インフラストラクチャと評判のしきい値に基づいて決定されます。
* メッセージングタイプに応じたトラフィックの分離が重要です。 最低でも、個別のIPプール上にマーケティングメールとトランザクションメールを個別に配置することが重要です。
* メール戦略に応じて、評価が大幅に異なる場合は、異なる製品やマーケティングストリームを異なるIPプールに分けることもお勧めします。 一部のマーケターは、地域別にセグメント化することもできます。 IPを低い評価を持つトラフィックと切り離しても、評価の問題は修正されませんが、「良い」評価の電子メール配信の問題は回避されます。 結局、リスキーなオーディエンスのために良い情報を犠牲にしたくない

## フィードバックループ{#feedback-loops}

内部では、Adobeプラットフォームがバウンス、苦情、申し込み解除などに関するデータを処理しています。 これらのフィードバックループの設定は、配信品質の重要な側面です。 苦情は評判を損なう可能性があるので、ターゲットオーディエンスからの苦情を登録した電子メールアドレスを送信する必要があります。 Gmailがこのデータを返さないことに注意してください。 リストの登録解除ヘッダーとエンゲージメントフィルターは、現在、大部分の加入者データベースを構成するGmailの加入者にとって特に重要です。

## 認証 {#authentication}

認証とは、ISPが送信者のIDを検証するために使用するプロセスです。 最も一般的な認証プロトコルは、[!DNL Sender Policy Framework](SPF)と[!DNL DomainKeys Identified Mail](DKIM)の2つです。 これらはエンドユーザには表示されませんが、ISPが確認済みの送信者からの電子メールをフィルタするのに役立ちます。 [!DNL Domain-based Message Authentication Reporting and Conformance] (DMARC)は人気を集めていますが、そのポリシーは評判システムのすべてのISPに組み込まれているわけではありません。

### SPF

[!DNL Sender Policy Framework] (SPF)は、ドメインの所有者が、そのドメインからのメールの送信に使用するメールサーバーを指定できる認証方式です。

### DKIM

[!DNL Domain Keys Identified Mail] (DKIM)は、偽造された送信者アドレスの検出（一般にスプーフィング）に使用される認証方式です。DKIMが有効な場合、受信者は、送信者がそのドメインからのメールの送信を許可されているかどうかを確認できます。

### DMARC

[!DNL Domain-based Message Authentication, Reporting and Conformance] (DMARC)は、ドメイン所有者がドメインを不正使用から保護できる認証方式です。DMARCは、SPF、DKIM、またはその両方を使用して、ドメインの所有者が認証に失敗したメールに対する処理を制御できるようにします。配信済み、検疫済み、または拒否済み。

## 製品固有のリソース

**Campaign**

* [このセクション](/help/additional-resources/ac-domain-name-setup.md)で、サブドメインをAdobe Campaign Classicまたは標準に完全に委任する方法を説明します。
* [Campaign コントロールパネル:完全なサブドメインの委任（チュートリアル）](https://experienceleague.corp.adobe.com/docs/campaign-classic-learn/control-panel/subdomains-and-certificates/subdomain-delegation.html)  — サブドメインを完全にAdobe Campaign Classicに委任する方法を *学びます。*
* [Campaign コントロールパネル:完全なサブドメインの委任（チュートリアル）](https://experienceleague.corp.adobe.com/docs/campaign-standard-learn/control-panel/subdomains-and-certificates/subdomain-delegation.html)  — サブドメインを完全にAdobe Campaign Standardに委任する方法を *学びます。*
* [このセクション](/help/additional-resources/acc-technical-recommendations.md#feedback-loop-acc)で、Campaign Classicインスタンスにフィードバックループを実装する方法の詳細を説明します。

## その他のリソース

* SPF、DKIM、およびDMARCの認証方法に関する詳細は、[このセクション](/help/additional-resources/authentication.md)を参照してください。
* [このセクション](/help/additional-resources/increase-reputation-with-ip-warming.md)では、IPの暖機を使ってメールの評判を高める方法について説明します。
