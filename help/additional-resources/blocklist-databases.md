---
title: リアルタイムブラックホールリスト
description: スパマーが使用する可能性の高いIPアドレスとドメインのリストを管理する組織について説明します。
feature: Additional resources
topics: Deliverability
kt: null
thumbnail: null
doc-type: article
activity: understand
team: ACS
translation-type: tm+mt
source-git-commit: 96ed84da391faaabd3001ddd6a411ddc1f46b033
workflow-type: tm+mt
source-wordcount: '409'
ht-degree: 90%

---


# リアルタイムブラックホールリスト

いくつかの組織では、スパム送信者に使用されていると考えられている IP アドレスおよびドメインのデータベースを維持管理しています。これらのサイトを参考にすると、特定のメッセージがスパムとして拒否された理由を理解するのに役立ちます。通常、これらのリストに誤って登録されたアドレスの削除を申請することは可能です。

これらのデータベースは RBL（リアルタイムブラックホールリスト）と呼ばれ、DNS メカニズムを通じて参照されます。次の 3 種類の RBL があります。

* IP アドレス別：スパムを送信しているかスパムを中継している可能性の高い IP アドレスをリストアップします。
* 送信者ドメイン別：スパムを送信しているか誤って設定された送信者ドメイン（バウンスメールアドレスのフルドメイン）をリストアップします。
* Web ドメイン別：スパムコンテンツに含まれているリンクや画像の URL にあるドメイン（登録機関に登録されている高レベルのドメイン）をリストアップします。Adobeソリューションでは、一般的に、考慮されるドメインは、追跡に使用されるアドレスです。

次に、最も広く使用されている RBL のリストを示します。詳細なリストについては、[https://www.dnsstuff.com/](https://tools.dnsstuff.com/) を参照してください。

* **Spamhaus**

   [https://www.spamhaus.org/](https://www.spamhaus.org/) を参照してください。

   データベースのほうが重要です。このリストで分類されているのは、一般に深刻な状況です。このような状況が発生した場合は、ただちに対応し、商用サービス、配信品質サービスおよび[アドビカスタマーケア](https://helpx.adobe.com/jp/enterprise/admin-guide.html/enterprise/using/support-for-experience-cloud.ug.html)に警告を出す必要があります。

* **SpamCop**

   [https://www.spamcop.net/](https://www.spamcop.net/) を参照してください。

   最も有名なデータベースの 1 つです。お使いの IP アドレスのいずれかがこのリストに載っている場合は、一般に、送信したメッセージが SpamCop ユーザーによりスパムであると宣言されたか、SpamCop ハニーポットにメッセージを送信したことがあるという意味です。

* **URIBL**

   [https://www.uribl.com/](https://www.uribl.com/) を参照してください。

   このリストでは、スパムとして宣言されたメッセージで定期的に見られるドメインを特定しています。お使いのドメインがこのリストに載った場合は、配信品質に重大な影響が及ぶおそれがあります。配信品質サービスと[アドビカスタマーケア](https://helpx.adobe.com/enterprise/admin-guide.html/enterprise/using/support-for-experience-cloud.ug.html)にただちに知らせる必要があります。

* **SURBL**

   [http://www.surbl.org/](http://www.surbl.org/) を参照してください。

   SURBL では、スパムで定期的に見られる Web サイトを特定しています。お使いのドメインがこのリストに載った場合は、配信品質に重大な影響が及ぶおそれがあります。配信品質サービスと[アドビカスタマーケア](https://helpx.adobe.com/enterprise/admin-guide.html/enterprise/using/support-for-experience-cloud.ug.html)にただちに知らせてください。

* **iX Manitu**

   IP アドレスのリストで、ドイツで広く使用されています。[https://www.heise.de/ix/nixspam/](https://www.heise.de/ix/nixspam/) を参照してください。

<!--* SORBS

  [https://www.nl.sorbs.net](https://www.nl.sorbs.net) compiles a list of IP addresses that are reputed to be dynamic IP address (i.e. attributed temporarily to ISP subscribers) or "open relay" addresses. Certain domains check whether the IP address of a sender is not listed on this site before accepting email. Checking the IP addresses on this site can prove useful.-->
