---
title: 苦情
description: 'ユーザーが電子メールが不要または予期しないものであると示した場合に登録される苦情について説明します。 '
feature: 指標
topics: Deliverability
kt: 7048
thumbnail: kt7048.jpg
doc-type: article
activity: understand
team: ACS
translation-type: tm+mt
source-git-commit: 550821608eb7049f739a156536dd31b6b2faa2fa
workflow-type: tm+mt
source-wordcount: '291'
ht-degree: 3%

---


# 苦情

苦情は、電子メールが不要または予期しないものであるとユーザが示した場合に登録されます。 通常、この購読アクションは、購読者がスパムボタンを押したとき、またはサードパーティのスパムレポートシステムを介して、購読者の電子メールクライアントを通じて記録されます。

## ISPに関する苦情

Tier 1とTier 2 ISPのほとんどは、過去に電子メールアドレスの検証に悪意を持って使用されたプロセスのオプトアウトや登録解除が行われたので、スパムレポート方式をユーザーに提供しています。 Adobe Campaignは、ISP FBLを介してこれらの苦情を受け取ります。 これは、FBLを提供するISPのセットアッププロセス中に確立され、Adobe Campaignは、強制隔離テーブルに対して不満を示した電子メールアドレスを自動的に追加して抑制できます。 ISPに関する苦情の急増は、リストの質の低さ、最適でないリスト収集方法、弱い関与ポリシーを示す可能性があります。 また、コンテンツに関連がない場合にもよく知られます。

## サードパーティからの苦情

より広いレベルでスパムレポートを可能にする複数のスパム対策グループがあります。 これらのサードパーティが使用する苦情指標は、電子メールの内容にタグを付けてスパム電子メールを識別するために使用されます。 この処理は「フィンガープリント」とも呼ばれます。 これらのサードパーティの苦情申し立て方のユーザは、一般的に電子メールに関する保護を受けているので、未回答のままにした場合に他の苦情よりも大きな影響を与えることができます。

>[!NOTE]
>
>ISPは、不満を収集し、それらを使用して送信者の全体的な評判を判断します。 すべての苦情は抑えられ、できるだけ早く、現地の法令に従って連絡を取らなくてはならない。

## 製品固有のリソース

**Adobe Campaign Classic**

* [トラッキング指標](https://experienceleague.adobe.com/docs/campaign-classic/using/reporting/reports-on-deliveries/delivery-reports.html#tracking-indicators)

**Adobe Campaign Standard**

* [苦情報告](https://experienceleague.adobe.com/docs/campaign-standard/using/reporting/list-of-reports/complaints.html#reporting)