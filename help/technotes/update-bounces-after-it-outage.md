---
title: Italia Online 停止後のバウンス認定条件の更新
description: Italia Online 停止後にバウンス認定条件を更新する方法を学ぶ
feature: Deliverability
exl-id: a11e88cf-bf37-42cc-9c09-1d58360459b7
hide: true
hidefromtoc: true
role: Admin
level: Beginner
source-git-commit: 6b312cdbba496818337c97ec4f42962aea757901
workflow-type: tm+mt
source-wordcount: '403'
ht-degree: 17%

---

# Italia Online 停止後の誤ったハードバウンスの更新 {#update-bounce-italia}

## コンテキスト{#outage-context}

1 月 22 日（現地時間）より、Italia Online はサービスが停止され、数件の遅延とメールの拒否が発生しています。 1 月 26 日から限定的にサービスを再開しました。

影響を受けるドメインは、**libero.it**、**virgilio.it**、**inwind.it**、**iol.it**、**blu.it** です。

この問題は 2023 年 1 月 22 日（PT）から 2023 年 1 月 26 日（PT）まで発生しましたが、誤った強制隔離のほとんどは 1 月 26 日に発生しました。

詳しくは、公式コミュニケーション [ こちら ](https://tecnologia.libero.it/avviato-il-ritorno-online-di-libero-mail-e-virgilio-mail-66832){_blank} を参照してください。


## 影響{#outage-impact}

インターネットサービスプロバイダー（ISP）が機能停止した場合によくあるように、Campaign またはJourney Optimizerを通じて送信される一部のメールは、誤ってバウンスとマークされていました。 これはAdobeに影響を与えただけでなく、サービス停止の期間中に Italia Online にメールを配信しようとしたすべてのユーザーに影響を与えました。

症状は次のとおりです。

* **ソフトバウンス** とメッセージ `452 requested action aborted: try again later` – これらは自動的に再試行され、アクションは必要ありません。

* **ハードバウンス** と、メッセージ `550 <email address> recipient rejected` が 1 月 26 日午前 8 時～午後 2 時（現地時間）に ISP によって返されました。これは、送信者がサーバーの過負荷を継続するのを防ぐためです。 Italia Online Postmaster によって確認されたように、これらは実際のハードバウンスではないので、そのメッセージにより 2023 年 1 月 26 日に除外されたすべてのメールアドレスの強制隔離を解除することをお勧めします。

## 更新処理{#outage-update}

### Adobe Campaign{#ac-update}

Adobe Campaignは、標準のバウンス処理ロジックに従って、これらの受信者を強制隔離リストに自動的に追加し、**[!UICONTROL ステータス]**&#x200B;を&#x200B;**[!UICONTROL 強制隔離]**&#x200B;に設定しました。 この問題を修正するには、Campaign の強制隔離テーブルを更新する必要があります。それには、該当する受信者を特定して削除するか、**[!UICONTROL ステータス]**&#x200B;を&#x200B;**[!UICONTROL 有効]**&#x200B;に変更して、夜間のクリーンアップワークフローで削除する必要があります。

この問題の影響を受けた受信者を見つける場合や、他の ISP で同じ状況が発生する場合は、次の手順を参照してください。

* Campaign Classic v7 および Campaign v8 については、[ このページ ](https://experienceleague.adobe.com/docs/campaign-classic/using/sending-messages/monitoring-deliveries/understanding-quarantine-management.html?lang=en#unquarantine-bulk){_blank} を参照してください。
* Campaign Standardについては、[ このページ ](https://experienceleague.adobe.com/docs/campaign-standard/using/testing-and-sending/monitoring-messages/understanding-quarantine-management.html?lang=en#unquarantine-bulk){_blank} を参照してください。

### Adobe Journey Optimizer{#ajo-update}

標準のバウンス処理ロジックに従い、Adobe Journey Optimizerは、これらのメールアドレスを **[!UICONTROL 無効な受信者**[!UICONTROL  の ]**理由]** 設定で抑制リストに自動的に追加しました。 これを修正するには、これらのメールアドレスを検索して削除し、抑制リストを更新する必要があります。

識別したら、「**[!UICONTROL 削除]**」ボタンを使用して、これらのアドレスを抑制リストから手動で削除できます。 その後、これらのアドレスは今後のメールキャンペーンに含めることができます。

詳しくは、[ この節 ](https://experienceleague.adobe.com/docs/journey-optimizer/using/configuration/monitor-reputation/manage-suppression-list.html#remove-from-suppression-list){_blank} を参照してください。

