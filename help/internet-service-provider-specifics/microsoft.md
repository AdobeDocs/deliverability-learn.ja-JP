---
title: Microsoft（Hotmail、Outlook、Windows Live など）
description: Microsoftは2番目または3番目（リストの構成によって異なります）に大きなプロバイダーであり、他のISPとは少し異なるトラフィックを処理します。
topics: Deliverability
jira: KT-5319
doc-type: article
activity: understand
role: Admin, Leader, User
level: Beginner
team: TM
exl-id: d706cb90-828a-4ab3-8f93-c9bd71553d63
TQID: https://experienceleague.adobe.com/pbp5vbHUIHSL9zL9gQf4LpIhEYZI1umEesy3czbJx-4
product_v2: id: b27e5950-9033-45ac-9f86-eb22e567f615id: d0a3eab4-7b10-4d96-a71e-6c0f8e7b7c87id: dfc56824-e8b9-499e-85d4-21aedb507314
feature_v2: id: ea90ebee-5c84-42d9-8b21-006bdabc95a3
role_v2: id: b69b2659-1057-424e-8fc5-ed9e016dc554id: c66ffd68-0f65-42bb-aa23-b4020f12e0bdid: f8a45b24-4be7-4f1b-909b-60d06b483a20
level_v2: id: e8ccd51f-da0d-4e3b-939b-e30d5ebb1ea5
topic_v2: id: aa2f3246-cb95-4b30-8899-fdf7d73550ccid: e1e0219c-f879-479f-8427-888ed2a6e9c2
source-git-commit: 75df8537199680e5f1fc4b98cefdb05220fee7bf
workflow-type: tm+mt
source-wordcount: 335
ht-degree: 2%

---

# [!DNL Microsoft] （[!DNL Hotmail]、[!DNL Outlook]、[!DNL Windows Live]など）

[!DNL Microsoft]は、通常、リストの構成によって2番目または3番目に大きなプロバイダーであり、他のISPとは少し異なるトラフィックを処理します。

主な特徴：

## 重要なデータ

[!DNL Microsoft]は、送信者のレピュテーション、苦情、ユーザーのエンゲージメントに焦点を当てます。また、フィードバックを求める対象となる、信頼できるユーザーのグループ（送信者レピュテーションデータ（SRD）とも呼ばれます）にも注目します。

## マーケターはチャネルをまたいで

[!DNL Microsoft]独自の送信者レポートツール [!DNL Smart Network Data Services] （SNDS）を使用すると、送信するメールの量と受け取られるメールの量に関する指標のほか、苦情やスパムトラップを確認できます。 共有されるデータはサンプルであり、正確な数値を反映しているわけではありませんが、[!DNL Microsoft]が送信者をどのように判別しているかがよくわかります。 [!DNL Microsoft]は、信頼できるユーザーグループに関する情報を公開していませんが、そのデータは[!DNL Return Path Certification] プログラムを通じて追加料金で利用できます。

## 送信者の評価

[!DNL Microsoft]は従来、レピュテーションの評価とフィルタリングの決定において、送信元IPに重点を置いていました。 また、送信元ドメイン機能の拡張にも積極的に取り組んでいます。 どちらも、苦情やスパムトラップなどの、従来のレピュテーションの影響要因が中心になっています。 配信品質はReturn Path Certification プログラムの影響も大きく受ける可能性があります。このプログラムには特定の定量的および定性的プログラム要件があります。

## Insights

[!DNL Microsoft]は、すべての受信ドメインを組み合わせて、送信レピュテーションを確立および追跡します。 これには、[!DNL Hotmail]、[!DNL Outlook]、MSN、[!DNL Windows Live]などが含まれます。また、企業のOffice 365でホストされているメールも含まれます。 [!DNL Microsoft]はボリュームの変動の影響を特に受けやすいので、ボリュームベースの急激な変化を許可するのではなく、大規模な送信から上下に変動させる特定の戦略を適用することを検討してください。

また、[!DNL Microsoft]はIP ウォーミングの初期の期間には特に厳しい条件を満たします。これは、ほとんどのメールが最初にフィルタリングされることを意味します。 ほとんどのISPは、送信者が有害であることが証明されるまで、無害であるものとみなします。 [!DNL Microsoft]は反対で、自分が無害であることを証明するまで、あなたを有害と見なします。
