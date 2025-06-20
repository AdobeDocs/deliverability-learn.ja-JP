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
source-wordcount: '898'
ht-degree: 2%

---

# インフラストラクチャ

配信品質を成功させるには、強力な基盤が必要です。 メールインフラストラクチャはコア要素です。 適切に構築されたメールインフラストラクチャには、複数のコンポーネント（ドメインと IP アドレス）が含まれます。 これらのコンポーネントは、送信するメールの背後にある機械のようなもので、多くの場合、送信の評判のアンカーになります。 配信品質コンサルタントは、実装時にこれらの要素が適切に設定されるようにしますが、レピュテーション要素により、この基本的な理解を持つことが重要です。

## ドメインの設定と戦略 {#domain-setup-and-strategy}

時代は変わり、一部の ISP （Gmail や Yahoo など）では、メールの評判を送信者に添付する際に、ドメインの評判を追加のポイントとして取り入れるようになりました。 ドメインレピュテーションは、IP アドレスではなく送信ドメインに基づきます。 つまり、ISP フィルタリングの決定に関しては、ブランドが優先されます。

Adobeプラットフォームにおける新しい送信者のオンボーディングプロセスの一部として、送信ドメインの設定や、インフラストラクチャが適切に確立されているかどうかの確認が含まれます。 長期的に使用する予定のドメインに関しては、エキスパートと相談する必要があります。 適切なドメイン戦略を形成するためのヒントを以下に示します。

* ユーザーがメールをスパムと誤って識別しないように、選択したドメインでブランドをできるだけ明確に反映させます。 例として、newsletter.foo.com、receipts.foo.comなどがあります。
* 組織から ISP へのメールの配信に影響を与える可能性があるので、親ドメインまたは会社ドメインを使用しないでください。
* 送信ドメインを正当化するには、親ドメインのサブドメインの使用を検討します。
* トランザクションメッセージカテゴリとマーケティングメッセージカテゴリのサブドメインを分離します。 これは、ISP がこの送信方法を探すので、より信頼性の高いベースでメールトラフィックフローを実行するのに役立ちます。これは既知のメールのベストプラクティスであり、強く推奨されます。

## IP 戦略 {#ip-strategy}

肯定的な評判を確立するのに役立つ、適切に構造化された IP 戦略を形成することが重要です。 IP の数と設定の内容は、ビジネスモデルとマーケティング目標によって異なります。 エキスパートと協力して、適切に作業を開始するための明確な戦略を策定します。 注意が必要な事項を次に示します。

* **IP が多すぎる** と、スパム発信者が **snowshoe** に対して行う一般的な戦術であるため、レピュテーションの問題がトリガーになる可能性があります。この戦術は、スパム発信者が多くの IP 間でトラフィックを広め、スパムメールを最大限に配信するために使用します。 スパマーではないにもかかわらず、使用する IP が多すぎる場合、特にそれらの IP に以前のトラフィックがない場合は、スパマーのように見えるかもしれません。
* **IP が少なすぎると** スループットの問題が発生し、トリガーのレピュテーションの問題が発生する可能性があります。 スループットは ISP によって異なります。 ISP が受け入れる度合いと速度は、通常、インフラストラクチャとレピュテーションしきい値の送信に基づいています。
* トラフィックをメッセージタイプに分離することが重要です。 少なくとも、個別の IP プールで個別のマーケティングメールとトランザクションメールを設定することが重要です。
* 評価が大幅に異なる場合は、メール戦略に応じて、異なる IP プールで異なる製品やマーケティングストリームを分離することをお勧めします。 一部のマーケターは、地域ごとにセグメント化します。 レピュテーションが低いトラフィックに IP を分離しても、レピュテーションの問題は修正されませんが、「良好な」レピュテーションメール配信に関する問題は回避できます。 結局のところ、よりリスクの高いオーディエンスのために良いオーディエンスを犠牲にしたくありません。

## フィードバックループ {#feedback-loops}

バックグラウンドで、Adobeプラットフォームはバウンス、苦情、購読解除などに関するデータを処理しています。 これらのフィードバックループの設定は、配信品質にとって重要な側面です。 苦情は評判を損なう可能性があるので、ターゲットオーディエンスから苦情を登録するメールアドレスを指定する必要があります。 Gmail はこのデータを提供しないことに注意する必要があります。 リスト登録解除ヘッダーとエンゲージメントフィルタリングは、購読者データベースの大部分を占めるようになった Gmail 購読者にとって特に重要です。

## 認証 {#authentication}

認証は、ISP が送信者の ID を検証するために使用するプロセスです。 最も一般的な 2 つの認証プロトコルは、[!DNL Sender Policy Framework] （SPF）と [!DNL DomainKeys Identified Mail] （DKIM）です。 これらは、エンドユーザーには表示されませんが、ISP が検証済みの送信者からメールをフィルタリングするのに役立ちます。 [!DNL Domain-based Message Authentication Reporting and Conformance] （DMARC）は人気を博していますが、そのポリシーは、まだ一部の ISP の評判システムに組み込まれていません。

### SPF

[!DNL Sender Policy Framework] （SPF）は、ドメインの所有者が、そのドメインからメールを送信するために使用するメールサーバーを指定できる認証方法です。

### DKIM

[!DNL Domain Keys Identified Mail] （DKIM）は、偽造された送信者アドレス（一般的にスプーフィングと呼ばれます）の検出に使用される認証方法です。 DKIM が有効になっている場合、送信者がそのドメインからのメールを送信する権限を持っているかどうかを受信者が確認できます。

### DMARC

[!DNL Domain-based Message Authentication, Reporting and Conformance] （DMARC）は、ドメイン所有者がドメインを不正使用から保護できるようにする認証方法です。 DMARC では、SPF、DKIM、またはその両方を使用して、ドメイン所有者が、認証に失敗したメールの配信済み、強制隔離、拒否を制御できるようにします。

## 製品固有のリソース

**Campaign**

* サブドメインをAdobe Campaign Classicまたは Standard に完全にデリゲートする方法については、[ この節 ](/help/additional-resources/ac-domain-name-setup.md) を参照してください。
* [Campaign コントロールパネル：完全なサブドメインデリゲーション（チュートリアル） ](https://experienceleague.adobe.com/docs/campaign-classic-learn/control-panel/subdomains-and-certificates/subdomain-delegation.html?lang=ja) - *サブドメインをAdobe Campaign Classicに完全にデリゲートする方法を説明します*。
* [Campaign コントロールパネル：完全なサブドメインデリゲーション（チュートリアル） ](https://experienceleague.adobe.com/docs/campaign-standard-learn/control-panel/subdomains-and-certificates/subdomain-delegation.html?lang=ja) - *サブドメインをAdobe Campaign Standardに完全にデリゲートする方法を説明します*。
* Campaign Classicインスタンスのフィードバックループの実装について詳しくは、[ この節 ](/help/additional-resources/acc-technical-recommendations.md#feedback-loop-acc) を参照してください。

## その他のリソース

* SPF、DKIM、DMARC の認証方法について詳しくは、[ この節 ](/help/additional-resources/authentication.md) を参照してください。
* IP ウォーミングを使用してメールの評判を高める方法について詳しくは、[ この節 ](/help/additional-resources/increase-reputation-with-ip-warming.md) を参照してください。
