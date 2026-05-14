---
title: Gmailのメッセージ識別（BIMI）のためのブランド指標の実装
description: BIMIの導入方法を学ぶ
topics: Deliverability
role: Admin
level: Beginner
jira: KT-14079
exl-id: 6b911bcc-a531-466a-8bd3-7fa469b96cc7
TQID: https://experienceleague.adobe.com/dPuoipUKH36RSGUfhzOV1Xhu9qQTLYV4zu6Vw0Be-xY
product_v2: id: b27e5950-9033-45ac-9f86-eb22e567f615id: d0a3eab4-7b10-4d96-a71e-6c0f8e7b7c87id: dfc56824-e8b9-499e-85d4-21aedb507314
feature_v2: id: b0bb9048-d951-48d8-8232-45cf248a7e27id: e2290edd-b061-4880-9d79-dee306cf5aa9id: ea90ebee-5c84-42d9-8b21-006bdabc95a3id: f71e690b-4480-4b67-9ef5-88f42f9cdfdb
role_v2: id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
level_v2: id: e8ccd51f-da0d-4e3b-939b-e30d5ebb1ea5
topic_v2: id: aa2f3246-cb95-4b30-8899-fdf7d73550ccid: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
source-git-commit: 75df8537199680e5f1fc4b98cefdb05220fee7bf
workflow-type: tm+mt
source-wordcount: 1164
ht-degree: 0%

---

# [!DNL Brand Indicators for Message Identification]の実装（BIMI）

[!DNL Brand Indicators for Message Identification] （BIMI）は、参加プラットフォームで承認済みのロゴを送信者のメールの横に表示できるようにする、業界標準です。

この標準を使用すると、ブランドは、メールプロバイダーの受信トレイに表示するロゴを決定できます。 いわゆるBIMI DNS （Domain Name System）レコードで公開されると、メールボックスプロバイダーはこのロゴをピックアップし、特定の条件を満たした場合に受信トレイに表示する可能性があります。

異なるプロバイダーが異なる実装をしていますが、そのメリットは明らかです。インボックスで目立ち、信頼を築き、表示されることを制御することです。

BIMIは、配信品質やレピュテーションを直接向上させるわけではありません。 しかし、受信者との信頼関係を築き、エンゲージメントを促進するのに役立ちます。

## ではその企業文化とはどのようなものでしょうか？

