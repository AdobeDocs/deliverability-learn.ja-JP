---
title: 苦情
description: ユーザーが、不要または予期しないメールであることを指摘した場合に登録される、苦情について説明します。
topics: Deliverability
jira: KT-7048
thumbnail: kt7048.jpg
doc-type: article
activity: understand
team: ACS
exl-id: 0343820d-f5af-4b8a-bcab-dbb47ae7aecb
source-git-commit: 9444f8601f2f349398ee5deb9d5f4d4f7abb44f5
workflow-type: tm+mt
source-wordcount: '276'
ht-degree: 100%

---

# 苦情

苦情は、不要または予期しないメールであることをユーザーが指摘した場合に登録されます。通常、購読者によるこのアクションは、購読者がメールクライアントのスパムボタンを押した際またはサードパーティのスパムレポートシステムを介して記録されます。

## ISP 苦情

オプトアウトや登録解除のプロセスがメールアドレスの検証目的で悪用された経緯があるので、大半の Tier 1 および一部の Tier 2 ISP は、ユーザーにスパム報告の手段を提供しています。Adobe Campaign は、ISP FBL を介してこれらの苦情を受け取ります。これは、FBL を提供する ISP のセットアッププロセス中に確立され、Adobe Campaign は、苦情を報告したメールアドレスを自動的に強制隔離テーブル追加して抑制することができます。ISP 苦情が急増した場合は、リスト品質の低さ、最適でないリスト収集方法、エンゲージメントポリシーの脆弱さなどを示している可能性があります。また、コンテンツが関連しない場合にも、苦情が多くなることがあります。

## サードパーティ苦情

より広範囲のレベルでのスパム報告を可能にするスパム対策グループもいくつかあります。これらのサードパーティが使用する苦情指標は、スパムメールを識別するためメール内容をタグ付けするのに利用されます。この処理は「フィンガープリント」とも呼ばれます。こうしたサードパーティ苦情申し立ての手段を使用するユーザーは、一般的にメールに関して精通しており、こうした苦情に対応しないでいると、他の苦情に比べて大きな影響がある場合があります。

>[!NOTE]
>
>ISP は、苦情を収集し、それらを使用して送信者の全体的な評判を判断します。すべての苦情については、現地の法令に従ってできるだけ迅速に抑制し、メール送信を停止する必要があります。

## 製品固有のリソース

**Adobe Campaign Classic**

* [トラッキング指標](https://experienceleague.adobe.com/docs/campaign-classic/using/reporting/reports-on-deliveries/delivery-reports.html?lang=ja#tracking-indicators)

**Adobe Campaign Standard**

* [苦情レポート](https://experienceleague.adobe.com/docs/campaign-standard/using/reporting/list-of-reports/complaints.html?lang=ja#reporting)
