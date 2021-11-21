---
title: Microsoft（Hotmail、Outlook、Windows Live など）
description: Microsoftは、通常、リストの構成に応じて 2 番目または 3 番目に大きいプロバイダーで、他の ISP とは少し異なるトラフィックを処理します。
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

[!DNL Microsoft] は、通常、リストの構成に応じて 2 番目または 3 番目に大きいプロバイダーで、他の ISP とは少し異なるトラフィックを処理します。

主な特徴を次に示します。

## 重要なデータ

[!DNL Microsoft] フィードバックを求めて投票する、送信者のレピュテーション、苦情、ユーザーエンゲージメント、および信頼できるユーザーのグループ（送信者レピュテーションデータまたは SRD とも呼ばれます）に焦点を当てます。

## 使用可能にするデータ

[!DNL Microsoft]の独自の送信者レポートツール [!DNL Smart Network Data Services] (SNDS) を使用すると、送信するメールの量と受け入れられるメールの量、苦情やスパムトラップに関する指標を確認できます。 共有されるデータはサンプルで、正確な数値は反映されませんが、方法を表すのが最適な方法であることに注意してください [!DNL Microsoft] 自分を送信者として表示します。 [!DNL Microsoft] では、信頼されたユーザーグループに関する情報は公開されていませんが、そのデータは [!DNL Return Path Certification] 追加料金のプログラム。

## 送信者の評価

[!DNL Microsoft] は、従来、レピュテーション評価での IP の送信とフィルタリングの決定に焦点を当ててきました。 また、送信ドメイン機能の拡張にも積極的に取り組んでいます。 どちらも、苦情やスパムトラップなど、従来の評判の影響者に主導されています。 また、配信品質は、特定の定量的および定性的なプログラム要件を持つ Return Path Certification プログラムの大きな影響を受ける場合があります。

## Insights

[!DNL Microsoft] は、すべての受信ドメインを組み合わせて、送信レピュテーションを確立し、追跡します。 これには以下が含まれます。 [!DNL Hotmail], [!DNL Outlook], MSN, [!DNL Windows Live]などを実行し、会社の Office 365 でホストされる電子メールも送信します。 [!DNL Microsoft] は、ボリュームの変動に特に影響を受けやすいので、ボリュームに基づく急激な変更を可能にするのではなく、大きな送り口からランプアップ/ダウンする特定の戦略を適用することを検討してください。

[!DNL Microsoft] また、は IP ウォーミングの初期の日には特に厳格です。これは、通常、ほとんどのメールが最初にフィルタリングされることを意味します。 多くの ISP は、有罪と判断されるまで送信者を無罪と見なします。 [!DNL Microsoft] その反対で、自分が無実であると証明するまで、自分を有罪と考える。
