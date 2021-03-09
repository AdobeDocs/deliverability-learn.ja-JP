---
title: スパムトラップ
description: 様々な種類のスパムトラップについて説明します。
feature: 指標
topics: Deliverability
kt: 7050
thumbnail: kt7050.jpg
doc-type: article
activity: understand
team: ACS
translation-type: tm+mt
source-git-commit: d42a8c3b06308fca0cf3e9db8d634a767fc0cdc6
workflow-type: tm+mt
source-wordcount: '422'
ht-degree: 3%

---


# スパムトラップ

不正な送信者からのメールや、電子メールのベストプラクティスに従っていない送信者からのメールを識別するのに役立つスパムトラップが存在します。 スパムトラップの電子メールアドレスは、一般公開されていないので、ほとんど特定できません。 スパムトラップに電子メールを配信すると、トラップの種類やISPに応じて、様々な重大度のユーザーの評判に影響を及ぼします。 スパムトラップの種類については、以下の節を参照してください。

## リサイクル済み

リサイクルされたスパムトラップは、以前は有効でしたが、使用されなくなったアドレスです。 リストをできる限りクリーンに保つための主な方法の1つは、リスト全体に電子メールを定期的に送信し、バウンスする電子メールを適切に抑制することです。 これにより、破棄された電子メールアドレスを隔離し、それ以上の使用を差し止めることができます。

30日以内に住所がリサイクルされる場合があります。 定期的に送信することは、リストの衛生状態を保つ上で重要な点であり、非アクティブなユーザを定期的に抑える上で重要です。 **[再エンゲージメント](https://experienceleague.adobe.com/docs/campaign-classic/using/sending-messages/deliverability-management/re-engagement-best-practices.html?lang=en#sending-messages)** キャンペーンは、通常、洗練された電子メールマーケティングプログラムの一部です。このキャンペーンスタイルを使用すると、送信者は、メールが送信されなくなったユーザーを取り戻そうとします。

## 誤植

誤字スパムトラップは、誤字または奇形を含むアドレスです。 これは多くの場合、Gmailのような主要ドメインの既知の誤ったつづりで発生します(例：gmialは一般的なタイポ)。 ISPやその他のブロックリスト操作者は、スパムトラップとして使用する既知の不正ドメインを登録し、スパムマーを識別して送信者の正常性を測定します。 タイプミススパムトラップを防ぐ最善の方法は、重複の収集に&#x200B;**リストオプトインプロセス**&#x200B;を使用することです。

## プリスチン

手付かずのスパムトラップは、エンドユーザーがいなく、エンドユーザーがいないアドレスです。 これは、純粋にスパムメールを識別する目的で作成されたアドレスです。 これは、リストから掃除する際に実質的に不可能で、実質的に十分な努力が必要となる、最も効果的なタイプのスパムトラップです。 ほとんどのブロックリストは、不名誉な送信者をリストするためにプライスチンのスパムトラップを利用しています。 一般的なスパムトラップがより広いマーケティング電子メールリストに感染するのを防ぐ唯一の方法は、リスト収集用に&#x200B;**重複オプトインプロセス**&#x200B;を利用することです。

## 製品固有のリソース

**Adobe Campaign Classic**

* [SpamAssassin](https://experienceleague.adobe.com/docs/campaign-classic/using/sending-messages/deliverability-management/spamassassin.html?lang=en#using-spamassassin)

**Adobe Campaign Standard**

* [E メールおよびスパム対策分析のプレビュー](https://experienceleague.adobe.com/docs/campaign-standard-learn/tutorials/designing-content/email-designer/preview-your-email.html#designing-content)
* [重複のオプトイン処理](https://experienceleague.adobe.com/docs/campaign-standard/using/communication-channels/landing-pages/setting-up-a-double-opt-in-process.html?lang=en#communication-channels)

