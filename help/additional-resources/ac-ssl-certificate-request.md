---
title: SSL証明書要求プロセス
description: DelegateにデリゲートしたサブドメインにSSL証明書をインストールする方法をAdobeします。
topics: Deliverability
doc-type: article
activity: understand
team: ACS
exl-id: 8a78abd3-afba-49a7-a2ae-8b2c75326749
source-git-commit: d6094cd2ef0a8a7741e7d8aa4db15499fad08f90
workflow-type: tm+mt
source-wordcount: '2265'
ht-degree: 2%

---

# SSL 証明書要求プロセス

Eメール送信用にAdobeにドメインをデリゲートしたら（[ドメイン名の設定](/help/additional-resources/ac-domain-name-setup.md)を参照）、Adobeは特定の機能用に特定のサブドメインを作成して使用します。

例えば、電子メール送信用に&#x200B;*email.example.com*&#x200B;をAdobeにデリゲートした場合、Adobeは次のようなサブドメインを作成します。
* *t.email.example.com*  — トラッキングリンク用
* *m.email.example.com*  — ミラーページ用
* *res.email.example.com*  — ホストされているリソース（画像など）の場合

SSL(HTTPS)**を介してこれらのドメインを**&#x200B;保護することをお勧めします。 実際、セキュリティで保護されていないリンク(HTTP)は傍受に対して脆弱で、最新のブラウザーでは警告がフラグアップされます。

これらのサブドメインにSSL証明書をインストールするには、CSRファイルをリクエストし、AdobeのSSL証明書を購入してインストールまたは更新する必要があります。

