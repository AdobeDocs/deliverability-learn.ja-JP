---
title: Italia Online の停止後にバウンスの選定を更新
description: Italia Online の停止後にバウンスの選定を更新する方法を説明します。
feature: Deliverability
exl-id: a11e88cf-bf37-42cc-9c09-1d58360459b7
hide: true
hidefromtoc: true
source-git-commit: 016d7f9da67193d893e762fbe6e191cf87d5b030
workflow-type: tm+mt
source-wordcount: '423'
ht-degree: 15%

---

# Italia Online の停止後に誤ったハードバウンスを更新する {#update-bounce-italia}

## コンテキスト{#outage-context}

1 月 22 日（現地時間）より、Italia Online は停止状態に陥り、いくつかの遅延が発生し、E メールが拒否されました。 サービスは、1 月 26 日に限られた容量で再開し始めました。

影響を受けるドメインは次のとおりです。 **libero.it**, **virgiio.it**, **inwind.it**, **iol.it**、および **blu.it**.

この問題は1/22/2023 ～ 1/26/2023で発生しましたが、誤って強制隔離されたのほとんどは 1 月 26 日に発生しました。

詳細は公式のコミュニケーションを参照 [ここ](https://tecnologia.libero.it/avviato-il-ritorno-online-di-libero-mail-e-virgilio-mail-66832){_blank}.


## 影響{#outage-impact}

ISP の機能停止が発生した場合のほとんどと同様に、Campaign を通じて送信された一部の E メールは誤ってバウンスとしてマークされていました。 これはAdobeに影響を与えるだけでなく、停止中に Italia Online にメールを配信しようとしたすべての人々に影響を与えました。

症状は次の通りです。

* **遅延バウンス** メッセージと共に `452 requested action aborted: try again later`  — これらは自動的に再試行されたので、アクションは必要ありません。

* **ハードバウンス** メッセージと共に `550 <email address> recipient rejected` は、送信者がサーバーの過負荷を防ぐため、1 月 26 日（現地時間の午前 8 時～午後 2 時）に ISP から返されました。 Italia Online Postmaster によって確認されたように、これらは実際のハードバウンスではないので、2023 年 1 月 26 日 (PT) に除外されたすべての E メールアドレスの強制隔離を解除することをお勧めします。

## 更新処理{#outage-update}

### Adobe Campaign{#ac-update}

Adobe Campaignは、標準のバウンス処理ロジックに従って、これらの受信者を強制隔離リストに自動的に追加し、**[!UICONTROL ステータス]**&#x200B;を&#x200B;**[!UICONTROL 強制隔離]**&#x200B;に設定しました。 この問題を修正するには、Campaign の強制隔離テーブルを更新する必要があります。それには、該当する受信者を特定して削除するか、**[!UICONTROL ステータス]**&#x200B;を&#x200B;**[!UICONTROL 有効]**&#x200B;に変更して、夜間のクリーンアップワークフローで削除する必要があります。

この問題の影響を受けた受信者を見つける、または他の ISP で問題が再び発生した場合は、以下の手順を参照してください。

* Campaign Classicv7 および Campaign v8 については、 [このページ](https://experienceleague.adobe.com/docs/campaign-classic/using/sending-messages/monitoring-deliveries/understanding-quarantine-management.html?lang=en#unquarantine-bulk){_blank}.
* Campaign Standardについては、 [このページ](https://experienceleague.adobe.com/docs/campaign-standard/using/testing-and-sending/monitoring-messages/understanding-quarantine-management.html?lang=en#unquarantine-bulk){_blank}.

### Adobe Journey Optimizer{#ajo-update}

標準のバウンス処理ロジックに従い、Adobe Journey Optimizerは、これらの電子メールアドレスを **[!UICONTROL 理由]** 設定 **[!UICONTROL 無効な受信者]**. これを修正するには、これらの電子メールアドレスを見つけて削除し、抑制リストを更新する必要があります。

特定されたアドレスは、 **[!UICONTROL 削除]** 」ボタンをクリックします。 その後、これらのアドレスを今後の E メールキャンペーンに含めることができます。

詳しくは、 [この節](https://experienceleague.adobe.com/docs/journey-optimizer/using/configuration/monitor-reputation/manage-suppression-list.html#remove-from-suppression-list){_blank}.