様々なプロバイダーの実装の例と、どのプロバイダーがロゴを表示するかに関する詳細は、[BIMI グループのページ ](https://bimigroup.org/where-is-my-bimi-logo-displayed/){target="_blank"}で確認できます。

## BIMI グループとは？

BIMI グループは、ロゴだけでなく、技術的、法的、コンプライアンス要件もカバーしているため、BIMIを開発するワーキンググループです。

BIMI Groupは、Google、Yahoo、Fastmail、Proofpoint、Mailchimp、Sendgrid、Valimail、Validityなど、業界の様々な分野の複数の関係者で構成されています。

## 誰がBIMIをサポートしていますか？

BIMIをサポートするメールボックスプロバイダーのリストは、着実に増加しています。 最新のリストは、BIMIを検討しているサポート プロバイダーとプロバイダーの両方に関して[ここ](https://bimigroup.org/bimi-infographic/){target="_blank"}にあります。

2023年4月現在、リストにはGmail、Yahoo、La Poste、Fastmail、Onet.pl、Zone、Proofpointがスパム対策アプライアンスとして含まれ、Apple Mail （iOS 16以降）が含まれています。

その中で最も有名な名前は、Yahoo、Gmail、そして最近のアダプターの1つであるAppleとiOS 16です。 Appleはメールプロバイダーではないため、特別な役割を果たしていますが、ネイティブメールアプリにはBIMI サポートを追加しました。 BIMIに準拠しているメールは、「デジタル認証メール」として表示され、ブランドへの信頼度が高まります。

## 実装

BIMIの実装には、いくつかのステップがあります。

1. 送信ドメインとその組織ドメインの両方に対する適用レベルでのDMARC（Domain based Message Authentication, Reporting and Conformance）の実装 – [詳細情報](#dmarc)

1. SVG TinyPS フォーマットでのブランドロゴの作成 – [詳細情報](#create-brand-logo)

1. 検証済みマーク証明書への登録（一部のプロバイダーにのみ必要） - [詳細情報](#vmc)

1. ロゴと証明書を含むBIMI DNS レコードの公開 – [詳細情報](#publish-bimi-record)

1. 良好なレピュテーションを持つ – [詳細情報](#good-reputation)

>[!NOTE]
>
>すべての手順をオフにする必要があることに注意してください。


### DMARC {#dmarc}

DMARCは、[認証](../additional-resources/authentication.md)に失敗した電子メールに対して、メールプロバイダーが何をすべきかを決定できる標準です。 いわゆるポリシーの範囲は、「隔離」（迷惑メールフォルダーの配置）よりも「なし」、「拒否」（メールを完全にブロック）です。 後者の2つのポリシーのみが「強制」と呼ばれ、BIMIの対象となります。 SPF （Sender Policy Framework）とDKIM（Domain Keys Identified Mail）がデフォルトで設定されているため、Adobeによって送信されたメールは認証を通過しています。 Adobeは、リクエストに応じて送信ドメインにDMARCを設定しています。

送信ドメインのDMARCに加えて、DMARCは組織ドメインの適用レベルでも使用する必要があります（送信ドメインがnews.example.comの場合は、example.comが組織ドメインです）。

### ブランドロゴの作成 {#create-brand-logo}

ロゴの作成は、要件に従って100%にする必要があります。 常に[BIMI グループのガイドライン ](https://bimigroup.org/creating-bimi-svg-logo-files/){target="_blank"}を参照してください。

コンテンツ配信ネットワーク （CDN）が使用される場合、メールボックスプロバイダーがロゴを取得できないような保護（ボット保護など）を無効にする必要がある場合は、ロゴを安全な場所（HTTPS）に保存する必要があります。

技術的な要件に加えて、正方形のロゴ、背景などの単色を持つような実用的な推奨事項がいくつかあります。 これらの推奨事項は、最適なビジュアライゼーションに役立ちます。 一部のプロバイダーには、BIMI ワーキンググループの要件に追加する独自の要件があります。 例えば、[Gmail](https://support.google.com/a/answer/10911027?sjid=903725605955621707-EU){target="_blank"}では、ロゴが96 x 96 ピクセル以上である必要があります。
コンプライアンスを遵守しないと、ロゴが表示されない場合があります。

### 検証済みマーク証明書（VMC） {#vmc}

検証済みマーク証明書（VMC）は、GmailやAppleなどの一部のメールボックスプロバイダーにのみ必要なので、オプションです。 私たちは本当にBIMIを活用するためにVMCを取得することをお勧めします。

認証済みマーク証明書は、ブランドがロゴを使用できる法的検証です。 認証機関は、ブランドロゴが登録されている商標局を通じてこれを確認します。 このプロセスには、いくつかの法的な検証とチェックが必要であり、時間がかかることがあります。 現在、2つのCA （証明書認証局）がVMCを発行しています：DigicertとEntrust。 最初の商標局は、米国、カナダ、EU、英国、ドイツ、日本、オーストラリア、スペインです。

一般的なルールとして、ロゴごとに1つのVMCが必要になります。 組織ドメイン用のVMCを持つことで、サブドメインがカバーされ、さらに別のドメインでも追加機能が追加されます。 ロゴが異なる場合は、複数のVMCが必要です。 選択した認証機関またはパートナーは、この設定に役立ちます。

>[!NOTE]
>
>VMCには年会費が発生します。

### BIMI レコードの公開 {#publish-bimi-record}

他の手順が完了すると、BIMI DNS レコードを公開できます。 レコードは次のようになります。

```
default._bimi.[domain] IN TXT "v=BIMI1; l=[SVG URL]; a=[PEM URL]
```

「PEM URL」は、検証済みマーク証明書のファイルの場所です。

送信ドメインの場合は、Adobeが行う必要があります。

### 高い評価 {#good-reputation}

BIMIでは、顧客の信頼が重要です。 ユーザーは、正当な送信者のロゴのみを表示するようにメールボックスプロバイダーを信頼しています。そのため、メールボックスプロバイダーはブランドを信頼する必要があり、これは送信者のレピュテーションによって行われます。 レピュテーションが高い場合は、すべてが良いですが、そうでない場合は、ロゴは表示されません。 しかし、レピュテーションが十分に高いかどうかを判断するための情報や指標はありません。

VMCの労力や費用を費やしても、この部分を取り除くことはありません。 メールプロバイダーがブランドを信頼しない場合、ロゴは表示されません。

## ヒントとテクニック

* BIMI Groupは、BIMIの便利な検証ツールを提供しています。 すべての設定が完了しているか、ロゴが準拠しているかどうかを確認する場合は、[このリンク ](https://bimigroup.org/bimi-generator/){target="_blank"}に移動します。 後者の場合は、「**[!UICONTROL BIMI]**&#x200B;を生成」をクリックし、正しいロゴ URLを含むプレースホルダードメインを入力します。 インスペクターは、ロゴがコンプライアンスに準拠しているかどうかを確認します。

* VMCなしで安全に始めることができます。BIMI レコードにVMC URLが含まれていない場合は評判に害はありませんが、ロゴは既にYahooで表示できます。

* DMARCを組織的に導入することは、大きな課題です。 企業によっては、DMARCを十分に活用できるように支援している場合もあります。

* よくある質問の詳細なリストが[こちら](https://bimigroup.org/faqs-for-senders-esps/){target="_blank"}に公開されています。
