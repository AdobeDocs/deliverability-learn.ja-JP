---
title: バウンス
description: 様々なタイプのバウンスについて説明します。
topics: Deliverability
jira: KT-7047
thumbnail: kt7047.jpg
doc-type: article
activity: understand
team: ACS
exl-id: 6338eb67-3efd-476e-8b26-97bbb6a1d35f
source-git-commit: 9444f8601f2f349398ee5deb9d5f4d4f7abb44f5
workflow-type: ht
source-wordcount: '0'
ht-degree: 100%

---

# バウンス

バウンスとは、配信の試行時に ISP がエラー通知を提供して発生するエラーです。バウンス処理プロセスは、リストの衛生状態を保つ上で重要な要素です。特定の E メールが連続して複数回バウンスした場合、このプロセスが該当 E メールに抑制のフラグを付けます。抑制がトリガーされるのに必要なバウンスの回数とタイプは、システムによって異なります。このプロセスにより、システムが無効な E メールアドレスを送信し続けるのを防ぎます。バウンスは、ISP が IP の評判を決定するのに使用する主要データの 1 つです。このため、この指標を監視することは非常に重要です。「配信済み」と「バウンス済み」を比較することは、恐らくマーケティングメッセージ配信の測定で最もよく使用される手法です。配信済みの割合が高いほど、優れていることになります。

ここでは、2 つのタイプのバウンスについて見ていきます。

## ハードバウンス

ハードバウンスとは、ISP が加入者アドレスへのメール送信試行後、配信不能と判定した際に生成される永続的なエラーです。Adobe Campaign 内では、配信不能として分類されたハードバウンスは強制隔離に追加されるので、その後再度試行されることはありません。エラーの原因が不明な場合などにハードバウンスが無視されるケースもあります。ハードバウンスの一般的な例を次に示します。

* 存在しないアドレス
* 無効なアカウント
* 不正な構文
* 不正なドメイン

## ソフトバウンス

ソフトバウンスとは、メールの配信に問題が発生した場合に ISP が生成する一時的なエラーです。ソフトエラーの場合、配信を成功させるために複数回（回数は、カスタム設定またはデフォルトの配信設定を使用しているかによって異なります）再試行されます。ソフトバウンスが継続的に発生しても、そのアドレスは、再試行の最大数（これも設定に応じて異なります）に達するまで強制隔離に追加されません。ソフトバウンスの一般的な原因は次のとおりです。

* メールボックス容量超過
* 受信 E メールサーバーダウン
* 送信者の評判の問題

![バウンスのタイプ](../assets/bounce-types.png)

>[!NOTE]
>
>バウンスは、不良なデータソース（ハードバウンス）または ISP の評判問題（ソフトバウンス）を浮き彫りにしている可能性があるので、評判の問題を示す重要な指標です。
>
>ソフトバウンスは E メール送信の一環で頻繁に発生するもので、配信品質の実際問題として考える前に、再試行処理により解決するかを確かめる必要があります。ソフトバウンス率が 1 つの ISP に対して 30％を超え、24 時間以内に解決しない場合は、その件について Adobe Campaign の配信品質コンサルタントに相談することをお勧めします。

## 製品固有のリソース

**Adobe Campaign Classic**

* [配信失敗のタイプと理由](https://experienceleague.adobe.com/docs/campaign-classic/using/sending-messages/monitoring-deliveries/understanding-delivery-failures.html?lang=ja#delivery-failure-types-and-reasons)
* [バウンスメールの管理](https://experienceleague.adobe.com/docs/campaign-classic/using/sending-messages/monitoring-deliveries/understanding-delivery-failures.html?lang=ja#bounce-mail-management)
* [配信不能件数とバウンス数のレポート](https://experienceleague.adobe.com/docs/campaign-classic/using/reporting/reports-on-deliveries/global-reports.html?lang=ja#non-deliverables-and-bounces)

**Adobe Campaign Standard**

* [配信失敗のタイプと理由](https://experienceleague.adobe.com/docs/campaign-standard/using/testing-and-sending/monitoring-messages/understanding-delivery-failures.html?lang=ja#delivery-failure-types-and-reasons)
* [バウンスメールの選定](https://experienceleague.adobe.com/docs/campaign-standard/using/testing-and-sending/monitoring-messages/understanding-delivery-failures.html?lang=ja#bounce-mail-qualification)
* [バウンスの概要レポート](https://experienceleague.adobe.com/docs/campaign-standard/using/reporting/list-of-reports/bounce-summary.html?lang=ja#reporting)
