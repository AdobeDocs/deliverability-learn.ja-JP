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
source-git-commit: 9444f8601f2f349398ee5deb9d5f4d4f7abb44f5
workflow-type: ht
source-wordcount: '453'
ht-degree: 100%

---

# スパムトラップ

スパムトラップは、不正な送信者や E メールのベストプラクティスに従っていない送信者からのメールを識別するために利用されます。スパムトラップの E メールアドレスは、通常一般公開されないので、ほぼ特定不可能です。スパムトラップに E メールを配信すると、送信者の評判に対し、トラップの種類や ISP に応じて多様な程度の影響を及ぼします。以下の節で、異なる種類のスパムトラップについて詳しく説明します。

## 再利用

再利用型のスパムトラップは、以前は有効だったが今では使用されなくなったアドレスです。リストをできる限りクリーンに保つための主な方法の 1 つは、定期的にリスト全体に E メールを送信し、バウンスする E メールを適切に抑制することです。これにより、破棄された E メールアドレスを強制隔離し、それ以降の使用を停止できます。

場合によっては、アドレスが 30 日以内に再利用されることもあります。定期的な送信をおこない、非アクティブユーザーを抑制することは、リストの衛生状態を保つうえで重要な点です。**再エンゲージメントキャンペーン**&#x200B;は通常、高度な電子メールマーケティングプログラムの一部です。 このキャンペーンスタイルでは、送信者は、メール送信対象ではなくなったユーザーを取り戻すための試行が可能です。

## タイプミス

タイプミス型のスパムトラップは、誤字または変形を含むアドレスです。これは多くの場合、Gmail など主要ドメインの既知の誤ったつづりで発生します（例：gmial はよくあるタイプミスです）。ISP やその他のブロックリスト運営者は、スパムトラップとして使用するために既知の不正ドメインを登録し、スパマーの識別、送信者の健全性の測定をおこないます。タイプミス型のスパムトラップを回避する最善の方法は、リスト収集に&#x200B;**ダブルオプトインプロセス**&#x200B;を使用することです。

## 未使用

未使用型のスパムトラップは、現在も過去にもエンドユーザーがいないアドレスです。これは、スパムメールを識別する目的のみに作成されたアドレスです。これは、最も影響力が大きい種類のスパムトラップです。実質的に特定は不可能で、リストから除去するには相当な努力を必要とします。ほとんどのブロックリストは、未使用型のスパムトラップを利用して信用できない送信者をリストに追加します。未使用型スパムトラップが広範なマーケティング E メールリストに侵入するのを防ぐ唯一の方法は、リスト収集時に&#x200B;**ダブルオプトインプロセス**&#x200B;を利用することです。

## その他のリソース

* [このセクション](/help/additional-resources/all-about-spam-traps.md)では、スパムトラップの特定と回避の詳細について説明します。
* [このセクション](/help/additional-resources/re-engagement.md)では、再エンゲージメント戦略を通じて配信品質を向上させる方法の詳細について説明します。

## 製品固有のリソース

**Adobe Campaign Classic**

* [SpamAssassin](https://experienceleague.adobe.com/docs/campaign-classic/using/sending-messages/deliverability-management/spamassassin.html?lang=ja#using-spamassassin)
* [ダブルオプトインによる購読フォームの作成](https://experienceleague.adobe.com/docs/campaign-classic/using/designing-content/web-forms/use-cases--web-forms.html?lang=ja#create-a-subscription--form-with-double-opt-in)

**Adobe Campaign Standard**

* [E メールおよびスパム対策分析のプレビュー](https://experienceleague.adobe.com/docs/campaign-standard-learn/tutorials/designing-content/email-designer/preview-your-email.html?lang=ja#designing-content)
* [ダブルオプトインプロセス](https://experienceleague.adobe.com/docs/campaign-standard/using/communication-channels/landing-pages/setting-up-a-double-opt-in-process.html?lang=ja#communication-channels)
