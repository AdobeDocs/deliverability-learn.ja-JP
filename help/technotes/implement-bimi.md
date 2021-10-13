---
title: メッセージ識別 (BIMI) のための Gmail のブランドインジケーターの実装
description: BIMI の実装方法の詳細
topics: Deliverability
exl-id: 6b911bcc-a531-466a-8bd3-7fa469b96cc7
source-git-commit: a4d2a75e85f37f48aa3246707b98e473682e13f6
workflow-type: tm+mt
source-wordcount: '0'
ht-degree: 0%

---

# Gmail の [!DNL Brand Indicators for Message Identification](BIMI) を実装

Gmail は最近、BIMI](https://cloud.google.com/blog/products/identity-security/bringing-bimi-to-gmail-in-google-workspace) の一般的な支援を展開する [ と発表した。 この機能を利用する前に、次のような項目を扱う必要があります。マーク証明書、商標ロゴ、適切な形式のロゴ、DMARC の設定を確認し、最終的に BIMI レコードを DNS に公開しました。 この記事では、これらの手順をすべて確認します。

[!DNL Brand Indicators for Message Identification] (BIMI) は、参加プラットフォームで送信者の E メールの横に承認済みのロゴを表示できる業界標準です。この目を捉えるだけでなく、エンゲージメントを高める可能性があるだけでなく、送信者の信憑性を確認するのに役立ち、フィッシングや他のスパム戦術のリスクを減らします。

## 検証済みのマーク証明書

Gmail の BIMI プログラムの主要な要素の 1 つは、送信者が有効な認証局から発行された Verified Mark Certificate(VMC) を持っていることです。 現在、これらの VMC は Entrust と DigiCert からのみ入手できますが、Gmail の発表に従って、プロバイダーのリストは増加する可能性が高くなります。

VMC は、いくつかの点で SSL 証明書と似ています。 表示したいロゴごとに 1 つの VMC が必要になるので、多数のブランドを持っている場合は、複数の VMC を必要とする予定です。 マルチ SAN VMC を取得した場合、各 VMC は複数のドメインで有効です。 したがって、複数の送信ドメインにまたがって 1 つのロゴを表示する場合、必要な VMC は 1 つだけです。

## ロゴ商標

VMC を入手する前に、もう 1 つの重要な手順を完了する必要があります。 VMC を取得するには、表示したいロゴを、8 の承認されたグローバル商標および特許事務所のいずれかに登録する必要があります。

* 米国特許商標局 (USPTO)
* カナダ知的財産局
* 欧州連合知的財産庁
* 英国知的財産庁
* ドイツ特許 — Und Markenamt
* 日本商標局
* スペイン特許商標局 O.A.
* IP オーストラリア

表示したいロゴが登録されていない場合、またはこれらの 8 つの組織のいずれにも登録されていない場合は、VMC に申し込む前に、法務チームと協力して対応する必要があります。

## ロゴ画像形式

また、ロゴが BIMI ロゴのフォーマット要件を満たすのも良い時期です。

SVG形式で、SVGポータブル/セキュア (SVG- P/S) プロファイルに準拠する必要があります。 その方法に関するガイダンスは [BIMI Working Group](https://bimigroup.org/svg-conversion-tools-released) にあります。

## DMARC

商標のロゴが適切にフォーマットされ、検証済みマークの証明書を取得したら、BMARC が BIMI を機能させたい送信ドメインで完全に設定されていることを確認する必要があります。

これには、P=が強制隔離または拒否に設定されていることも含まれます。 P=None を使用する場合は、BIMI に該当しません。 P=None 設定は、ドメインから送信されるメールを把握し、「強制隔離」または「却下」に変更した場合に誤ってブロックされることはないことを確認するために強くお勧めします。これは、テストおよび情報収集フェーズと考えてください。 BIMI が利用できるようになる前に、それを越えて実施する必要があります。

## DNS エントリ

その他すべてが最終的に整列し、準備が整ったので、DNS エントリを BIMI で更新する時が来ました。

これは、次のような簡単なエントリです。

```
default._bimi.[domain] IN TXT “v=BIMI1; l=[SVG URL] 
```

そのエントリの詳細を入手し、[BIMI 作業グループサイト ](https://bimigroup.org/implementation-guide) で無料の BIMI チェッカーを使用することもできます。


## Key Takeaways

[!DNL Adobe Campaign] またはMarketoクライアントの場合、Adobeは BIMI DNS アップデートの作成に役立ちます。カスタマーケアに問い合わせて、リクエストしてください。 Adobeは、BIMI が正しく機能しない場合のトラブルシューティングにも役立ちます。

商標または検証済みマーク証明書に関するヘルプについては、法務チームおよび認定 VMC ベンダーと協力してください。

Gmail 用の BIMI の設定を取得するのは簡単な作業ではないかもしれませんが、マーケティングとセキュリティの両方の観点から大きなメリットを得ることができます。
