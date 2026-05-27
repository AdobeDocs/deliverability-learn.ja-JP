---
title: スパムトラップ
description: 様々な種類のスパムトラップについて説明します。
topics: Deliverability
jira: KT-7050
thumbnail: kt7050.jpg
doc-type: article
activity: understand
team: ACS
exl-id: ffacc1b1-bf3f-466e-9a1d-63aad4d2ec45
TQID: https://experienceleague.adobe.com/qandgsfuAA4E9uHfZ0jrgpkjs-kt9Izs8k-HvtgDF7A
product_v2: id: b27e5950-9033-45ac-9f86-eb22e567f615id: d0a3eab4-7b10-4d96-a71e-6c0f8e7b7c87id: dfc56824-e8b9-499e-85d4-21aedb507314
feature_v2: id: a075b2c1-7748-4328-b7f6-343aa314616aid: b0bb9048-d951-48d8-8232-45cf248a7e27id: e64968b2-4ee5-47f9-8cae-0588f184b9ebid: f71e690b-4480-4b67-9ef5-88f42f9cdfdb
role_v2: id: b69b2659-1057-424e-8fc5-ed9e016dc554id: f8a45b24-4be7-4f1b-909b-60d06b483a20
level_v2: id: e8ccd51f-da0d-4e3b-939b-e30d5ebb1ea5
topic_v2: id: beb7a3c1-66ab-4786-b879-7621375b3c40
source-git-commit: 75df8537199680e5f1fc4b98cefdb05220fee7bf
workflow-type: tm+mt
source-wordcount: 495
ht-degree: 100%

---

# スパムトラップ

スパムトラップは、不正な送信者やメールのベストプラクティスに従っていない送信者からのメールを識別するために利用されます。 スパムトラップのメールアドレスは、通常一般公開されないので、ほぼ特定不可能です。 スパムトラップにメールを配信すると、送信者の評判に対し、トラップの種類や ISP に応じて多様な程度の影響を及ぼします。 以下の節で、異なる種類のスパムトラップについて詳しく説明します。

## 再利用

再利用型のスパムトラップは、以前は有効だったが今では使用されなくなったアドレスです。 リストをできる限りクリーンに保つための主な方法の 1 つは、定期的にリスト全体にメールを送信し、バウンスするメールを適切に抑制することです。 これにより、破棄されたメールアドレスを強制隔離し、それ以降の使用を停止できます。

場合によっては、アドレスが 30 日以内に再利用されることもあります。 定期的な送信をおこない、非アクティブユーザーを抑制することは、リストの衛生状態を保つうえで重要な点です。 **再エンゲージメントキャンペーン**&#x200B;は通常、高度なメールマーケティングプログラムの一部です。 このキャンペーンスタイルでは、送信者は、メール送信対象ではなくなったユーザーを取り戻すための試行が可能です。

## タイプミス

タイプミス型のスパムトラップは、誤字または変形を含むアドレスです。 これは多くの場合、Gmail など主要ドメインの既知の誤ったつづりで発生します（例：gmial はよくあるタイプミスです）。 ISP やその他のブロックリスト運営者は、スパムトラップとして使用するために既知の不正ドメインを登録し、スパマーの識別、送信者の健全性の測定をおこないます。 タイプミス型のスパムトラップを回避する最善の方法は、リスト収集に&#x200B;**ダブルオプトインプロセス**&#x200B;を使用することです。

## 未使用

未使用型のスパムトラップは、現在も過去にもエンドユーザーがいないアドレスです。 これは、スパムメールを識別する目的のみに作成されたアドレスです。 これは、最も影響力が大きい種類のスパムトラップです。実質的に特定は不可能で、リストから除去するには相当な努力を必要とします。 ほとんどのブロックリストは、未使用型のスパムトラップを利用して信用できない送信者をリストに追加します。 未使用型スパムトラップが広範なマーケティングメールリストに侵入するのを防ぐ唯一の方法は、リスト収集時に&#x200B;**ダブルオプトインプロセス**&#x200B;を利用することです。

## その他のリソース

* [このセクション](/help/additional-resources/all-about-spam-traps.md)では、スパムトラップの特定と回避の詳細について説明します。
* [このセクション](/help/additional-resources/re-engagement.md)では、再エンゲージメント戦略を通じて配信品質を向上させる方法の詳細について説明します。

## 製品固有のリソース

**Adobe Campaign Classic**

* [SpamAssassin](https://experienceleague.adobe.com/docs/campaign-classic/using/sending-messages/deliverability-management/spamassassin.html?lang=ja#using-spamassassin)
* [ダブルオプトインを備えた購読フォームの作成](https://experienceleague.adobe.com/docs/campaign-classic/using/designing-content/web-forms/use-cases--web-forms.html?lang=ja#create-a-subscription--form-with-double-opt-in)

**Adobe Campaign Standard**

* [メールおよびスパム対策分析のプレビュー](https://experienceleague.adobe.com/docs/campaign-standard-learn/tutorials/designing-content/email-designer/preview-your-email.html?lang=ja#designing-content)
* [ダブルオプトインプロセス](https://experienceleague.adobe.com/docs/campaign-standard/using/communication-channels/landing-pages/setting-up-a-double-opt-in-process.html?lang=ja#communication-channels)
