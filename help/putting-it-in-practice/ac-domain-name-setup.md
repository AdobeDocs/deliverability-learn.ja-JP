---
title: ドメイン名の設定
description: サブドメインをAdobe Campaignに委任する方法を説明します。
feature: 実際に使う
topics: Deliverability
kt: null
thumbnail: null
doc-type: article
activity: understand
team: ACS
translation-type: tm+mt
source-git-commit: 96ed84da391faaabd3001ddd6a411ddc1f46b033
workflow-type: tm+mt
source-wordcount: '2032'
ht-degree: 2%

---


# ドメイン名の設定

このドキュメントでは、ドメイン名の設定と委任に関するビジネス要件と技術要件について説明します。 使用しているAdobeプラットフォーム用のWebコンポーネント(ランディングページ、オプトアウトページ)をホストするための、外部に接続するサブドメイン（サブドメイン）を送信する電子メールを選択する必要があります。

>[!NOTE]
>
>また、Campaign コントロールパネル（ベータ版）を使用して新しいサブドメインを設定することもできます。 詳しくは、[この節](https://experienceleague.adobe.com/docs/control-panel/using/subdomains-and-certificates/setting-up-new-subdomain.html#must-read)を参照してください。

## サブドメイン

Adobeにより、デジタルマーケティングは、ブランドの顧客エンゲージメントマーケティングプログラムを強化する、コンテキストに基づくエンジンに本当になり得ます。  電子メールは、引き続きデジタルマーケティングプログラムの基盤となります。 しかし、受信トレイに到達するのは今まで以上に難しくなっています。

電子メールキャンペーンのサブドメインを作成すると、異なるタイプのトラフィック（マーケティングや企業など）を特定のIPプールと特定のドメインに分離できるので、[IP暖機プロセス](../../help/additional-resources/increase-reputation-with-ip-warming.md)の速度が向上し、配信品質が向上します。 ドメインを共有していて、そのドメインがブロックされたりブロックリストに追加された場合は、会社のメール配信に影響を与える可能性があります。 ただし、電子メールマーケティングの通信に固有のドメインでの評判の問題やブロックは、電子メールのフローにのみ影響を与えます。  複数のメールストリームの送信者または「送信者」アドレスとしてメインドメインを使用すると、電子メールの認証が中断され、メッセージがブロックされたりスパムフォルダーに配置されたりする場合もあります。

### 委任

ドメイン名の委任は、ドメイン名(技術的には：DNSゾーン)を使用して、その分割を委任する(技術的には：その下にあるDNSゾーン（サブゾーンと呼ぶことができます）を別のエンティティに対して呼び出します。 基本的に、顧客がゾーン「example.com」を処理している場合、「marketing.example.com」というサブゾーンをAdobe Campaignに委任できます。

つまり、Adobe CampaignのDNSサーバーは、そのゾーンに対してのみ完全な権限を持ち、トップレベルドメインに対しては権限を持ちません。 Adobe CampaignのDNSサーバーは、「t.marketing.example.com」自体ではなく「www.example.com」など、そのゾーン内のドメイン名に関するクエリに対して権限のある回答を提供します。

Adobe Campaignで使用するサブドメインを委任することで、クライアントは、社内電子メールドメインのDNSの保守と管理を継続しながら、電子メールマーケティング用の業界標準の配信品質要件を満たすために必要なDNSインフラストラクチャを維持するAdobeに依存できます。  サブドメインの委任では次のことが可能です。

DNSエイリアスとドメイン名を使用してブランドイメージを保持するクライアント
電子メール送信時に配信品質を完全に最適化するためのすべての技術的なベストプラクティスを自律的に実装するAdobe

## DNSセットアップオプション

クラウドベースのマネージドサービスを提供するために、Adobeは、Adobe Campaignの展開時にサブドメインの委任を使用することを強くお勧めします。  ただし、Adobeはオファークライアントに対して、DNSを設定するための別のオプション（CNAME設定）を提供します。

| オプション | 説明 | Adobe責任 | お客様の責任 |
|--- |------- |--- |--- |
| Adobe Campaignへのサブドメインの委任 | クライアントはサブドメイン(email.example.com)をAdobeに委任します。 このシナリオでは、Adobeは、電子メールキャンペーンの配信、レンダリング、追跡に必要なDNSのすべての要素を制御し、保守することで、キャンペーンを管理対象サービスとして配信できます。 | サブドメインとAdobe Campaignに必要なすべてのDNSレコードの完全な管理。 | サブドメインのAdobeへの適切な委任 |
| CNAME の使用 | クライアントはサブドメインを作成し、CNAMEを使用してAdobe固有のレコードを指定します。  この設定を使用すると、アドビとお客様の両方が DNS の維持に対する責任を共有します。 | Adobe Campaignに必要なDNSレコードの管理。 | サブドメインの作成と制御、およびAdobe Campaignに必要なCNAMEレコードの作成と管理。 |

## 必要なDNSレコード

| レコードの種類 | 目的 | レコード/コンテンツの例 |
|--- |--- |--- |
| MX | 受信メッセージ用のメールサーバーを指定する | <i>email.example.com</i></br><i>10 inbound.email.example.com</i> |
| SPF(TXT) | Sender Policy Framework | <i>email.example.com</i></br>&quot;v=spf1 redirect=__spf.キャンペーン.adobe.com&quot; |
| DKIM(TXT) | DomainKeys識別メール | <i>client._domainkey.email.example.com</i></br>&quot;v=DKIM1;k=rsa;&quot; &quot;DKIMPUBLICKEY HERE&quot; |
| DMARC(TXT) | ドメインベースのメッセージ認証 | レポートと準拠 | _dmarc.email.example.com</br>&quot;v=DMARC1;p=none;rua=mailto:mailauth-reports@myemail.com&quot; |
| ホストレコード(A) | ミラーページ、画像ホスティング、トラッキングリンク、すべての送信ドメイン | A 123.111.100.99 IN A 123.111.100.99</br>t.email.example.com IN A 123.111.100.98</br>email.example.com IN A 123.111.100.97 |
| 逆DNS (PTR) | クライアントのIPアドレスをクライアントブランドのホスト名にマップします | 18.101.100.192.in-addr.arpaドメイン名ポインタr18.email.example.com |
| CNAME | 別のドメイン名にエイリアスを指定します。 | t1.email.example.comは、 | t1.email.example.campaign.adobe.com |

## 設定要件

### サブドメインの委任

この場合、クライアントはDNSサーバーにサブドメインを作成し、Adobeが管理するサブドメインのネームサーバーを定義する必要があります。  例えば、メインドメイン名が「example.com」で、電子メール配信のAdobeに「marketing.example.com」の管理を委任するクライアントは、次の種類のレコードをDNSに追加するために、この委任を実現する必要があります。

```
marketing.example.com. NS a.ns.campaign.adobe.com.
marketing.example.com. NS b.ns.campaign.adobe.com.
marketing.example.com. NS c.ns.campaign.adobe.com.
marketing.example.com. NS d.ns.campaign.adobe.com.
```

ドメイン名の委任は、このドメインがAdobe Campaignプラットフォーム経由での電子メール配信専用になるので、他の方法（例えば、別の電子メールインフラストラクチャからの電子メールの送信）には使用できないことを意味します。

セットアッププロセス中、Adobeは、これらのドメインに返されるリバウンド電子メール（MXタイプDNSレコードの設定）を管理および処理するために、Adobeが受信電子メールインフラストラクチャに接続されていることを確認します。

### CNAME の使用

クライアントがサブドメインをAdobeに委任せずにCNAMEを使用する場合、セットアップ段階で、AdobeはクライアントDNSサーバに配置するレコードを提供し、Adobe CampaignDNSサーバで対応する値を設定します。

## 導入に関する一般的な要件

新しいエンタープライズマーケティングソリューションを導入する場合、外部から直接アクセスするコンポーネントに関する要件があります。  例えば、ホスティングランディングページやWebフォーム、追跡するリンクやWebページの設定、ミラーページの表示、オプトアウトページの設定などがあります。

これらの要件は、Adobeと顧客の両方がホストするコンポーネントによって管理されますが、電子メールの受信者が参照できるURLが含まれています。  基盤となる技術ソリューションやホスティングプロバイダーを示すURLを持つことを避けるために、電子メールの受信者に対してこの情報を透過的にするようにサブドメインを設定できます。  例えば、http://www.customer.com/のようなURLを見ると、ドメインは「www.customer.com」になります。  このサブドメインは「www」になります。

### サブドメインの要件

Adobe Campaignアプリケーションから、ブランドURL(ミラーページおよび追跡URL)に使用するサブドメインを決定します。  また、電子メール配信の各サブドメインの「送信者のアドレス」、「送信者の名前」、「返信先のアドレス」も決定します。

以下の表を完成させます。最初の行は一例にすぎません。

| Subdomain | 送信元アドレス | 送信元名 | 返信先のアドレス |
|--- |--- |--- |--- |
| emails.customer.com | news@emails.customer.com | 顧客 | customercare@customer.com |
| </br> | </br> | </br> | </br> |

>[!NOTE]
>
>* [返信先アドレス]フィールドは、受信者が[差出人アドレス]とは異なるアドレスに返信する場合に使用します。  必須フィールドではありませんが、Adobeは、「Reply-To Address」が有効で、監視対象のメールボックスにリンクされていることを強く推奨します。  このメールボックスは、お客様がホストする必要があります。  例えば、customercare@customer.comのような、電子メールが読み取られ応答するサポート用のメールボックスを指定できます。
>* お客様が「Reply-To Address」を選択しない場合、デフォルトのアドレスは常に`<tenant>-<type>-<env>@<subdomain>`です。
>* 「Reply-To Address」がこのように設定されると、返信は監視されていないメールボックスに送信されます。
>* Adobe Campaignから電子メールを送信する際、「送信者アドレス」メールボックスは監視されず、マーケティングユーザーはこのメールボックスにアクセスできません。 Adobe Campaignは、このメールボックスで受信した自動返信または自動転送の電子メールの機能をオファーしません。
>* キャンペーンの送信者/送信者のアドレスとエラーのアドレスは、「悪用」または「ポストマスター」にできません。


## サブドメインのデリゲート

Adobe Campaignプラットフォームに使用するサブドメインは、4つのネームサーバー(NS)レコードを作成することで委任する必要があります。  これにより、サブドメインをAdobeに適切に委任できます。  サブドメインの委任と各DNS命令の例を以下に示します。  「emails.customer.com」を委任するサブドメインに置き換えてください。  サブドメインは一意である必要があり、既に他のパーティ（既存のESPやMSPなど）で使用されていることはできません。

| 委任されたサブドメイン | DNS命令 |
|--- |--- |
| `<subdomain>` | `<subdomain>` NS a.ns.campaign.adobe.com。  </br> `<subdomain>` NS b.ns.campaign.adobe.com。  </br> `<subdomain>` NS c.ns.campaign.adobe.com。  </br> `<subdomain>` NS d.ns.campaign.adobe.com。 |

## トラッキング、ミラーページ、リソース

電子メール送信サブドメインがAdobe Campaignに適切に委任/委任されると、Adobeテクニカルオペレーション(TechOps)チームは、トラッキングとミラーページを個別に管理する2つ以上の下位レベルドメインを作成します。

| タイプ | Domain |
|--- |--- |
| ミラーページ | m.`<subdomain>` |
| トラッキング | t.`<subdomain>` |
| リソース | res.`<subdomain>` |

## クラウドの導入（オプション）

これは、Adobe Campaign Classicがクラウド内でAdobeによって完全にホストされている場合にのみ適用されます。  これはオプションの設定です。

開発対象の調査、Webフォームおよびランディングページは、Adobe Campaignを通じてクラウドで完全にホストされます。  必要に応じて、追加のサブドメインをAdobe（web.customer.comなど）に委任し、ツール内のWebコンポーネントに使用できます。  サブドメインは一意である必要があり、他のパーティ（既存のESPやMSPなど）で使用できないことに注意してください。

| 委任されたサブドメイン | DNS命令 |
|--- |--- |
| `<subdomain>` | `<subdomain>` NS a.ns.campaign.adobe.com。</br>`<subdomain>` NS b.ns.campaign.adobe.com。</br>`<subdomain>` NS c.ns.campaign.adobe.com。</br>`<subdomain>` NS d.ns.campaign.adobe.com。 |

>[!NOTE]
>
>デフォルトでは、ツール内のWebコンポーネントは、電子メールに使用する権限を委任された最初のサブドメインを使用します。

## クラウドメッセージングの導入（オプション）

Adobe Campaign Classicのマーケティングインスタンスがお客様のオンプレミスでホストされる場合は、お客様が追加の技術的な設定を行う必要があります。

開発対象の調査、Webフォームおよびランディングページは、Adobe Campaignマーケティングインスタンス(受信者レコードが存在する)で管理されます。

Adobe Campaignマーケティングインスタンスがホストする外部に接続するWebコンポーネントを展開するには、追加のCNAME DNS設定が必要です。  これにより、Webコンポーネント（web.customer.comなど）がインターネットに公開され、お客様のドメインのブランドで提供されます。

また、これらのWebコンポーネントをホストするAdobe Campaignマーケティングインスタンス（ポート80または443）へのアクセスを許可するように、ファイアウォールを設定する必要があります。

**ベストプラクティスRecommendations:**

Webコンポーネントをホストするサブドメインは、顧客に表示されるので、次のように、手動で入力する必要がある場合があるので、適切にブランド化し、覚えやすくします。https://web.customer.com
安全なページ(HTTPS)でフォームをホストする必要がある場合は、以下に説明する技術的な設定を追加する必要があります。

| 委任されたサブドメイン | DNS命令 |
|--- |--- |
| `<subdomain>` | `<subdomain>` CNAME `<internal customer server>` |

## レンダリングされたサービス

これらの委任の後、Adobeがインフラストラクチャを導入すると、委任された送信ドメインまたはCNAMEに基づく送信ドメインごとに、次のサービスが実行されます。

* postmaster@の作成と@ inboxの無効化
* 委任ドメインのフィードバック・ループの設定
* リクエストに応じて、Adobeは指定したDMARCレコードも設定します。 配信品質コンサルタントは、ドメインを送信する際の長期DMARCポリシーの設計と計画を支援します。
Adobeによって設定されたパラメーターは、委任が完了し、Adobeによって検証された時点からのみ有効で、引き続き機能します。  すべてのAdobe Campaignクラウドオファーに、標準としてドメイン名の委任が含まれます。

## 請求条件と導入条件

* 選択した最初の契約とパッケージの種類に応じて、最初の委任の後に標準として含まれる委任以外の委任も含めることができます。
* これらの委任以外にも、追加の委任に対して請求が発生します。
* これらの追加委任の請求方法は、最初の契約で指定されたとおり、追加の月額料金で行われます。

CLIENTがAdobe Campaignツールを使用して配信専用の関連ドメイン名を選択し、関連ドキュメントに詳細に示す委任の前提条件が正しく実装されている場合、これらの委任は受け入れられます。

## 業務の廃止

CLIENTは、委任サービスの利点がなくなるように書面による要求を行い、必要なDNS設定を自ら引き継ぐことができます。

このような状況が発生した場合、Adobeは、非ドメイン委任モードに戻すのに必要なサービス日数の見積もりをCLIENTに提供します。

Adobeは、前述の配信品質率に関する責任を負わない場合、お客様が上記のコミットメントを遵守できないと、その責任を免除されます。

Marketing Cloudサービスが終了すると、ドメインの委任が自動的に終了し、Adobe別にそれらのドメインのDNSメンテナンスが行われます。

## Campaign コントロールパネルを使用したサブドメインの監視

インスタンスに対してサブドメインを設定したら、Campaign コントロールパネルを使用してサブドメインを監視できます。

これにより、Adobe Campaignに委任したすべてのサブドメインを表示し、SSL証明書の更新を要求できます。

詳しくは、[該当するドキュメント](https://experienceleague.adobe.com/docs/control-panel/using/subdomains-and-certificates/monitoring-subdomains.html#subdomains-and-certificates)を参照してください。

>[!NOTE]
>
>[制御](https://experienceleague.adobe.com/docs/control-panel/using/control-panel-home.html?lang=ja) パネルは、Adobe Managed Servicesを使用するお客様のみ利用できます。