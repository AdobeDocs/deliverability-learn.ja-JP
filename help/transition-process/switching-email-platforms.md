---
title: メールプラットフォームを切り替える際にスムーズに移行する方法。
description: メールサービスプロバイダー（ESP）を移行する場合、既存のIP アドレスを移行することはできません。 新しいメールマーケティングを始める際には、肯定的なレピュテーションを得るためのベストプラクティスに従うことが重要です。
topics: Deliverability
jira: KT-5259
thumbnail: kt5259.jpg
doc-type: article
activity: understand
role: Admin
level: Beginner
team: ACS
exl-id: 5444d576-5bc1-4fa6-9956-c63dc3c60440
TQID: https://experienceleague.adobe.com/sxCdMHKqdCZ3z2xp-aMYKiFfqu5Y-iDhk8FeergrgZw
product_v2: id: b27e5950-9033-45ac-9f86-eb22e567f615id: d0a3eab4-7b10-4d96-a71e-6c0f8e7b7c87id: dfc56824-e8b9-499e-85d4-21aedb507314
feature_v2: id: b0bb9048-d951-48d8-8232-45cf248a7e27
role_v2: id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
level_v2: id: e8ccd51f-da0d-4e3b-939b-e30d5ebb1ea5
source-git-commit: 75df8537199680e5f1fc4b98cefdb05220fee7bf
workflow-type: tm+mt
source-wordcount: 215
ht-degree: 8%

---

# メールプラットフォームの切り替え時に移行をスムーズに行う方法

メールサービスプロバイダー（ESP）を移行する場合、既存のIP アドレスを移行することはできません。 新しいメールマーケティングを始める際には、肯定的なレピュテーションを得るためのベストプラクティスに従うことが重要です。 新しいIP アドレスにはまだレピュテーションがないので、ISPはそのIP アドレスから送信されるメールを完全に信頼できず、顧客へのメール配信に慎重な姿勢を示す必要があります。

肯定的なレピュテーションを確立するには、ある程度時間を要します。 しかし、一度確立すれば、多少マイナス要素があったとしても、あなたやメール配信への影響を低減できます。

![移行プロセス ](../assets/transition-process.png)

IP アドレスとドメインをウォームする時間は異なる場合がありますが、一般的な送信者は、多くのTier 1 ISP （Gmail、Microsoft、Verizon/Yahoo/AOLなど）でレピュテーションを確立するために、最大8週間のベンチマークを設定するのが一般的です。

以降のセクションでは、オンボーディングを適切に行うために重点的に取り組むべき主な領域について説明します。

1. [インフラストラクチャ](/help/transition-process/infrastructure.md)
2. [ターゲティング設定条件](/help/transition-process/targeting-criteria.md)
3. [IP ウォーミング中の ISP 別考慮事項](/help/transition-process/isp-specific-considerations-during-ip-warming.md)
4. [ボリューム](/help/transition-process/volume.md)
