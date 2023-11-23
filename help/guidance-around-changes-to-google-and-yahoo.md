---
title: ' [!DNL Google]  と  [!DNL Yahoo] で発表された変更に関するガイダンス'
description: ' [!DNL Google]  と  [!DNL Yahoo] で発表された変更に関するガイダンス'
role: Admin
level: Experienced
doc-type: Article
last-substantial-update: 2023-11-06T00:00:00Z
jira: KT-14320
thumbnail: KT-14320.jpeg
exl-id: 879e9124-3cfe-4d85-a7d1-64ceb914a460
source-git-commit: be133b442284b39daa8e2dd276c2942402b4936d
workflow-type: tm+mt
source-wordcount: '1329'
ht-degree: 74%

---

# [!DNL Google] と [!DNL Yahoo] で発表された変更に関するガイダンス

10月3日（PT）、[!DNL Google] と [!DNL Yahoo] の両社は共同で、ブログを通じて予定された変更を発表しました。これらの変更は、2024年2月以降の新しい要件として業界の一般的なベストプラクティスを適用することで、ユーザーの安全を確保し、メールエクスペリエンスを向上させるように設計されています。

[https://blog.google/products/gmail/gmail-security-authentication-spam-protection/](https://blog.google/products/gmail/gmail-security-authentication-spam-protection/){target="_blank"}

![[!DNL Google] お知らせ_](/help/assets/Gmail.png)

[https://blog.postmaster.yahooinc.com/post/730172167494483968/more-secure-less-spam](https://blog.postmaster.yahooinc.com/post/730172167494483968/more-secure-less-spam){target="_blank"}

![[!DNL Yahoo] お知らせ](/help/assets/Yahoo.png)

Adobeの E メール配信品質の専門家は、必要ないように、これらのブログ投稿とリンクされたドキュメントをすべて読み上げています。 重要な留意点を以下に示します。

## [!DNL Google] と [!DNL Yahoo] が行っている内容

メールの世界には、法的要件、実用的な要件、一般的なベストプラクティスがあります。法的要件は場所によって大きく異なるので、このトピックには含まれていません。代わりに、[!DNL Google] と [!DNL Yahoo] はベストプラクティスを採用し、実用的な要件に変えています。[!DNL Google] と [!DNL Yahoo] が 2月に義務化を開始する予定の項目はどれも新しいものではなく、多くの場合、長年にわたってベストプラクティスとして推奨されてきましたが、業界内での採用は遅く、不均一でした。これは [!DNL Google] および [!DNL Yahoo]は、「E メールをユーザーにデプロイする場合（地域や業界によっては 70%もの高さになる場合があります）、これらの作業をおこなう必要があります」と、採用プロセスの進展を支援する方法です。

## 詳細内容

お客様がアドビの顧客である場合、必要なもののほとんどは既に設定の一部となっていますが、技術的にオプションである重要な項目がいくつかあり、2024年2月までに組織がこれらの項目を正しく採用および設定していることを確認する必要があります。

## DMARC：

[!DNL Google] と [!DNL Yahoo] の両社はどちらも、お客様にメールの送信に使用するドメインの DMARC レコードをリクエストします。現在、p=reject または p=quarantine の設定は必要ないので、p=none（一般的に「監視」設定と呼ばれる）の設定は、完全に受け入れ可能です。 これによって、メールの処理方法が変わることはありません。DMARC を使用しない場合と同様に、通常どおりに処理されます。これを設定することは、DMARC で自分自身を保護するための最初の手順であり、[!DNL Google] や [!DNL Yahoo] へのメールの送信を支援するという新しい利点に加えて、メールエコシステム内の任意の場所に認証の問題があるかどうかを確認するのにも役立ちます。
DMARC は現在アドビで完全にサポートされていますが、必須ではありません。無料の DMARC チェッカーを使用して、サブドメインに DMARC が設定されているかどうかを確認します。設定されてない場合は、アドビのサポートチームにお問い合わせの上、その設定を取得するための最適な方法を確認してください。

DMARC の詳細と、Marketo Engage に対する実装方法については、[こちら](https://experienceleague.adobe.com/docs/deliverability-learn/deliverability-best-practice-guide/additional-resources/technotes/implement-dmarc.html?lang=ja){target="_blank"} for Adobe Campaign or [here](https://experienceleague.adobe.com/docs/marketo/using/getting-started-with-marketo/setup/configure-protocols-for-marketo.html?lang=ja){target="_blank"}を参照してください。

## ワンクリック（リスト）登録解除：

パニックに陥るな。 [!DNL Google] と [!DNL Yahoo] は、セキュリティボットが単にジョブを実行することで、または誤ってクリックする可能性のある、メールの本文やフッター内の登録解除リンクについては触れていません。これは、「mailto」または「http/URL」バージョンの List-Unsubscribe ヘッダー機能を意味します。 これは、ユーザーが登録解除をクリックできる [!DNL Yahoo] および Gmail UI 内の機能です。Gmail は、「スパムを報告」をクリックして登録解除を行うかをユーザーに尋ねるメッセージも表示します。これにより、送信する苦情の数を減らす（苦情は評判を傷つける）ことができます（評判を損ないません）。
注意すべき点は [!DNL Google] および [!DNL Yahoo] はどちらも、「1-Click」という名前の「http/URL」オプションを参照しているので、意図的なものです。 技術的には、元の「http/URL」オプションを使用して、受信者を Web サイトにリダイレクトできます。 それは～の焦点ではない [!DNL Yahoo] および [!DNL Google]この 2 人は、更新された RFC8058 を参照し、Web サイトの代わりに HTTPSPOSTリクエストを使用して配信停止を処理し、「1-Click」にすることに重点を置いています。
Marketo Engageの場合、Adobeは既に「mailto」オプションを有効にしており、現在「http/URL」オプションをサポートしていません。 それに関するさらなる更新は、今後予定されています。
Adobe CampaignとAdobe Journey OptimizerのAdobeでは、「mailto」と「1-Click」の両方のオプションを使用することをお勧めします。

list-unsubscribe ヘッダーの必要性は、トランザクションメールには適用されません。トリガーされたメッセージ（放棄された買い物かごなど）や、サブスクライバーによって生成されない類似の通信は、[!DNL Google] や [!DNL Yahoo] などのメールボックスプロバイダーによってマーケティングと見なされ、list-unsubscribe が必要になることに注意してください。

>[!INFO]
> ソリューションに list-unsubscribe を実装する方法の詳細については、以下を確認してください。
> * [!DNL Adobe Campaign Classic]: [技術的なレコメンデーション](https://experienceleague.adobe.com/docs/deliverability-learn/deliverability-best-practice-guide/additional-resources/campaign/acc-technical-recommendations.html?lang=ja#list-unsubscribe){target="_blank"}
>* [!DNL Adobe Campaign Standard]: [List-Unsubscribe ヘッダーとは何ですか。 ACS でこれを実装する方法は？](https://experienceleague.adobe.com/docs/experience-cloud-kcs/kbarticles/KA-14778.html?lang=ja){target="_blank"}
>* [!DNL Adobe Journey Optimizer]: [メールオプトアウトの管理](https://experienceleague.adobe.com/docs/journey-optimizer/using/email/email-opt-out.html?lang=ja){target="_blank"}
>
> または、いつでもAdobeカスタマーサポートチームに連絡してください。


## 2 日以内での登録解除プロセス：

これは、しばらくの間推奨されるベストプラクティスでした。登録解除したユーザーにメールをデプロイすると、通常、スパムの苦情が発生するので、そのユーザーへのメールの送信を早く停止するほど良いでしょう。繰り返しになりますが、法的要件は場合によっては非常に長くなる可能性がありますが、[!DNL Google] と [!DNL Yahoo] は、ユーザーが List-Unsubscribe 経由で登録解除したことと、3 日目になってもメールを送信していることを認識し、そのような行為を行う送信者には、今後どのユーザーにもメールを引き続き送信することを許可しないと述べています。
この 2 日間の要件は、様々な list-unsubscribe メソッドによるすべての登録解除に適用されます。場合によっては（「mailto」のように）、Adobeがそれらを処理することを意味します。 アドビでは、すべての登録解除リクエストを受信後、2 日の制限内で直ちに処理します。場合によっては、お客様が処理する可能性があります。お客様がこれらのリクエストを処理している場合は、この 2 日間のタイムラインに合わせるために、お客様側で変更を行う必要がある場合があります。

## 苦情率：

苦情率を 0.2％未満に抑えることが、長い間ベストプラクティスとして行われてきました。[!DNL Google] は長期間にわたって基準を 0.3％と高めに設定していますが、0.1％未満に抑えることにはメリットがあると明確に述べています。共有した詳細を以下に示します。

* スパム率を 0.10％未満に抑えるようにします。
* 特に継続的にスパム率が 0.30％以上になることは避けます。
* スパム率を低く維持すると、時折急増するユーザーフィードバックに対する送信者の回復力が高まります。
* 同様に、スパム率を高く維持すると、スパムの分類が増加します。スパム率の改善がスパムの分類に積極的に反映されるまでには時間がかかる場合があります。
  [!DNL Yahoo] は、苦情のしきい値も 0.30％の範囲内になると述べています。


苦情率の監視や、苦情を減らすための戦略にサポートが必要な場合は、アドビ配信品質コンサルタントにご相談いただくか、配信品質コンサルタントがまだいない場合はアカウントチームに配信品質コンサルタントの追加についてご相談ください。

## マーケターに与える影響

Gmail と [!DNL Yahoo] のこれらの新しい要件に従わない場合、メールがスパムフォルダーに分類されるか、ブロックされることが予想されます（つまり、メールが配信されなかったことを示す MBP のバウンスが返されます）。
したがって、アドビでは、上記で概要を示した変更を実施し、できるだけ早く準拠し始めることを強くお勧めします。また、[!DNL Yahoo] と [!DNL Google] でのパフォーマンスのベンチマークを開始し、2月に向けて指標に重大な変更があるかどうかを確認するのに最適な時期でもあります。
ご質問がある場合やサポートが必要な場合は、アドビ配信品質コンサルタントにご連絡いただくか、配信品質コンサルタントがまだいない場合はアカウントチームに配信品質コンサルタントの追加についてご相談ください。

## 回避策

これは常に問題となるものですが、実際には、これらの変更はのエンドユーザーにとって意味を持つということです。 [!DNL Google] および [!DNL Yahoo]のプラットフォーム。 彼らは、これらのルールを実施するためのユーザーの期待によって動機付けられています。 これらの変更を回避しようとするのではなく、一歩下がってこれらの変更に対応する方法を検討することをお勧めします。
