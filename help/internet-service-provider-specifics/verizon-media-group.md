---
title: Verizon Media Group（Yahoo、AOL、Verizon など）
description: '[!DNL Verizon Media Group]は、ほとんどのB2C リストの上位3つのドメインの1つです。 レピュテーションの問題が発生した場合、通常はメールのスロットリングやバルク処理を行うので、他社とはやや違う対応になります。'
topics: Deliverability
jira: KT-5320
doc-type: article
activity: understand
role: Admin, Leader, User
level: Beginner
team: TM
exl-id: 43e6d3cb-23c3-4076-8026-a1a08e76bd1b
TQID: https://experienceleague.adobe.com/ycELLXdqC1E3EIxywp-I1HWnSyWayRHcwkNOzmzSBvY
product_v2:
  - id: b27e5950-9033-45ac-9f86-eb22e567f615
  - id: d0a3eab4-7b10-4d96-a71e-6c0f8e7b7c87
  - id: dfc56824-e8b9-499e-85d4-21aedb507314
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
  - id: f8a45b24-4be7-4f1b-909b-60d06b483a20
level_v2:
  - id: e8ccd51f-da0d-4e3b-939b-e30d5ebb1ea5
topic_v2:
  - id: e1e0219c-f879-479f-8427-888ed2a6e9c2
source-git-commit: 75df8537199680e5f1fc4b98cefdb05220fee7bf
workflow-type: tm+mt
source-wordcount: 289
ht-degree: 3%

---

# [!DNL Verizon Media Group] （Yahoo、AOL、Verizonなど）

[!DNL Verizon Media Group]は、ほとんどのB2C リストの上位3つのドメインの1つです。 レピュテーションの問題が発生した場合、通常はメールのスロットリングやバルク処理を行うので、他社とはやや違う対応になります。

主な特徴：

## 重要なデータ

[!DNL Verizon Media Group] （VMG）は、コンテンツとURL フィルタリングおよび迷惑メールの苦情を組み合わせて使用する、独自の迷惑メールフィルターを構築し、維持しています。 Gmailと同様、IP アドレスだけでなくドメインごとにメールをフィルタリングするISPを早くから採用している企業のひとつです。

## マーケターはチャネルをまたいで

VMGには、苦情に関する情報を送信者にフィードバックするために使用されるFBLがあります。 また、将来的にデータを追加することも検討しています。

## 送信者の評価

送信者のレピュテーションは、IP アドレス、ドメイン、送信元アドレスの組み合わせで構成されます。 レピュテーションは、苦情、スパムトラップ、非アクティブまたは不正なアドレス、エンゲージメントなど、従来のコンポーネントを使用して計算されます。 VMGでは、迷惑メールから保護するために、レート制限（スロットリングとも呼ばれます）とバルクフォルダーを使用します。 PBL、SBL、XBLなどの[!DNL Spamhaus]個のブラックリストを使用して、内部フィルタリングシステムを補完し、ユーザーを保護します。

## Insights

VMGには、最近、古くて非アクティブなメールアドレスの定期的なメンテナンス期間があります。 そのため、無効なアドレスバウンスの大幅な増加が確認されることが一般的になり、これが到達率に短期間影響を与える可能性があります。 また、送信者からの無効なアドレスバウンスの割合が高いと影響を受けやすいため、取得ポリシーまたはエンゲージメントポリシーを強化する必要があります。 送信者は、多くの場合、無効なアドレスの約1%に否定的な影響を及ぼします。
