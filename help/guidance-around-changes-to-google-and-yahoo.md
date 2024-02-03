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
source-git-commit: 50017358f7f88f5579de282a1f528916ecb17493
workflow-type: tm+mt
source-wordcount: '1775'
ht-degree: 90%

---

# [!DNL Google] と [!DNL Yahoo] で発表された変更に関するガイダンス

10月3日（PT）、[!DNL Google] と [!DNL Yahoo] の両社は共同で、ブログを通じて予定された変更を発表しました。これらの変更は、2024年2月1日（PT）以降の新しい要件として業界の一般的なベストプラクティスを適用することで、ユーザーの安全を確保し、メールエクスペリエンスを向上させるように設計されています。

[https://blog.google/products/gmail/gmail-security-authentication-spam-protection/](https://blog.google/products/gmail/gmail-security-authentication-spam-protection/){target="_blank"}

![[!DNL Google] お知らせ_](/help/assets/Gmail.png)

[https://blog.postmaster.yahooinc.com/post/730172167494483968/more-secure-less-spam](https://blog.postmaster.yahooinc.com/post/730172167494483968/more-secure-less-spam){target="_blank"}

![[!DNL Yahoo] お知らせ](/help/assets/Yahoo.png)

アドビのメール配信品質のエキスパートは、これらのブログ投稿とリンクされたドキュメントをすべて熟読しているので、お客様が読む必要はありません。重要な留意点を以下に示します。

## [!DNL Google] と [!DNL Yahoo] が行っている内容

メールの世界には、法的要件、実用的な要件、一般的なベストプラクティスがあります。法的要件は場所によって大きく異なるので、このトピックには含まれていません。代わりに、[!DNL Google] と [!DNL Yahoo] はベストプラクティスを採用し、実用的な要件に変えています。

[!DNL Google] と [!DNL Yahoo] が 2月に義務化を開始する予定の項目はどれも新しいものではなく、多くの場合、長年にわたってベストプラクティスとして推奨されてきましたが、業界内での採用は遅く、不均一でした。これは、[!DNL Google] と [!DNL Yahoo] が「お客様がユーザーにメールをデプロイする場合（これはメールリストのかなりの部分を占める可能性があり、地域や業界によっては 70％に達する場合もあります）、これらの作業を行う必要があります」と表明することで採用プロセスの進行を支援する方法です。

## 詳細内容

お客様がアドビの顧客である場合、必要なもののほとんどは既に設定の一部となっていますが、技術的にオプションである重要な項目がいくつかあり、2024年2月までに組織がこれらの項目を正しく採用および設定していることを確認する必要があります。

## DMARC：

[!DNL Google] と [!DNL Yahoo] の両社はどちらも、お客様にメールの送信に使用するドメインの DMARC レコードをリクエストします。現在、p=reject または p=quarantine 設定は必要ありません。そのため、現時点では、一般に「モニタリング」設定と呼ばれる p=none の設定が完全に許容されます。これによって、メールの処理方法が変わることはありません。DMARC を使用しない場合と同様に、通常どおりに処理されます。これを設定することは、DMARC で自分自身を保護するための最初の手順であり、[!DNL Google] や [!DNL Yahoo] へのメールの送信を支援するという新しい利点に加えて、メールエコシステム内の任意の場所に認証の問題があるかどうかを確認するのにも役立ちます。

DMARC のルールは変更されていません。つまり、DMARC を防止するように設定していない限り、親ドメイン（adobe.com など）の DMARC レコードが継承され、サブドメイン（email.adobe.com など）が対象になります。様々なビジネス上の理由で追加する必要がある場合を除き、サブドメインに異なる DMARC レコードは必要ありません。

DMARC TXT レコードの設定は、現在、Campaign と AJO のAdobeで完全にサポートされていますが、必須ではありません。 無料の DMARC チェッカーを使用して、サブドメインに DMARC が設定されているかどうかを確認します。設定されてない場合は、アドビのサポートチームにお問い合わせの上、その設定を取得するための最適な方法を確認してください。

DMARC の詳細と、Marketo Engage に対する実装方法については、[こちら](https://experienceleague.adobe.com/docs/deliverability-learn/deliverability-best-practice-guide/additional-resources/technotes/implement-dmarc.html?lang=ja){target="_blank"} for Adobe Campaign, [here](https://experienceleague.adobe.com/docs/journey-optimizer/using/reporting/deliverability/dmarc-record-update.html?lang=en){target="_blank"} for AJO, or [here](https://experienceleague.adobe.com/docs/marketo/using/getting-started-with-marketo/setup/configure-protocols-for-marketo.html?lang=ja){target="_blank"}を参照してください。

## ワンクリック（リスト）登録解除：

混乱する必要はありません。[!DNL Google] と [!DNL Yahoo] は、セキュリティボットが単にジョブを実行することで、または誤ってクリックする可能性のある、メールの本文やフッター内の登録解除リンクについては触れていません。これは、「mailto」または「http/URI」バージョンの List-Unsubscribe ヘッダー機能を意味します。 これは、ユーザーが登録解除をクリックできる [!DNL Yahoo] および Gmail UI 内の機能です。Gmail では、「スパムを報告」をクリックしたユーザーに対して、登録を解除するかどうかを確認するメッセージも表示します。これにより、受け取った苦情（お客様の評判を傷つける）を登録解除（お客様の評判を傷つけない）に変えることで、苦情の件数を減らすことができます。

注意すべき点は [!DNL Google] および [!DNL Yahoo] はどちらも、「1-Click」という名前の「http/URI」オプションを指しているので、意図的なものです。 技術的には、元の「http/URI」オプションを使用して、受信者を Web サイトにリダイレクトできます。 これは、[!DNL Yahoo] と [!DNL Google] の焦点ではありません。両社は更新された [RFC8058](https://datatracker.ietf.org/doc/html/rfc8058){target="_blank"} を参照しています。この RFC8058 は、web サイトではなく HTTPS POST リクエストを介して登録解除を処理し、「ワンクリック」にすることにフォーカスしています。

現在、Gmail では「mailto」list-unsubscribe オプションを使用できます。Gmail では、「mailto」は今後の期待に応えられないため、送信者は「投稿」list-unsubscribe オプションを有効にする必要があるとの見解を示しています。既に何らかのタイプの list-unsubscribe を設定している送信者は、2024年6月1日（PT）までに「ワンクリック」list-unsubscribe を設定する必要があります。

[!DNL Yahoo] では、現時点では「mailto」オプションを引き続き使用するものの、今後は「投稿」オプションも必要になると述べています。

アドビでは、「mailto」と「投稿／ワンクリック」list-unsubscribe オプションの両方を使用することをお勧めします。アドビは、これらの要件を満たすユーザーをサポートするために、すべてのメール送信プラットフォームで「投稿」サポートを有効にすることに取り組んでいます。詳しくは、以下を参照してください。

list-unsubscribe ヘッダーの必要性は、トランザクションメールには適用されません。トリガーされたメッセージ（放棄された買い物かごなど）や、サブスクライバーによって生成されない類似の通信は、[!DNL Google] や [!DNL Yahoo] などのメールボックスプロバイダーによってマーケティングと見なされ、list-unsubscribe が必要になることに注意してください。

[!DNL Google] と [!DNL Yahoo] は両社とも、受信者が登録解除し、後日再登録する場合があることを認識しています。両社とも、これらの状況をどのように識別するかという秘密のソースを共有するつもりはありませんが、このような場合に送信者に誤ってペナルティを課すことを回避する方法に取り組んでいます。

>[!INFO]
> アドビは、これらの要件を満たすユーザーをサポートするために、すべてのメール送信プラットフォームで「投稿」サポートを有効にすることに取り組んでいます。
> 
> 
> * [!DNL Adobe Campaign Classic V7/V8]：完全にサポートPOST1 — クリック今日、手順が見つかります [ここ](https://experienceleague.adobe.com/docs/deliverability-learn/deliverability-best-practice-guide/additional-resources/campaign/acc-technical-recommendations.html?lang=ja#list-unsubscribe){target="_blank"}.
>* [!DNL Adobe Campaign Standard]:2 月下旬までにPOST1 回のクリックをサポートするように更新中です。 設定手順が提供されます [ここ](https://experienceleague.adobe.com/docs/experience-cloud-kcs/kbarticles/KA-14778.html?lang=ja){target="_blank"} 準備が整いました。
>* [!DNL Adobe Journey Optimizer]：今日のPOST1 回のクリックをサポートしますが、主な改善が進行中で、2024 年 3 月に実施される予定です。 ドキュメントの更新が公開されます [ここ](https://experienceleague.adobe.com/docs/journey-optimizer/using/email/email-opt-out.html?lang=ja){target="_blank"} 準備が整いました。
> * [!DNL Marketo]:2024 年 1 月 31 日現在、POST1-Click-List-Unsubscribe が完全にサポートされています。 ユーザーに必要なアクションはありません。


## 2 日以内での登録解除プロセス：

これは、しばらくの間推奨されるベストプラクティスでした。登録解除したユーザーにメールをデプロイすると、通常、スパムの苦情が発生するので、そのユーザーへのメールの送信を早く停止するほど良いでしょう。ここでも、法的要件は場合によっては非常に多くなることがありますが、ユーザーが List-Unsubscribe 経由で登録解除したことと、3 日目になってもユーザーにメールが送信されている場合、[!DNL Google] と [!DNL Yahoo] はそれらの事実を把握し、そのような行為を行う送信者には、今後いかなるユーザーに対するメール送信も継続を許可しないと表明しています。

この 2 日間の要件は、様々な list-unsubscribe メソッドによるすべての登録解除に適用されます。場合によっては（「mailto」など）、アドビが処理することを意味します。アドビでは、すべての登録解除リクエストを受信後、2 日の制限内で直ちに処理します。場合によっては、お客様が処理する可能性があります。お客様がこれらのリクエストを処理している場合は、この 2 日間のタイムラインに合わせるために、お客様側で変更を行う必要がある場合があります。

## 苦情率：

苦情率を 0.2％未満に抑えることが、長い間ベストプラクティスとして行われてきました。[!DNL Google] は長期間にわたって基準を 0.3％と高めに設定していますが、0.1％未満に抑えることにはメリットがあると明確に述べています。共有した詳細を以下に示します。

* スパム率を 0.10％未満に抑えるようにします。
* 特に継続的にスパム率が 0.30％以上になることは避けます。
* スパム率を低く維持すると、時折急増するユーザーフィードバックに対する送信者の回復力が高まります。
* 同様に、スパム率を高く維持すると、スパムの分類が増加します。スパム率の改善がスパムの分類に積極的に反映されるまでには時間がかかる場合があります。

[!DNL Yahoo] は、苦情のしきい値も 0.30％の範囲内になると述べています。

[!DNL Google] と [!DNL Yahoo] の目標は、たった 1 日の悪い日や苦情の一時的急増を引き起こす 1 つの誤りによって送信者を処罰することではありません。代わりに、長期間にわたって苦情率が高い送信者や、不適切な送信動作のパターンに焦点を当てています。

苦情率の監視や、苦情を減らすための戦略にサポートが必要な場合は、アドビ配信品質コンサルタントにご相談いただくか、配信品質コンサルタントがまだいない場合はアカウントチームに配信品質コンサルタントの追加についてご相談ください。

## 確認しているタイムライン

10 月の初回発表以降、タイムラインの更新が行われています。最新のタイムラインは次のようになります。

[!DNL Gmail]：

2024年2月 - コンプライアンス違反の警告を提供するために設計された、一時的なバウンスが開始されます。お客様がまだ準拠していない場合、メールは少し遅れてから通常どおり配信されます。完全に準拠している場合、一時的なバウンスは発生せず、お客様には何の影響もありません。

2024年4月 - ワンクリックリスト登録解除を除くすべてに準拠していない送信者に対して、ブロックが開始されます。最初は準拠していないメールの一部のみがブロックされ、時間の経過と共にブロック対象の割合が増加します。

2024年6月1日（PT）- ワンクリックリスト登録解除など、完全に準拠していない送信者はブロックされます。

[!DNL Yahoo]：

2024 年 2 月 — 1-Click List-Unsubscribe 以外のすべての要件に対する実施の段階的な展開は、2024 年 2 月に開始されます。

2024 年 6 月 — 1-Click List-Unsubscribe の実施は 2024 年 6 月に開始されます。

## マーケターに与える影響

Gmail と [!DNL Yahoo] のこれらの新しい要件に従わない場合、メールがスパムフォルダーに分類されるか、ブロックされることが予想されます（つまり、メールが配信されなかったことを示す MBP のバウンスが返されます）。

したがって、アドビでは、上記で概要を示した変更を実施し、できるだけ早く準拠し始めることを強くお勧めします。また、[!DNL Yahoo] と [!DNL Google] でのパフォーマンスのベンチマークを開始し、2月に向けて指標に重大な変更があるかどうかを確認するのに最適な時期でもあります。

ご質問がある場合やサポートが必要な場合は、アドビ配信品質コンサルタントにご連絡いただくか、配信品質コンサルタントがまだいない場合はアカウントチームに配信品質コンサルタントの追加についてご相談ください。

## 回避策

これは常に浮上する質問ですが、実際には、これらの変更は [!DNL Google] と [!DNL Yahoo] のプラットフォームのエンドユーザーにとって意味があります。これらのルールを適用するというユーザーの期待が動機となっています。これらの変更を回避しようとするのではなく、一歩下がってこれらの変更に対応する方法を検討することをお勧めします。

## 最終メモ：

現時点では、これは、[!DNL Yahoo].JP または [!DNL Gmail] Workspace アカウントに送信されるメールには適用されませんが、これらの場所から送信されるメールには適用されます。

## その他のリソース（これらの変更に固有ではありません）：

[Google Sender のガイドライン](https://support.google.com/mail/answer/81126){target="_blank"}

[Google FAQ](https://support.google.com/a/answer/14229414?sjid=2864589551334481470-NC){target="_blank"}

[Yahoo Sender のガイドライン](https://senders.yahooinc.com/best-practices/){target="_blank"}

[Yahoo FAQ](https://senders.yahooinc.com/faqs/){target="_blank"}
