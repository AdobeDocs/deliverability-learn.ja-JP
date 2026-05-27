---
title: リアルタイムブラックホールリスト
description: 迷惑メール送信者が使用する可能性の高いIP アドレスとドメインのリストを管理する組織について説明します。
topics: Deliverability
doc-type: article
activity: understand
team: ACS
exl-id: 4155b89f-a636-404c-8951-563c1b4d0289
TQID: https://experienceleague.adobe.com/dsyoiAT3fYro3L8HkRT6OuXGfBqaVOJNy-IoFXQK37I
product_v2: id: b27e5950-9033-45ac-9f86-eb22e567f615id: d0a3eab4-7b10-4d96-a71e-6c0f8e7b7c87id: dfc56824-e8b9-499e-85d4-21aedb507314
feature_v2: id: c5f60233-d5ea-4453-a799-0ad258b4d399id: f71e690b-4480-4b67-9ef5-88f42f9cdfdb
role_v2: id: b69b2659-1057-424e-8fc5-ed9e016dc554id: f8a45b24-4be7-4f1b-909b-60d06b483a20
level_v2: id: e8ccd51f-da0d-4e3b-939b-e30d5ebb1ea5
topic_v2: id: c1579802-ddd4-4214-8a91-97b2066abe11
source-git-commit: 75df8537199680e5f1fc4b98cefdb05220fee7bf
workflow-type: tm+mt
source-wordcount: 423
ht-degree: 91%

---

# リアルタイムブラックホールリスト

いくつかの組織では、スパム送信者に使用されていると考えられている IP アドレスおよびドメインのデータベースを維持管理しています。 これらのサイトを参考にすると、特定のメッセージがスパムとして拒否された理由を理解するのに役立ちます。 通常、これらのリストに誤って登録されたアドレスの削除を申請することは可能です。

これらのデータベースは RBL（リアルタイムブラックホールリスト）と呼ばれ、DNS メカニズムを通じて参照されます。 次の 3 種類の RBL があります。

* IP アドレス別：スパムを送信しているかスパムを中継している可能性の高い IP アドレスをリストアップします。
* 送信者ドメイン別：スパムを送信しているか誤って設定された送信者ドメイン（バウンスメールアドレスのフルドメイン）をリストアップします。
* Web ドメイン別：スパムコンテンツに含まれているリンクや画像の URL にあるドメイン（登録機関に登録されている高レベルのドメイン）をリストアップします。 Adobe ソリューションでは、考慮されるドメインは、一般的にトラッキングに使用されるアドレスです。

次に、最も広く使用されている RBL のリストを示します。 詳細なリストについては、[https://www.dnsstuff.com/](https://tools.dnsstuff.com/) を参照してください。

* **Spamhaus**

  [https://www.spamhaus.org/](https://www.spamhaus.org/) を参照してください。

  データベースのほうが重要です。 このリストで分類されているのは、一般に深刻な状況です。 このような状況が発生した場合は、ただちに対応し、商用サービス、配信品質サービスおよび[アドビカスタマーケア](https://helpx.adobe.com/jp/enterprise/admin-guide.html/enterprise/using/support-for-experience-cloud.ug.html)に警告を出す必要があります。

* **SpamCop**

  [https://www.spamcop.net/](https://www.spamcop.net/) を参照してください。

  最も有名なデータベースの 1 つです。 お使いの IP アドレスのいずれかがこのリストに載っている場合は、一般に、送信したメッセージが SpamCop ユーザーによりスパムであると宣言されたか、SpamCop ハニーポットにメッセージを送信したことがあるという意味です。

* **URIBL**

  [https://www.uribl.com/](https://www.uribl.com/) を参照してください。

  このリストでは、スパムとして宣言されたメッセージで定期的に見られるドメインを特定しています。 お使いのドメインがこのリストに載った場合は、配信品質に重大な影響が及ぶおそれがあります。 配信品質サービスと[アドビカスタマーケア](https://helpx.adobe.com/jp/enterprise/admin-guide.html/enterprise/using/support-for-experience-cloud.ug.html)にただちに知らせる必要があります。

* **SURBL**

  [https://surbl.org/](https://surbl.org/)を参照してください

  SURBL では、スパムで定期的に見られる Web サイトを特定しています。 お使いのドメインがこのリストに載った場合は、配信品質に重大な影響が及ぶおそれがあります。 配信品質サービスと[アドビカスタマーケア](https://helpx.adobe.com/jp/enterprise/admin-guide.html/enterprise/using/support-for-experience-cloud.ug.html)にただちに知らせる必要があります。

* **iX Manitu**

  IP アドレスのリストで、ドイツで広く使用されています。 [https://www.heise.de/ix/nixspam/](https://www.heise.de/ix/nixspam/) を参照してください。

<!--
* SORBS

  [https://www.nl.sorbs.net](https://www.nl.sorbs.net) compiles a list of IP addresses that are reputed to be dynamic IP address (i.e. attributed temporarily to ISP subscribers) or "open relay" addresses. Certain domains check whether the IP address of a sender is not listed on this site before accepting email. Checking the IP addresses on this site can prove useful.
-->
