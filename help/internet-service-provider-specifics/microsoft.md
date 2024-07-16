---
title: Microsoft（Hotmail、Outlook、Windows Live など）
description: Microsoftは通常、リストの構成に応じて 2 番目または 3 番目に大きなプロバイダーであり、他の ISP とは少し異なるトラフィックを処理します。
topics: Deliverability
jira: KT-5319
doc-type: article
activity: understand
role: Admin, Leader, User
level: Beginner
team: TM
exl-id: d706cb90-828a-4ab3-8f93-c9bd71553d63
source-git-commit: 6b312cdbba496818337c97ec4f42962aea757901
workflow-type: tm+mt
source-wordcount: '335'
ht-degree: 2%

---

# [!DNL Microsoft] （[!DNL Hotmail]、[!DNL Outlook]、[!DNL Windows Live] など）

[!DNL Microsoft] は通常、リストの構成に応じて 2 番目または 3 番目に大きなプロバイダーであり、他の ISP とは少し異なるトラフィックを処理します。

ハイライトを次に示します。

## 重要なデータ

[!DNL Microsoft] は、送信者のレピュテーション、苦情、ユーザーエンゲージメント、フィードバックをポーリングする信頼できるユーザーグループ（送信者レピュテーションデータまたは SRD とも呼ばれます）に焦点を当てています。

## 使用可能にするデータ

[!DNL Microsoft] 独自の送信者レポートツールである [!DNL Smart Network Data Services] （SNDS）を使用すると、送信するメールの量と受け入れられるメールの量に関する指標のほか、苦情やスパムトラップを確認できます。 共有されるデータはサンプルであり、正確な数値を反映しているわけではありませんが、送信者としての [!DNL Microsoft] の考え方を表すのに最適です。 [!DNL Microsoft] は、信頼できるユーザーグループに関する情報を公開していませんが、そのデータは [!DNL Return Path Certification] プログラムを通じて追加料金で利用できます。

## 送信者の評価

[!DNL Microsoft] は従来、評判の評価とフィルタリングの決定で IP の送信に重点を置いていました。 また、送信ドメイン機能の拡張にも積極的に取り組んでいます。 どちらも、苦情やスパムトラップなど、従来の評判の影響力者によって主に推進されています。 配信品質は、特定の定量的および定性的プログラム要件を持つリターンパス認定プログラムの影響も大きく受ける可能性があります。

## Insights

[!DNL Microsoft] は、すべての受信ドメインを組み合わせて、送信レピュテーションを確立および追跡します。 これには、[!DNL Hotmail]、[!DNL Outlook]、MSN、[!DNL Windows Live] などが含まれるほか、企業の Office 365 でホストされているメールも含まれます。 [!DNL Microsoft] はボリュームの変動に特に影響を受けやすいので、ボリュームベースの急激な変化を許可するのではなく、大規模な送信から上下にランプアップする特定の戦略を適用することを検討してください。

[!DNL Microsoft] た、IP ウォーミングの初期の期間には特に厳しくなります。つまり、ほとんどのメールが最初にフィルタリングされます。 ほとんどの ISP は、有罪と証明されるまで、送信者を無罪と見なします。 [!DNL Microsoft] れは反対であり、あなた自身が無罪を証明するまで、あなたを有罪と見なします。
