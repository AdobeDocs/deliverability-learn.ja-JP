---
title: バウンス
description: 様々なタイプのバウンスについて説明します。
feature: 指標
topics: Deliverability
kt: 7047
thumbnail: kt7047.jpg
doc-type: article
activity: understand
team: ACS
translation-type: tm+mt
source-git-commit: d42a8c3b06308fca0cf3e9db8d634a767fc0cdc6
workflow-type: tm+mt
source-wordcount: '449'
ht-degree: 3%

---


# バウンス

バウンスとは、配信の試行と失敗の結果です。ISPは、エラー通知を返します。 バウンス処理は、リストの衛生上重要な部分です。 特定の電子メールが連続して複数回送信された後、この処理は抑制のフラグを付けます。 トリガーの抑制に必要なバウンスの数とタイプは、システムによって異なります。 このプロセスにより、システムが無効な電子メールアドレスを送信し続けるのを防ぎます。 バウンスは、IPの評判を判断する際にISPが使用するデータの主要部分の1つです。 この指標を注意深く見ておくことは非常に重要です。 「配信済み」と「バウンス済み」は、おそらくマーケティングメッセージの配信を測定する最も一般的な方法です。配信率が高いほど、高い方が良い。

2種類のバウンスを調べます

## ハードバウンス

ハードバウンスとは、ISPが加入者アドレスへのメーリング試行を配信不能と判定した後に生成される永続的なエラーです。 Adobe Campaign内では、配信不能として分類されたハードバウンスが強制隔離に追加され、再試行されません。 エラーの原因が不明な場合にハードバウンスが無視される場合があります。
ハードバウンスの一般的な例を次に示します。

* アドレスが存在しません
* 無効なアカウント
* 構文が正しくありません
* 不正なドメイン

## ソフトバウンス

ソフトバウンスとは、ISPがメールの配信に問題を抱えた場合に発生する一時的な障害です。 ソフトエラーは、配信を成功させるために複数回(カスタム設定または既製の配信設定の使用によって異なります)再試行されます。 強制隔離の最大数が試行されるまで（設定に応じて再び異なります）、ソフトバウンスが継続して再試行に追加されません。 ソフトバウンスの一般的な原因は次のとおりです。

* メールボックス容量超過
* 電子メールサーバーのダウン受信
* 送信者の評判の問題

![直帰タイプ](../assets/bounce-types.png)

>[!NOTE]
>
>バウンスは、不良データソース（ハードバウンス）やISP（ソフトバウンス）での評判の問題を強調する可能性があるので、評判の問題を示す重要な指標です。
>
>ソフトバウンスは電子メールの送信の一部として頻繁に発生し、実際の配信品質の問題として特徴付ける前に、再試行処理中に解決できる必要があります。 ソフトバウンス率が1つのISPに対して30%を超え、24時間以内に解決しない場合は、Adobe Campaignの配信品質コンサルタントに懸念を抱かせることをお勧めします。

## 製品固有のリソース

**Adobe Campaign Standard**

* [レポートのリスト — バウンスの概要（製品ドキュメント）](https://experienceleague.adobe.com/docs/campaign-standard/using/reporting/list-of-reports/bounce-summary.html?lang=en#reporting)
* [配信エラーについて（製品ドキュメント）](https://experienceleague.adobe.com/docs/campaign-standard/using/testing-and-sending/monitoring-messages/understanding-delivery-failures.html?lang=en#about-delivery-failures)

**Adobe Campaign Classic**

* [配信エラーについて（製品ドキュメント）](https://experienceleague.adobe.com/docs/campaign-classic/using/sending-messages/monitoring-deliveries/understanding-delivery-failures.html?lang=en#sending-messages)