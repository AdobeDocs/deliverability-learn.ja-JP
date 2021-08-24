---
title: 電子メールプラットフォーム切り替え時のスムーズな移行方法.
description: '電子メールサービスプロバイダー(ESP)を移動する場合、既存の確立されたIPアドレスを移行することもできません。 新たに開始する際に、肯定的なレピュテーションを開発するためのベストプラクティスに従うことが重要です。 '
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

電子メールサービスプロバイダー(ESP)を移動する場合、既存の確立されたIPアドレスを移行することもできません。 新たに開始する際に、肯定的なレピュテーションを開発するためのベストプラクティスに従うことが重要です。 使用する新しいIPアドレスにはまだレピュテーションがないので、ISPはメールを完全に信頼できず、顧客に配信できる内容に注意する必要があります。

肯定的な評判を確立することは、プロセスです。 しかし、設定後は、小さなマイナス指標は、あなたやメール配信に与える影響を少なくします。

![移行プロセス](../assets/transition-process.png)

IPアドレスとドメインをウォームアップする時間は異なる場合がありますが、一般的な送信者は、最大8週間のベンチマークまでが、最大で第1層のISP（Gmail、Microsoft、Verizon/Yahoo/AOLなど）での評判を確立するのに一般的です。

次の節では、適切にオンボーディングするために焦点を当てるいくつかの主要な領域を調査します。

1. [インフラストラクチャ](/help/transition-process/infrastructure.md)
2. [ターゲティング設定条件](/help/transition-process/targeting-criteria.md)
3. [IP ウォーミング中の ISP 別考慮事項](/help/transition-process/isp-specific-considerations-during-ip-warming.md)
4. [ボリューム](/help/transition-process/volume.md)
