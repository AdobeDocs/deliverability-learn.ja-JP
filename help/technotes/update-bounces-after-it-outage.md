---
title: Italia Onlineの停止後にバウンスの選定を更新
description: Italia Onlineの停止後にバウンスの選定を更新する方法について説明します
feature: Deliverability
exl-id: a11e88cf-bf37-42cc-9c09-1d58360459b7
hide: true
role: Admin
level: Beginner
TQID: https://experienceleague.adobe.com/hPHB9s3PH7E9L3omZMTWZA2ZB0d1JS5vEfawQOjnBLw
product_v2:
  - id: b27e5950-9033-45ac-9f86-eb22e567f615
  - id: d0a3eab4-7b10-4d96-a71e-6c0f8e7b7c87
  - id: dfc56824-e8b9-499e-85d4-21aedb507314
feature_v2:
  - id: a075b2c1-7748-4328-b7f6-343aa314616a
  - id: b3b8a63f-51fc-40f6-a7d2-a31c5d49fb45
  - id: f71e690b-4480-4b67-9ef5-88f42f9cdfdb
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
level_v2:
  - id: e8ccd51f-da0d-4e3b-939b-e30d5ebb1ea5
source-git-commit: 75df8537199680e5f1fc4b98cefdb05220fee7bf
workflow-type: tm+mt
source-wordcount: 467
ht-degree: 16%

---

# Italia Online 停止後の誤ったハードバウンスの更新 {#update-bounce-italia}

## コンテキスト{#outage-context}

1月22日（現地時間）以降、Italia Onlineは停止し、メールが何度か遅延して拒否されました。 サービスは1月26日に限られた容量で再開されました。

影響を受けるドメイン：**libero.it**、**virgilio.it**、**inwind.it**、**iol.it**、および&#x200B;**blu.it**。

この問題は2023年1月22日から2023年1月26日に発生しましたが、不正な隔離のほとんどは1月26日に発生しました。

詳しくは、公式コミュニケーション [こちら](https://tecnologia.libero.it/avviato-il-ritorno-online-di-libero-mail-e-virgilio-mail-66832){_blank}をご覧ください。


## 影響{#outage-impact}

インターネットサービスプロバイダー（ISP）の停止が発生した場合のほとんどと同様に、CampaignまたはJourney Optimizerを通じて送信された電子メールの中には、誤ってバウンスとマークされたものもあります。 これはAdobeに影響を与えただけでなく、停電中にItalia Onlineにメールを配信しようとしていたすべての人に影響を与えました。

症状は：

* メッセージ `452 requested action aborted: try again later`の&#x200B;**ソフトバウンス** – これらは自動的に再試行され、アクションは必要ありません。

* メッセージ `550 <email address> recipient rejected`を含む&#x200B;**ハードバウンス**&#x200B;は、送信者がサーバーの過負荷を維持できないように、現地時間の午前8時から午後2時の間の1月26日にISPによって返されました。 Italia Online Postmasterが確認したように、これらは実際のハードバウンスではないので、そのメッセージのために2023年1月26日に除外されたすべてのメールアドレスを強制隔離を解除することをお勧めします。

## 更新処理{#outage-update}

### Adobe Campaign{#ac-update}

Adobe Campaignは、標準のバウンス処理ロジックに従って、これらの受信者を強制隔離リストに自動的に追加し、**[!UICONTROL ステータス]**&#x200B;を&#x200B;**[!UICONTROL 強制隔離]**&#x200B;に設定しました。 この問題を修正するには、Campaign の強制隔離テーブルを更新する必要があります。それには、該当する受信者を特定して削除するか、**[!UICONTROL ステータス]**&#x200B;を&#x200B;**[!UICONTROL 有効]**&#x200B;に変更して、夜間のクリーンアップワークフローで削除する必要があります。

この問題の影響を受けた受信者を見つけるか、他のISPで再度発生する場合は、次の手順を参照してください。

* Campaign Classic v7およびCampaign v8については、[このページ &#x200B;](https://experienceleague.adobe.com/docs/campaign-classic/using/sending-messages/monitoring-deliveries/understanding-quarantine-management.html?lang=en#unquarantine-bulk){_blank}を参照してください。
* Campaign Standardについては、[このページ &#x200B;](https://experienceleague.adobe.com/docs/campaign-standard/using/testing-and-sending/monitoring-messages/understanding-quarantine-management.html?lang=en#unquarantine-bulk){_blank}を参照してください。

### Adobe Journey Optimizer{#ajo-update}

標準的なバウンス処理ロジックごとに、Adobe Journey Optimizerはこれらのメールアドレスを抑制リストに自動的に追加し、**[!UICONTROL 理由]**&#x200B;設定は&#x200B;**[!UICONTROL 無効な受信者]**&#x200B;です。 これを修正するには、これらのメールアドレスを見つけて削除することで、抑制リストを更新する必要があります。

識別されると、これらのアドレスは、**[!UICONTROL 削除]** ボタンを使用して、抑制リストから手動で削除できます。 これらのアドレスは、今後のメールキャンペーンに含めることができます。

詳しくは、[この節](https://experienceleague.adobe.com/docs/journey-optimizer/using/configuration/monitor-reputation/manage-suppression-list.html#remove-from-suppression-list){_blank}を参照してください。

