---
title: 電子メールプラットフォームをスムーズにトランジションする方法。
description: '電子メールサービスプロバイダー(ESP)を移動する場合、既存の確立済みIPアドレスにトランジションを設定することもできません。 新たに開始する際に、肯定的な評価を開発するためのベストプラクティスに従うことが重要です。 '
feature: 配信品質
topics: Deliverability
kt: 5259
thumbnail: kt5259.jpg
doc-type: article
activity: understand
team: ACS
translation-type: tm+mt
source-git-commit: d42a8c3b06308fca0cf3e9db8d634a767fc0cdc6
workflow-type: tm+mt
source-wordcount: '213'
ht-degree: 0%

---


# 電子メールプラットフォームをスムーズにトランジションする方法。

電子メールサービスプロバイダー(ESP)を移動する場合、既存の確立済みIPアドレスにトランジションを設定することもできません。 新たに開始する際に、肯定的な評価を開発するためのベストプラクティスに従うことが重要です。 使用する新しいIPアドレスは評価を受けていないため、ISPはメールの送信を完全に信頼できず、顧客への配信を許可する内容には注意が必要です。

肯定的な評価を確立することは、プロセスです。 ただし、この機能が確立されると、小さな否定的な指標がユーザーやメール配信に与える影響は小さくなります。

![トランジション過程](../assets/transition-process.png)

IPアドレスとドメインを暖める時間は異なる場合がありますが、一般的な送信者は、最大8週間のベンチマークまでが、最大で第1層のISP（Gmail、Microsoft、Verizon/Yahoo/AOLなど）での評価を確立するのに一般的です。

次の節では、適切に搭載するための重要な領域を調べます。

1. [インフラ](/help/transition-process/infrastructure.md)
2. [ターゲット条件](/help/transition-process/targeting-criteria.md)
3. [IP暖機中のISP固有の考慮事項](/help/transition-process/isp-specific-considerations-during-ip-warming.md)
4. [ボリューム](/help/transition-process/volume.md)
