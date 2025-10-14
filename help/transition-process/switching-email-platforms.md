---
title: メールプラットフォーム切り替え時のスムーズな移行方法。
description: メールサービスプロバイダー（ESP）を移動する場合、既存の確立済み IP アドレスも移行できません。 新しく始める際には、肯定的な評判を得るためのベストプラクティスに従うことが重要です。
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
source-wordcount: '213'
ht-degree: 7%

---

# メールプラットフォームの切り替え時に移行をスムーズに行う方法

メールサービスプロバイダー（ESP）を移動する場合、既存の確立済み IP アドレスも移行できません。 新しく始める際には、肯定的な評判を得るためのベストプラクティスに従うことが重要です。 使用する新しい IP アドレスはまだ評判が立っていないので、ISP は送信されるメールを完全に信頼できないので、顧客に配信できるメールに注意する必要があります。

肯定的な評判を確立することはプロセスです。 しかし、一度設定されると、小さな負の指標は、あなたとあなたのメール配信に与える影響が少なくなります。

![&#x200B; 移行プロセス &#x200B;](../assets/transition-process.png)

IP アドレスとドメインをウォームアップする時間は場合によって異なりますが、一般的な送信者が最も多くの Tier 1 ISP （Gmail、Microsoft、Verizon/Yahoo/AOL など）で評価を確立するのに最大 8 週間のベンチマークが用いられます。

次の節では、オンボーディングを適切に行うために焦点を当てる必要がある主な領域について説明します。

1. [インフラストラクチャ](/help/transition-process/infrastructure.md)
2. [ターゲティング設定条件](/help/transition-process/targeting-criteria.md)
3. [IP ウォーミング中の ISP 別考慮事項](/help/transition-process/isp-specific-considerations-during-ip-warming.md)
4. [ボリューム](/help/transition-process/volume.md)