>[!CAUTION]
>
>SSL証明書をインストールする前に、[このページ](https://experienceleague.adobe.com/docs/control-panel/using/subdomains-and-certificates/renewing-subdomain-certificate.html#installing-ssl-certificate)に記載されている前提条件を確認してください。
>
>Adobeでは、最大2048ビットの証明書のみがサポートされます。 4096ビット証明書はまだサポートされていません。

## 用語集

| 用語 | 説明 |
|--- |--- |
| CA （認証局） | DigiCert、Symantecなど、組織や個人のIDを確認した後に電子証明書を発行するSSL証明書プロバイダー。<ul><li>信頼できるCAは、通常、ルート証明書を発行するサードパーティCAと見なされます。</li><li>証明書を使用している同じ組織または会社によって証明書が署名されている場合、自己署名証明書などのSSL証明書であっても、その証明書は信頼できないCAに分類されます。</li></ul> |
| チェーン証明書 | ルート証明書と1つ以上の中間証明書を含む証明書は、チェーン（またはチェーン）証明書と呼ばれます。 |
| CSR（証明書署名要求） | SSL証明書を適用する際に証明機関に提供される、エンコードされたテキストのブロック。 通常、証明書がインストールされているサーバーで生成されます。 |
| DER(Distinguished Encoding Rules) | 証明書拡張の種類。 .der拡張子は、バイナリDERでエンコードされた証明書に使用されます。 これらのファイルは、 .cerまたは.crt拡張子もサポートしている場合があります。 |
| EV（拡張検証）証明書 | EV証明書は、フィッシング攻撃を防ぐように設計された新しい種類の証明書です。 お客様のビジネスと証明書の注文者の拡張検証が必要です。 |
| 高保証証明書 | ドメイン名の所有権と有効なビジネス登録を確認した後、CAによって高保証証明書が発行されます。 |
| 中間CA | チェーン証明書に含まれる中間証明書の証明機関。 |
| 中間証明書 | 証明機関は、ツリー構造の形式で証明書を発行します。 ルート証明書は、ツリーの最上位の証明書です。 証明書とルート証明書の間の証明書は、チェーン証明書または中間証明書と呼ばれます。 |
| 低保証証明書 | 低保証証明書（ドメイン検証済み証明書とも呼ばれます）は、証明書にドメイン名のみを含みます（ビジネス名や組織名は含みません）。 |
| PEM（プライバシー強化メール） | ASCII(Base64)データを含む.pem拡張子の証明書。 このような証明書は、「 - - - - - - BEGIN CERTIFICATE - - — 」行で始まります。 |
| ルート証明書 | 証明機関は、ツリー構造の形式で証明書を発行します。 ルート証明書は、ツリーの最上位の証明書です。 |
| SAN（サブジェクトの代替名） | 件名の代替名は、追加のホスト名（サイト、IPアドレス、共通名など） これらは、単一のSSL証明書の一部として署名する必要があります。 |
| 自己署名証明書 | 信頼できる証明機関ではなく、作成者が署名した証明書。 自己署名証明書は、CAによって署名された証明書と同じレベルの暗号化を有効にできますが、次の2つの大きな欠点があります。<ul><li>訪問者の接続がハイジャックされ、攻撃者が送信されたすべてのデータを表示できる（その結果、接続を暗号化する目的がなくなる）可能性があります</li><li> 信頼された証明書と同様に、証明書は失効できません。</li></ul> |
| SSL (Secure Sockets Layer) | ウェブサーバとブラウザとの間に暗号化リンクを確立するための標準的なセキュリティ技術。 |
| ワイルドカード証明書 | ワイルドカード証明書により、1つのドメイン名（*.adobe.comなど）で無制限の数の第1レベルサブドメインを保護できます。 |

## 主な手順

1. 証明書署名要求(CSR)ファイルを要求し、必要な情報（国、都道府県、市区町村、組織名、組織単位名など）を Adobe
1. Adobeで生成されたCSRファイルを検証し、入力した情報がすべて正しいことを確認します。
1. CSRの詳細を使用して、信頼できる証明機関<!--taking care of asking for using the subjectAltName SSL extension (SAN) if it is for several domain names, and get/purchase the resulting certificate (ideally) in PEM format for Apache server-->によって署名された証明書を生成します。
1. SSL証明書を検証し、CSRと一致することを確認します。
1. SSL証明書をインストールするAdobeに指定します。
1. 保護された各サブドメインに対してSSL証明書が正常にインストールされていることをテストします。
1. SSL証明書の有効期間を監視します。
1. Adobe Campaignの特定の設定を更新します。

## 詳細なプロセス

### 前提条件

ドメイン名と機能（トラッキング、ミラーページ、Webアプリなど）を をセキュアに設定します。
>[!NOTE]
>
>Adobeは、関連付けるドメイン名と関数を定義する際に役立ちます。 詳しくは、担当のAdobeカスタマーサクセスマネージャーにお問い合わせください。

### 手順1 - CSRファイルを取得する

CSR（証明書署名要求）ファイルを取得するには、次の手順に従います。

* [Campaign コントロールパネル](https://experienceleague.adobe.com/docs/control-panel/using/control-panel-home.html?lang=ja)にアクセスできる場合は、[このページ](https://experienceleague.adobe.com/docs/control-panel/using/subdomains-and-certificates/renewing-subdomain-certificate.html#subdomains-and-certificates)の手順に従って、Campaign コントロールパネルからCSRファイルを生成し、ダウンロードします。

* それ以外の場合は、 https://adminconsole.adobe.com/を使用してサポートチケットを作成し、必要なサブドメインに対して、AdobeカスタマーケアからCSRファイルを取得します。

以下に、従うべきベストプラクティスをいくつか示します。

* デリゲートされたサブドメインごとに1つの要求を発生させます。
* 複数のサブドメインを1つのCSRリクエストに組み合わせることができますが、同じ環境内でのみ可能です。 例えば、Campaign Classicでは、マーケティングサーバー、[ミッドソーシングサーバー](https://experienceleague.adobe.com/docs/campaign-classic/using/installing-campaign-classic/install-campaign-on-prem/mid-sourcing-server.html)、[実行インスタンス](https://experienceleague.adobe.com/docs/campaign-classic/using/transactional-messaging/configure-transactional-messaging/configuring-instances.html#execution-instance)が3つの異なる環境になります。
* SSL証明書を更新する前に、新しいCSRを取得する必要があります。 1年以上前の古いCSRファイルは使用しないでください。

次の情報を入力する必要があります。

>[!CAUTION]
>
>以下の表に示すフィールドはすべて入力する必要があります。 そうしないと、CSRリクエストを処理できません。

**Adobeチームの支援を得るための情報：**

| 提供する情報 | 値の例 | 注釈 |
|--- |--- |--- |
| クライアント名 | マイカンパニー | 組織の名前。このフィールドは、Adobeがリクエストの追跡に使用します（CSR/SSL証明書には含まれません）。 |
| Adobe Campaign環境URL | https://client-mid-prod1.campaign.adobe.com | Adobe CampaignインスタンスのURL。 |
| 共通名[CN] | t.subdomain.customer.com | これは、任意の関連ドメインですが、通常はトラッキングドメインです。 |
| サブジェクトの代替名[SAN] | t.subdomain.customer.com | トラッキングサブドメインをSANとして含めてください。 |
| サブジェクトの代替名[SAN] | m.subdomain.customer.com |
| サブジェクトの代替名[SAN] | res.subdomain.customer.com |

**IT/SSL社内チームから提供される情報：**

| 提供する情報 | 値の例 | 注釈 |
|--- |--- |--- |
| 国[C] | 米国 | これは2文字のコードにする必要があります。 [ここ](https://www.ssl.com/csrs/country_codes/)から国名の一覧にアクセスします。</br>*注意：英国の場合は、GB（英国ではない）を使用します。* |
| 都道府県名[ST] | イリノイ | 該当する場合。 値は省略ではなく、完全な名前にする必要があります。 |
| 市区町村名[L] | シカゴ |
| 組織名[O] | ACME |
| 組織単位名[OU] | IT |

>[!NOTE]
>
>「subdomain.customer.com」をデリゲートされたサブドメインに置き換え、他のサンプル値を適切な値に置き換えます。

### 手順2 - CSRファイルの検証

関連情報を使用して要求を送信すると、Adobeが証明書署名要求(CSR)ファイルを生成して提供します。

結果のCSRファイルのテキストは、**&quot;—BEGIN CERTIFICATE REQUEST—&quot;**&#x200B;で始まる必要があります。

CSRファイルをAdobeから受け取ったら、次の手順に従います。

1. CSRファイルテキストを、https://www.sslshopper.com/csr-decoder.html、<!--https://www.certlogik.com/decoder/,-->、https://www.entrust.net/ssl-technical/csr-viewer.cfmなどのオンラインデコーダーにコピー&amp;ペーストします。
または、Linuxマシン上でローカルに*OpenSSL*&#x200B;コマンドを使用できます。 詳しくは、[この外部ページ](https://www.question-defense.com/2009/09/22/use-openssl-to-verify-the-contents-of-a-csr-before-submitting-for-a-ssl-certificate)を参照してください。
1. すべてのチェックが正常に実行されたことを確認します。
1. 正しいパラメーターとドメイン名が含まれていることを確認します。
1. その他のすべてのデータが、リクエストの送信時に指定した詳細と一致することを確認します。

### 手順3 - SSL証明書の生成

CSRファイルを指定したら、CSRファイルを使用して、適切なドメインのSSL証明書を購入し、生成する必要があります。

* SSL証明書：
   * はApache PEM形式である必要があります。
   * は2048ビット以下にする必要があります。
   * は、有効なCA（証明機関）によって署名されている必要があります。
   * CSRファイルに記載されているように、すべてのSAN（サブジェクトの代替名）を含める必要があります。
* 1つ以上の中間証明書がある場合は、ルート証明書とすべての中間証明書をAdobeに指定する必要があります。
* 証明書の有効期間は任意に設定できますが、Adobeは証明書の有効期間を十分に長く選択することを推奨します（例：2年）。

>[!NOTE]
>
>独自の内部ツールまたはCAが提供するポータルを使用して証明書を要求する場合は、証明書生成プロセスで遅延や不一致が生じないよう、CSR要求で指定したのと同じ詳細を必ず使用してください。

### 手順4 - SSL証明書の検証

SSL証明書が生成されたら、Adobeに送信する前に検証する必要があります。 これをおこなうには、以下の手順に従います。

1. 証明書の拡張子が.pemであることを確認します。 該当しない場合は、PEM形式に変換します。 *OpenSSL*&#x200B;を使用して変換を行うことができます。
1. 証明書が&#x200B;**&quot;—BEGIN CERTIFICATE—&quot;**&#x200B;で始まっていることを確認します。
1. 証明書のテキストを、オンラインのデコーダー(https://www.sslshopper.com/certificate-decoder.htmlやhttps://www.entrust.net/ssl-technical/csr-viewer.cfmなど)にコピーします。
または、Linuxマシン上でローカルに*OpenSSL*&#x200B;コマンドを使用できます。 詳しくは、[この外部ページ](https://www.shellhacks.com/decode-ssl-certificate/)を参照してください。
1. 共通名、SAN、発行者、有効期間を含む証明書が正しく解決されていることを確認します。
1. SSL証明書の検証が成功した場合は、[このWebサイト](https://www.sslshopper.com/certificate-key-matcher.html)を使用して証明書がCSRと一致することを確認します。**CSRと証明書が一致するかどうかを確認し、該当するフィールドに証明書とCSRを入力します。**&#x200B;一致するはずです。

### 手順5 - SSL証明書のインストールを要求する

* [Campaign コントロールパネル](https://experienceleague.adobe.com/docs/control-panel/using/control-panel-home.html)にアクセスできる場合は、[このページ](https://experienceleague.adobe.com/docs/control-panel/using/subdomains-and-certificates/renewing-subdomain-certificate.html#installing-ssl-certificate)の手順に従って、Campaign コントロールパネルに証明書をアップロードします。

* それ以外の場合は、https://adminconsole.adobe.com/から別のサポートチケットを作成して、Adobeに証明書をAdobeサーバーにインストールするよう要求します。

以下を指定する必要があります。

* 証明書ファイル、ルート証明書および（チケットに添付されている）中間証明書。できれば、Apache PEM形式です。
* CSRに対して引き上げられた以前のサポートチケットの数。
* CSRチケットに指定されたデータと同じもの（共通名、インスタンスURL、状態、市区町村、組織名、組織単位名など）。

### 手順6 - SSL証明書のインストールのテスト

SSL証明書がインストールされ、Adobeカスタマーケアによって確認されたら、すべてのURLに対して正常にインストールされていることを確認します。

SSLインストールチケットを閉じる前に、以下のテストを実行します。 また、[この節](#update-configuration)の指示に従って、特定の設定を更新してください。

ブラウザーで次のURLに移動します（「subdomain.customer.com」をサブドメインに置き換えます）。

* https://subdomain.customer.com/r/test （[webアプリケーション](https://experienceleague.adobe.com/docs/campaign-classic/using/designing-content/web-applications/about-web-applications.html)サブドメインのみ — 電子メールのサブドメインには適用されません）
* https://t.subdomain.customer.com/r/test
* https://m.subdomain.customer.com/r/test
* https://res.subdomain.customer.com/r/test

成功すると、環境情報が表示され、URLのアドレスバーに接続がセキュリティで保護されていることが示されます。 例えば、Google Chromeで次のメッセージを表示できます。

![](../../help/assets/ssl-google-successful-result.png)

SSL証明書が正しくインストールされていない場合は、次の警告が表示されます。

![](../../help/assets/ssl-google-unsuccessful-result.png)

### 手順7 — 証明書の有効期間の確認

ブラウザーで証明書の有効期間を確認できます。 例えば、Google Chromeで、**セキュア** /**証明書**&#x200B;をクリックします。

有効期間を確認するのは、お客様の責任です。 Adobeでは、証明書の有効期限を監視するプロセスを実装することをお勧めします。 [この記事](https://www.thesslstore.com/blog/what-happens-when-your-ssl-certificate-expires/)でSSL証明書の有効期限が切れた場合の影響について詳しく説明します。

* サポートチケットを作成して、証明書の有効期限の2週間前以降に更新された証明書をリクエストします。 CSRの詳細が変更されていない限り、追加のCSRをリクエストする必要はありません。

* [Campaign コントロールパネル](https://experienceleague.adobe.com/docs/control-panel/using/control-panel-home.html)にアクセスでき、環境がAWS環境でAdobeによってホストされている場合は、Campaign コントロールパネルを使用して証明書を期限切れにする前に更新できます。 詳しくは、[この節](https://experienceleague.adobe.com/docs/control-panel/using/subdomains-and-certificates/monitoring-ssl-certificates.html#monitoring-certificates)を参照してください。

### 手順8 — 特定の設定を更新する {#update-configuration}

要求されたSSL証明書が正しくインストールされると確信したら、Adobe Campaignのすべての参照をHTTPからHTTPSに更新できます。

>[!NOTE]
>
>Campaign Classicの場合、更新するURLは主に[デプロイウィザード](https://experienceleague.adobe.com/docs/campaign-classic/using/installing-campaign-classic/initial-configuration/deploying-an-instance.html#deployment-wizard)と[外部アカウント](https://experienceleague.adobe.com/docs/campaign-classic/using/installing-campaign-classic/accessing-external-database/external-accounts.html)（トラッキング、ミラーページ、パブリックリソースドメイン）にあります。 Campaign Standardについては、[ブランディング設定](https://experienceleague.adobe.com/docs/campaign-standard/using/administrating/application-settings/branding.html#about-brand-identity)を参照してください。

設定が更新されると、HTTPではなくHTTPS URLを使用して新しい電子メールが送信されます。 URLがセキュリティで保護されたことを確認するには、次のテストをすばやく実行できます。

* Adobe Campaignから画像をアップロードします。 画像がアップロードされたら、返されるURLはHTTPSにする必要があります。
* ミラーページのリンク、一部の画像、テキスト、購読解除リンクを含むテスト用Eメール配信を作成します。 外部の電子メールID（Gmailアドレスなど）に電子メールを送信します。 受信したら、電子メールを開き、SSL証明書の警告やエラーなしで、電子メール内のすべてのリンクが（HTTPではなく）HTTPS形式で正しく開くことを確認します。

## 製品固有のリソース

**Campaign Classic**

* [Campaign コントロールパネル:SSL証明書の追加（チュートリアル）](https://experienceleague.adobe.com/docs/campaign-classic-learn/control-panel/subdomains-and-certificates/adding-ssl-certificates.html)  - SSL証明書を追加してサブドメインを保護する方法を説明します。

**Campaign Standard**

* [Campaign コントロールパネル:SSL証明書の追加（チュートリアル）](https://experienceleague.adobe.com/docs/campaign-standard-learn/control-panel/subdomains-and-certificates/adding-ssl-certificates.html)  - SSL証明書を追加してサブドメインを保護する方法を説明します。
