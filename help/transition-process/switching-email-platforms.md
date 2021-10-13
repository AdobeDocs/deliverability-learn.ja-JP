---
title: 電子メールプラットフォーム切り替え時のスムーズな移行方法.
description: 'When moving email service providers (ESPs), it’s not possible to also transition your existing, established IP addresses. 新しく始める際に、肯定的な評判を高めるためのベストプラクティスに従うことが重要です。 '
topics: Deliverability
kt: 5259
thumbnail: kt5259.jpg
doc-type: article
activity: understand
team: ACS
exl-id: 5444d576-5bc1-4fa6-9956-c63dc3c60440
source-git-commit: 68c403f915287e1a50cd276b67b3f48202f45446
workflow-type: tm+mt
source-wordcount: '212'
ht-degree: 11%

---

# 電子メールプラットフォーム切り替え時のスムーズな移行方法

電子メールサービスプロバイダー (ESP) を移動する場合、既存の確立された IP アドレスを移行することもできません。 It is important that you follow best practices for developing a positive reputation when starting afresh. 使用する新しい IP アドレスはまだレピュテーションを持っていないので、ISP はメールを完全に信頼できず、顧客に配信できる内容に注意する必要があります。

肯定的な評判を確立することはプロセスです。 しかし、設定後は、小さなマイナス指標は、お客様やメール配信に与える影響を少なくします。

![移行プロセス](../assets/transition-process.png)

IP アドレスとドメインをウォームアップする時間は異なる場合がありますが、一般的な送信者は、最大 8 週間のベンチマークを使用して、最大で Tier 1 ISP(Gmail、Microsoft、Verizon/Yahoo/AOL など ) での評判を確立するのが一般的です。

次の節では、適切にオンボーディングするために重点を置くいくつかの主要な領域を調べます。

1. [インフラストラクチャ](/help/transition-process/infrastructure.md)
2. [ターゲティング設定条件](/help/transition-process/targeting-criteria.md)
3. [IP ウォーミング中の ISP 別考慮事項](/help/transition-process/isp-specific-considerations-during-ip-warming.md)
4. [ボリューム](/help/transition-process/volume.md)
