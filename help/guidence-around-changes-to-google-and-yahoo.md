---
title: 発表された変更に関するガイダンス： [!DNL Google] および [!DNL Yahoo]
description: 発表された変更に関するガイダンス： [!DNL Google] および [!DNL Yahoo]
role: Admin
level: Experienced
doc-type: Article
last-substantial-update: 2023-11-06T00:00:00Z
jira: KT-14320
thumbnail: KT-14320.jpeg
source-git-commit: 00b4b4c3396fc4a71484cd12e8c89cd8371ad1ce
workflow-type: tm+mt
source-wordcount: '1297'
ht-degree: 0%

---


# 発表された変更に関するガイダンス： [!DNL Google] および [!DNL Yahoo]

10 月 3 日、両方 [!DNL Google] および [!DNL Yahoo] 共同で発表した予定変更は、ブログを通じて行われた。 これらの変更は、2024 年 2 月以降の新しい要件として、一般的な業界のベストプラクティスを適用することで、ユーザーの安全を確保し、E メールエクスペリエンスを向上させるように設計されました。

[https://blog.google/products/gmail/gmail-security-authentication-spam-protection/](https://blog.google/products/gmail/gmail-security-authentication-spam-protection/){target="_blank"}

![[!DNL Google] お知らせ](/help/assets/Gmail.png)

[https://blog.postmaster.yahooinc.com/post/730172167494483968/more-secure-less-spam](https://blog.postmaster.yahooinc.com/post/730172167494483968/more-secure-less-spam){target="_blank"}

![[!DNL Yahoo] お知らせ](/help/assets/Yahoo.png)

Adobeの E メール配信品質の専門家は、必要ないように、これらのブログ投稿とリンクされたドキュメントをすべて読み上げています。 重要な留意点を次に示します。

## では、具体的には何なのでしょうか [!DNL Google] および [!DNL Yahoo] やってる？

電子メールの世界には、法的要件、実用的な要件、一般的なベストプラクティスがあります。 法的要件は場所によって大きく異なり、このトピックには含まれていません。 代わりに、 [!DNL Google] および [!DNL Yahoo] ベストプラクティスを実践し、実践的な要件に変えている 項目が見つかりません [!DNL Google] および [!DNL Yahoo] 2 月には新しい要件が必要となり、何年もの間、ベストプラクティスの推奨事項となっていますが、業界では採用が遅く、不均等です。 これは [!DNL Google] および [!DNL Yahoo]は、「E メールをユーザーにデプロイする場合（地域や業界によっては 70%もの高さになる場合があります）、これらの作業をおこなう必要があります」と、採用プロセスの進展を支援する方法です。

## 詳細は？

Adobeのお客様の場合は、既に設定に含まれていますが、技術的にはオプションの重要な項目がいくつかあり、2024 年 2 月より前に組織でこれらの項目が適切に採用され、設定されていることを確認する必要があります。

## DMARC:

[!DNL Google] および [!DNL Yahoo] 両方とも、電子メールを送信するために使用するドメインの DMARC レコードを持っている必要があります。 現在、p=reject または p=quarantine の設定は必要ないので、p=none（一般的に「監視」設定と呼ばれる）の設定は、完全に受け入れ可能です。 これにより、E メールの処理方法が変わることはありません。E メールは、DMARC を使用せずに通常どおりに処理されます。 これは DMARC で自分自身を保護する最初のステップであり、メールの送信を支援する新しいメリットに加えて、 [!DNL Google] および [!DNL Yahoo] また、e メールエコシステム内のどこでも認証の問題が発生しているかどうかを確認するのに役立ちます。
DMARC は現在、Adobeで完全にサポートされていますが、必須ではありません。 任意の無料の DMARC チェッカーを使用して、サブドメインに対して DMARC が設定されているかどうかを確認し、設定されていない場合は、Adobeサポートチームに問い合わせて、設定の取得方法の最善を確認します。 また、DMARC の詳細と実装方法についても確認できます [ここ](https://experienceleague.adobe.com/docs/deliverability-learn/deliverability-best-practice-guide/additional-resources/technotes/implement-dmarc.html?lang=ja){target="_blank"} for Adobe Campaign and Adobe Journey Optimizer Adobe or [here](https://experienceleague.adobe.com/docs/marketo/using/getting-started-with-marketo/setup/configure-protocols-for-marketo.html){target="_blank"} Marketo Engage。

## 1 — クリック（リスト）配信停止：

パニックに陥るな。 [!DNL Google] および [!DNL Yahoo] は、電子メールの本文またはフッター内の配信停止リンクについて話しているわけではありません。このリンクは、セキュリティボットがジョブを実行した場合や偶然にクリックされた場合にクリックされる可能性があります。 これは、「mailto」または「http/URL」バージョンの List-Unsubscribe ヘッダー機能を意味します。 これは、 [!DNL Yahoo] および Gmail UI を使用して、ユーザーが購読解除をクリックできるようにします。 Gmail は、「スパムを報告」をクリックして登録解除を行うかをユーザーに尋ねるメッセージも表示します。これにより、送信する苦情の数を減らす（苦情は評判を傷つける）ことができます（評判を損ないません）。
注意すべき点は [!DNL Google] および [!DNL Yahoo] はどちらも、「1-Click」という名前の「http/URL」オプションを参照しているので、意図的なものです。 技術的には、元の「http/URL」オプションを使用して、受信者を Web サイトにリダイレクトできます。 それは～の焦点ではない [!DNL Yahoo] および [!DNL Google]この 2 人は、更新された RFC8058 を参照し、Web サイトの代わりに HTTPSPOSTリクエストを使用して配信停止を処理し、「1-Click」にすることに重点を置いています。
Marketo Engageの場合、Adobeは既に「mailto」オプションを有効にしており、現在「http/URL」オプションをサポートしていません。 今後の更新。
Adobe CampaignとAdobe Journey OptimizerのAdobeでは、「mailto」と「1-Click」の両方のオプションを使用することをお勧めします。
list-unsubscribe の実装方法の詳細については、こちらでAdobe Campaign Classic、こちらでAdobe Campaign Standard、こちらでAdobe Journey Optimizerを確認するか、いつでもAdobeカスタマーサポートチームにお問い合わせください。
list-unsubscribe ヘッダーの必要性は、トランザクション E メールには適用されません。 「放棄された買い物かご」などのトリガーされたメッセージや、購読者が生成しなかった類似の通信は、 [!DNL Google] および [!DNL Yahoo] リスト配信停止が必要になります。

## 配信停止を 2 日以内に処理：

配信停止済みのユーザーにデプロイする電子メールは通常スパムの苦情を報告するので、電子メールの送信を中止するのが早ければ早いほど、これはしばらくの間推奨されるベストプラクティスでした。 法的要件が大幅に長くなる場合もありますが、 [!DNL Google] および [!DNL Yahoo] は、ユーザーが List-Unsubscribe を使用して購読解除し、Day 3 にもまだメールを送信していることを知っており、このメールを送信した送信者が引き続きどのユーザーにもメールを送信することを許可しないと述べています。
この 2 日間の要件は、様々な list-unsubscribe メソッドを使用して登録解除する場合に必要です。 場合によっては（「mailto」のように）、Adobeがそれらを処理することを意味します。 Adobeは、リクエストを受け取るとすぐに、2 日の制限内で、すべての配信停止リクエストを処理します。 その他の場合は、処理している可能性があります。 これらのリクエストを処理する場合、この 2 日間のタイムラインに合わせて自分の側で変更を加える必要が生じる場合があります。

## 苦情率：

0.2%未満の低い苦情率を維持することは、長い間ベストプラクティスとなってきました。 [!DNL Google] は、長期的にバーを 0.3%に高く設定していますが、0.1%未満に保つ利点があることは明らかです。 次に、共有した詳細を示します。
* スパム率を 0.10%未満に抑えるようにします。
* スパム率が 0.30%以上の場合は、特に何らかの持続期間に対して避けてください。
* スパム率を低く保つと、送信者は、ユーザーのフィードバックが頻繁に発生するスパイクに対してより柔軟に対処できます。
* 同様に、高いスパム率を維持すると、スパムの分類が増加します。 スパムの分類に積極的に反映するには、スパム率の改善に時間がかかる場合があります。
  [!DNL Yahoo] は、苦情数のしきい値も 0.30%の範囲にあると述べています。
苦情率の監視に関するサポートが必要な場合や、苦情数を減らす戦略に役立つ場合は、Adobeの配信品質コンサルタントにお問い合わせいただくか、まだ配信品質コンサルタントをお持ちでない場合はアカウントチームにお問い合わせください。

## これはマーケターとしての影響を与えますか？

Gmail のこれらの新しい要件に従わないことと [!DNL Yahoo] は、e メールがスパムフォルダーにランディングしたり、ブロックされたりする（つまり、e メールが配信されなかったことを示すバウンスを MBP から取得する）ことが予想されます。
したがって、Adobeでは、上記の変更を確認し、できるだけ早く変更に準拠することを強くお勧めします。 今は、次の場所でパフォーマンスのベンチマークを開始する絶好の機会です： [!DNL Yahoo] および [!DNL Google] 指標に重要な変更があるかどうかを確認するには、2 月を訪問します。
お問い合わせはこちらです。ご不明な点やサポートが必要な場合は、担当のAdobe配信品質コンサルタントにお問い合わせいただくか、まだ配信品質コンサルタントをお持ちでない場合はアカウントチームにお問い合わせください。

## この周りに道はありますか？

これは常に問題となるものですが、実際には、これらの変更はのエンドユーザーにとって意味を持つということです。 [!DNL Google] および [!DNL Yahoo]のプラットフォーム。 彼らは、これらのルールを実施するためのユーザーの期待によって動機付けられています。 これらの変更を回避することはお勧めしませんが、変更に対応する方法について考え直すことをお勧めします。
