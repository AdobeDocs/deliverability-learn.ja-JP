---
title: Microsoft（Hotmail、Outlook、Windows Live など）
description: Microsoftは、通常、リストの構成に応じて2番目または3番目に大きいプロバイダーで、他のISPとは少し異なるトラフィックを処理します。
topics: Deliverability
kt: 5319
doc-type: article
activity: understand
team: TM
exl-id: d706cb90-828a-4ab3-8f93-c9bd71553d63
source-git-commit: 68c403f915287e1a50cd276b67b3f48202f45446
workflow-type: tm+mt
source-wordcount: '334'
ht-degree: 2%

---

# [!DNL Microsoft] ([!DNL Hotmail], [!DNL Outlook], [!DNL Windows Live], etc.)

[!DNL Microsoft] は、通常、リストの構成に応じて2番目または3番目に大きいプロバイダーで、他のISPとは少し異なるトラフィックを処理します。

主な特徴は次のとおりです。

## 重要なデータ

[!DNL Microsoft] フィードバックを求めてポーリングする送信者のレピュテーション、苦情数、ユーザーエンゲージメント、および信頼できるユーザーのグループ（送信者レピュテーションデータまたはSRDとも呼ばれます）に焦点を当てます。

## 利用可能なデータ

[!DNL Microsoft]の独自の送信者レポートツール( [!DNL Smart Network Data Services] SNDS)を使用すると、送信するメールの量と受け入れられるメールの量、苦情やスパムトラップに関する指標を確認できます。共有されるデータはサンプルで、正確な数値は反映されませんが、[!DNL Microsoft]が送信者としてどのように見るかを表すのが最適です。 [!DNL Microsoft] では、信頼されたユーザーグループに関する情報は公に提供されませんが、そのデータは、プログラムを通じ [!DNL Return Path Certification] て追加料金で利用できます。

## 送信者の評価

[!DNL Microsoft] は、従来、レピュテーション評価やフィルタリングの判断でIPを送信することに重点を置いてきました。また、送信ドメイン機能の拡張にも積極的に取り組んでいます。 どちらも、苦情やスパムトラップなど、従来の評判インフルエンサーによって主に動かされています。 配信品質は、特定の定量的および定性的なプログラム要件を持つReturn Path Certificationプログラムの影響を大きく受ける場合もあります。

## Insights

[!DNL Microsoft] は、すべての受信ドメインを組み合わせて、送信レピュテーションを確立し、追跡します。これには、[!DNL Hotmail]、[!DNL Outlook]、MSN、[!DNL Windows Live]などのほか、会社のOffice 365でホストされている電子メールも含まれます。 [!DNL Microsoft] は、特にボリュームの変動に敏感な場合があるので、ボリュームに基づく急激な変化を可能にするのではなく、大きな送り口から上昇および下降する特定の戦略を適用することを検討してください。

[!DNL Microsoft] は、IPウォーミングの初期日にも特に厳格です。これは、通常、ほとんどのメールが最初にフィルタリングされることを意味します。多くのISPは、有罪が証明されるまで送信者を無罪と見なします。 [!DNL Microsoft] その反対で、自分が無罪だと証明するまで、自分を有罪と考える。
