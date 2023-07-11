---
title: メールプラットフォームの切り替え時に移行をスムーズに行う方法.
description: 電子メールサービスプロバイダー (ESP) を移動する場合、既存の確立された IP アドレスを移行することもできません。 新たに開始する際に、肯定的な評判を開発するためのベストプラクティスに従うことが重要です。
topics: Deliverability
jira: KT-5259
thumbnail: kt5259.jpg
doc-type: article
activity: understand
role: Admin
level: Beginner
team: ACS
exl-id: 5444d576-5bc1-4fa6-9956-c63dc3c60440
source-git-commit: 6b312cdbba496818337c97ec4f42962aea757901
workflow-type: tm+mt
source-wordcount: '212'
ht-degree: 11%

---

# メールプラットフォームの切り替え時に移行をスムーズに行う方法

電子メールサービスプロバイダー (ESP) を移動する場合、既存の確立された IP アドレスを移行することもできません。 新たに開始する際に、肯定的な評判を開発するためのベストプラクティスに従うことが重要です。 使用する新しい IP アドレスにはまだレピュテーションがないので、ISP はメールを完全に信頼できず、顧客に配信できる内容に注意する必要があります。

肯定的な評判を確立することは、プロセスです。 しかし、設定後、小さな否定的な指標は、あなたやメール配信に対する影響を少なくします。

![移行プロセス](../assets/transition-process.png)

IP アドレスとドメインをウォームアップする時間は異なる場合がありますが、一般的な送信者は、最大 8 週間のベンチマークで、ほとんどの第 1 層 ISP(Gmail、Microsoft、Verizon/Yahoo/AOL など ) でレピュテーションを確立するのが一般的です。

次の節では、適切にオンボーディングするために焦点を当てるべき重要な領域をいくつか調査します。

1. [インフラストラクチャ](/help/transition-process/infrastructure.md)
2. [ターゲティング設定条件](/help/transition-process/targeting-criteria.md)
3. [IP ウォーミング中の ISP 別考慮事項](/help/transition-process/isp-specific-considerations-during-ip-warming.md)
4. [ボリューム](/help/transition-process/volume.md)
