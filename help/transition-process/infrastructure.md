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
source-git-commit: 6b312cdbba496818337c97ec4f42962aea757901
workflow-type: tm+mt
source-wordcount: '910'
ht-degree: 2%

---

# インフラストラクチャ

配信品質の向上は、強力な基盤に依存しています。 E メールインフラストラクチャは、中核的な要素です。 適切に構築された E メールインフラストラクチャには、複数のコンポーネント（ドメインと IP アドレス）が含まれます。 これらのコンポーネントは、送信する E メールの背後にある機械のようなもので、しばしば評判を送る錨となります。 配信品質コンサルタントは、実装時にこれらの要素が適切に設定されていることを確認しますが、レピュテーション要素が原因で、この基本的な理解を持つことが重要です。

## ドメインの設定と戦略 {#domain-setup-and-strategy}

時間が変わり、一部の ISP（Gmail や Yahoo など）では、E メールの評判を送信者に付け加える際に、ドメインの評判を追加のポイントとして取り込むようになりました。 ドメインのレピュテーションは、IP アドレスではなく、送信ドメインに基づいています。 つまり、ISP のフィルタリングの決定に関しては、ブランドが優先されます。

Adobeプラットフォームでの新しい送信者のオンボーディングプロセスの一部には、送信ドメインの設定と、インフラストラクチャが正しく確立されていることの確認が含まれます。 長期的に使用する予定のドメインについては、エキスパートと協力する必要があります。 次に、優れたドメイン戦略を形成するためのヒントを示します。

* ユーザーがメールをスパムとして誤って識別しないように、選択したドメインでブランドをできるだけ明確に反映します。 例として、newsletter.foo.com、receipts.foo.comなどがあります。
* 親ドメインや企業ドメインは、組織から ISP へのメール配信に影響を与える可能性があるので、使用しないでください。
* 送信ドメインを正式化するために、親ドメインのサブドメインの使用を検討します。
* トランザクションメッセージカテゴリとマーケティングメッセージカテゴリでサブドメインを区別します。 ISP は、既知の E メールのベストプラクティスであり、強くお勧めするこの送信方法を探すので、これは、E メールトラフィックの流れをより信頼性の高いものにするのに役立ちます。

## IP 戦略 {#ip-strategy}

肯定的な評判を確立するのに役立つ、適切に構造化された IP 戦略を作成することが重要です。 IP の数と設定は、ビジネスモデルとマーケティング目標に応じて異なります。 エキスパートと協力し、適切なスタートを開始するための明確な戦略を策定します。 次の点に注意してください。

* **IP が多すぎます** はスパム送信者の一般的な戦術なので、レピュテーションの問題をトリガーする可能性があります。 **スノーシュー**：スパムメールの配信を最大化するために、トラフィックが多くの IP に分散されるスパム送信者が使用する戦術です。 スパム送信者ではないのに、IP を多く使用しすぎる場合、特にこれらの IP に以前のトラフィックがない場合は、1 つのように見えることがあります。
* **IP が少なすぎます** は、スループットの問題を引き起こし、トリガーレピュテーションの問題が発生する可能性があります。 スループットは、ISP によって異なります。 ISP が受け入れるのにかかる時間と速度は、通常、インフラストラクチャに基づいており、レピュテーションのしきい値を送信します。
* メッセージングタイプに合わせてトラフィックを分離することが重要です。 最低でも、個別の IP プール上で、個別のマーケティングメールとトランザクションメールを個別におこなうことが重要です。
* メール戦略に応じて、レピュテーションが大幅に異なる場合は、異なる製品やマーケティングストリームを異なる IP プールで分離することをお勧めします。 また、一部のマーケターは、地域別にセグメント化します。 レピュテーションの低いトラフィック用に IP を分離しても、レピュテーションの問題は修正されませんが、「レピュテーションの高い」E メール配信の問題は回避されます。 結局、リスキーのために良い聴衆を犠牲にしたくないのです。

## フィードバックループ {#feedback-loops}

バックグラウンドで、Adobeプラットフォームは、バウンス、苦情、登録解除などに関するデータを処理します。 これらのフィードバックループの設定は、配信品質の重要な側面です。 苦情は評判を損なう可能性があるので、ターゲットオーディエンスからの苦情を登録する E メールアドレスを送信する必要があります。 Gmail がこのデータを返さないことに注意する必要があります。 リスト配信停止ヘッダーとエンゲージメントフィルターは、現在購読者データベースの大部分を構成する Gmail 購読者にとって特に重要です。

## 認証 {#authentication}

認証とは、ISP が送信者の ID を検証するために使用するプロセスです。 最も一般的な認証プロトコルは次の 2 つです。 [!DNL Sender Policy Framework] (SPF) および [!DNL DomainKeys Identified Mail] (DKIM)。 これらはエンドユーザーには表示されませんが、ISP が検証された送信者からの E メールをフィルタリングするのに役立ちます。 [!DNL Domain-based Message Authentication Reporting and Conformance] (DMARC) は、評判システムのすべての ISP にまだポリシーが組み込まれていないにもかかわらず、人気を集めています。

### SPF

[!DNL Sender Policy Framework] (SPF) は、ドメインの所有者が、そのドメインからメールを送信する際に使用するメールサーバーを指定できる認証方法です。

### DKIM

[!DNL Domain Keys Identified Mail] (DKIM) は、偽造された送信者アドレスの検出（一般的にスプーフィングと呼ばれます）に使用される認証方法です。 DKIM が有効な場合は、送信者がそのドメインからのメール送信を許可されているかどうかを受信者が確認できます。

### DMARC

[!DNL Domain-based Message Authentication, Reporting and Conformance] (DMARC) は、ドメインの所有者がドメインを不正使用から保護できる認証方法です。 DMARC は、SPF、DKIM、またはその両方を使用して、ドメイン所有者が認証に失敗したメールに対する影響（配信済み、強制隔離済み、拒否済み）を制御できるようにします。

## 製品固有のリソース

**Campaign**

* でサブドメインをAdobe Campaign Classicまたは Standard に完全にデリゲートする方法を説明します。 [この節](/help/additional-resources/ac-domain-name-setup.md).
* [Campaign コントロールパネル：完全なサブドメインデリゲーション（チュートリアル）](https://experienceleague.adobe.com/docs/campaign-classic-learn/control-panel/subdomains-and-certificates/subdomain-delegation.html) - *サブドメインをAdobe Campaign Classicに完全にデリゲートする方法を説明します。*
* [Campaign コントロールパネル：完全なサブドメインデリゲーション（チュートリアル）](https://experienceleague.adobe.com/docs/campaign-standard-learn/control-panel/subdomains-and-certificates/subdomain-delegation.html) - *サブドメインをAdobe Campaign Standardに完全にデリゲートする方法を説明します。*
* でCampaign Classicインスタンスのフィードバックループを実装する方法の詳細 [この節](/help/additional-resources/acc-technical-recommendations.md#feedback-loop-acc).

## その他のリソース

* の SPF、DKIM、DMARC 認証方式の詳細 [この節](/help/additional-resources/authentication.md).
* IP ウォーミングを使用した E メールの評判の向上に関する詳細 [この節](/help/additional-resources/increase-reputation-with-ip-warming.md).
