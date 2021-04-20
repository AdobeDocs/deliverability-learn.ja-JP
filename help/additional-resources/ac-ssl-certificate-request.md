---
title: SSL証明書要求プロセス
description: Adobeに委任したサブドメインにSSL証明書をインストールする方法を説明します。
feature: Putting it in practice
topics: Deliverability
kt: null
thumbnail: null
doc-type: article
activity: understand
team: ACS
translation-type: tm+mt
source-git-commit: 1e539b5df54250a5927701009e7a9c84e5d73fae
workflow-type: tm+mt
source-wordcount: '2269'
ht-degree: 2%

---


# SSL証明書要求プロセス

電子メールを送信するためのAdobeにドメインを委任すると（[ドメイン名の設定](/help/additional-resources/ac-domain-name-setup.md)を参照）、Adobeは特定の機能に対して特定のサブドメインを作成し、使用します。

例えば、電子メールを送信するAdobeに&#x200B;*email.example.com*&#x200B;を委任した場合、Adobeは次のようなサブドメインを作成します。
* *t.email.example.com*  — トラッキングリンク用
* *m.email.example.com* -ミラーページ用
* *res.email.example.com*  — ホストされているリソース（画像など）

SSL(HTTPS)**を介して、**&#x200B;これらのドメインを保護することをお勧めします。 実際、セキュリティで保護されていないリンク(HTTP)は傍受に弱く、最新のブラウザーで警告をフラグアップします。

これらのサブドメインにSSL証明書をインストールするには、CSRファイルを要求し、次にAdobeがインストールまたは更新できるSSL証明書を購入する必要があります。

>[!CAUTION]
>
>SSL証明書をインストールする前に、[このページ](https://experienceleague.adobe.com/docs/control-panel/using/subdomains-and-certificates/renewing-subdomain-certificate.html#installing-ssl-certificate)に記載されている前提条件を確認してください。
>
>Adobeでは、2048ビットの証明書のみがサポートされます。 4096ビット証明書はまだサポートされていません。

## 用語集 

| 用語 | 説明 |
|--- |--- |
| CA （認証局） | DigiCert、Symantecなど、組織または個人のIDを確認した後にデジタル証明書を発行するSSL証明書プロバイダー。<ul><li>信頼できるCAは、通常、ルート証明書を発行するサードパーティCAと見なされます。</li><li>証明書を使用している組織/会社と同じ組織/組織/組織が証明書に署名している場合、自己署名証明書などのSSL証明書であっても、証明書は信頼されていないCAとして分類されます。</li></ul> |
| チェーン証明書 | ルート証明書と1つ以上の中間証明書を含む証明書は、チェーン（またはチェーン）証明書と呼ばれます。 |
| CSR（証明書署名要求） | SSL証明書の申請時に証明機関に渡される、エンコードされたテキストのブロックです。 通常、証明書は証明書がインストールされているサーバーで生成されます。 |
| DER(Distinguished Encoding Rules) | 証明書拡張の種類です。 .der拡張子は、バイナリのDERエンコードされた証明書に使用されます。 これらのファイルは.cerまたは.crt拡張子もサポートしている場合があります。 |
| EV（拡張検証）証明書 | EV証明書は、フィッシング攻撃を防ぐために設計された新しい種類の証明書です。 ビジネスおよび証明書の注文者の拡張検証が必要です。 |
| 高保証証明書 | 高保証証明書は、ドメイン名の所有権と有効なビジネス登録を確認した後、CAによって発行されます。 |
| 中間CA | チェーン証明書に含まれる中間証明書の認証局。 |
| 中間証明書 | 認証局は、ツリー構造の形式で証明書を発行します。 ルート証明書は、ツリーの一番上の証明書です。 証明書とルート証明書の間にある証明書は、チェーン証明書または中間証明書と呼ばれます。 |
| 低保証証明書 | 低保証証明書（ドメイン検証証明書とも呼ばれます）には、証明書にドメイン名のみが含まれます（ビジネス名や組織名は含まれません）。 |
| PEM （プライバシー強化メール） | ASCII(Base64)データを含む.pem拡張子の証明書。 「 — - - - - - BEGIN CERTIFICATE - - — 」行を持つ証明書開始です。 |
| ルート証明書 | 認証局は、ツリー構造の形式で証明書を発行します。 ルート証明書は、ツリーの一番上の証明書です。 |
| SAN(Subject Alternative Name) | サブジェクトの代替名は、追加のホスト名（サイト、IPアドレス、共通名など）です。 の値は、単一のSSL証明書の一部として署名する必要があります。 |
| 自己署名証明書 | 信頼できる証明機関ではなく、作成者が署名した証明書です。 自己署名入り証明書は、CAによって署名された証明書と同じレベルの暗号化を有効にすることができますが、大きな欠点は2つあります。<ul><li>訪問者の接続がハイジャックされ、攻撃者が送信したすべてのデータを表示できるようにする（つまり、接続を暗号化する目的を破る）</li><li> 信頼された証明書とは異なり、証明書を失効させることはできません。</li></ul> |
| SSL (Secure Sockets Layer) | Webサーバーとブラウザーの間に暗号化されたリンクを確立するための標準的なセキュリティテクノロジーです。 |
| ワイルドカード証明書 | ワイルドカード証明書は、1つのドメイン名に対して、*.adobe.comなど、無制限の数の第1レベルのサブドメインを保護できます。 |

## 主な手順

1. 証明書署名要求(CSR)ファイルを要求し、必要な情報（国、州、市区町村、組織名、組織単位名など）を入力します。 をAdobeに追加します。
1. Adobeが生成したCSRファイルを検証し、入力した情報がすべて正しいことを確認します。
1. CSRの詳細を使用して、信頼できる証明機関<!--taking care of asking for using the subjectAltName SSL extension (SAN) if it is for several domain names, and get/purchase the resulting certificate (ideally) in PEM format for Apache server-->によって署名された証明書を生成します。
1. SSL証明書を検証し、CSRと一致することを確認します。
1. SSL証明書をAdobeに提供します。ユーザーはこの証明書をインストールします。
1. 保護された各サブドメインに対してSSL証明書が正常にインストールされていることをテストします。
1. SSL証明書の有効期間を監視します。
1. Adobe Campaign内の特定の設定を更新します。

## 詳細なプロセス

### 前提条件

ドメイン名と関数(追跡、ミラーページ、Webアプリなど)を をセキュリティで保護します。
>[!NOTE]
>
>Adobeは、関与するドメイン名と関数を定義する際に役立ちます。 詳しくは、Adobeカスタマーサクセスマネージャーにお問い合わせください。

### 手順1 - CSRファイルを取得する

CSR（証明書署名要求）ファイルを取得するには、次の手順に従います。

* [Campaign コントロールパネル](https://experienceleague.adobe.com/docs/control-panel/using/control-panel-home.html?lang=ja)にアクセスできる場合は、[このページ](https://experienceleague.adobe.com/docs/control-panel/using/subdomains-and-certificates/renewing-subdomain-certificate.html#subdomains-and-certificates)の指示に従って、Campaign コントロールパネルからCSRファイルを生成し、ダウンロードします。

* それ以外の場合は、https://adminconsole.adobe.com/を介してサポートチケットを作成し、必要なサブドメインのCSRファイルをAdobeカスタマーケアから取得します。

次に、従うべきベストプラクティスをいくつか示します。

* 委任されたサブドメインごとに1つの要求を発生させます。
* 複数のサブドメインを1つのCSR要求に結合することは可能ですが、同じ環境内でのみ可能です。 例えば、Campaign Classicでは、マーケティングサーバー、[ミッドソーシングサーバー](https://experienceleague.adobe.com/docs/campaign-classic/using/installing-campaign-classic/additional-configurations/mid-sourcing-server.html)、[実行インスタンス](https://experienceleague.adobe.com/docs/campaign-classic/using/transactional-messaging/instance-configuration/creating-a-shared-connection.html)の3つの環境が別々に存在します。
* SSL証明書を更新する前に、新しいCSRを取得する必要があります。 1年前以降の古いCSRファイルは使用しないでください。

次の情報を入力する必要があります。

>[!CAUTION]
>
>以下の表に示すフィールドはすべて入力する必要があります。 そうしないと、CSR要求は処理できません。

**Adobeチームの支援を得るための情報：**

| 提供する情報 | 値の例 | 注釈 |
|--- |--- |--- |
| クライアント名 | マイ会社 | 組織の名前。このフィールドは、Adobeが要求を追跡する際に使用します（CSR/SSL証明書には含まれません）。 |
| Adobe Campaign環境URL | https://client-mid-prod1.campaign.adobe.com | Adobe CampaignインスタンスのURL |
| 共通名[CN] | t.subdomain.customer.com | これは任意の関連ドメインにすることができますが、通常はトラッキングドメインです。 |
| サブジェクトの代替名[SAN] | t.subdomain.customer.com | 追跡サブドメインをSANとして含めてください。 |
| サブジェクトの代替名[SAN] | m.subdomain.customer.com |
| サブジェクトの代替名[SAN] | res.subdomain.customer.com |

**IT/SSL内部チームが提供する情報：**

| 提供する情報 | 値の例 | 注釈 |
|--- |--- |--- |
| 国[C] | US | 2文字のコードにする必要があります。 国全体のリスト[ここ](https://www.ssl.com/csrs/country_codes/)にアクセスします。</br>*注意：英国の場合は、GB（英国ではない）を使用します。* |
| 州（または郡名） [ST] | イリノイ | 該当する場合。 値は、略称ではなくフルネームで指定する必要があります。 |
| 市区町村名[L] | シカゴ |
| 組織名[O] | ACME |
| 組織単位名[OU] | IT |

>[!NOTE]
>
>「subdomain.customer.com」を委任されたサブドメインに置き換え、他の例の値を適切な値に置き換えます。

### 手順2 - CSRファイルの検証

関連情報を含む要求を送信した後、Adobeは、証明書署名要求(CSR)ファイルを生成して提供します。

結果のCSRファイル内のテキストは、**&quot;—BEGIN CERTIFICATE REQUEST—&quot;**&#x200B;で開始する必要があります。

AdobeからCSRファイルを受け取ったら、次の手順に従います。

1. CSRファイルのテキストを、https://www.sslshopper.com/csr-decoder.html、<!--https://www.certlogik.com/decoder/,-->、https://www.entrust.net/ssl-technical/csr-viewer.cfmなどのオンラインデコーダーにコピー&amp;ペーストします。
または、Linuxマシン上で*OpenSSL*&#x200B;コマンドをローカルで使用することもできます。 詳しくは、[この外部ページ](https://www.question-defense.com/2009/09/22/use-openssl-to-verify-the-contents-of-a-csr-before-submitting-for-a-ssl-certificate)を参照してください。
1. すべてのチェックが正常に完了したことを確認します。
1. 正しいパラメーターとドメイン名が含まれていることを確認します。
1. その他すべてのデータが、リクエストの送信時に指定した詳細と一致することを確認します。

### 手順3 - SSL証明書を生成する

CSRファイルを指定したら、CSRファイルを使用して、該当するドメインのSSL証明書を購入し、生成する必要があります。

* SSL証明書：
   * はApache PEM形式である必要があります。
   * は2048ビット以下にする必要があります。
   * は、有効なCA （証明機関）によって署名されている必要があります。
   * CSRファイルに記載されているすべてのSAN(Subject Alternative Names)を含める必要があります。
* 1つ以上の中間証明書がある場合は、ルート証明書とすべての中間証明書をAdobeに提供する必要があります。
* 証明書の有効期間は任意に設定できますが、Adobeは証明書の有効期間を十分に長く設定することを推奨します（例：2年）。

>[!NOTE]
>
>独自の内部ツールまたはCAが提供するポータルを使用して証明書を要求する場合は、証明書の生成プロセスの遅延や不一致を避けるために、CSR要求に記載されているのと同じ詳細を必ず使用してください。

### 手順4 - SSL証明書の検証

SSL証明書が生成されたら、Adobeに送信する前に検証を行う必要があります。 これをおこなうには、以下の手順に従います。

1. 証明書に.pem拡張子が付いていることを確認します。 そうでない場合は、PEM形式に変換します。 *OpenSSL*&#x200B;を使用して変換を行うことができます。
1. **&quot;—BEGIN CERTIFICATE—&quot;**&#x200B;を持つ証明書開始を確認します。
1. 証明書テキストを、https://www.sslshopper.com/certificate-decoder.htmlやhttps://www.entrust.net/ssl-technical/csr-viewer.cfmなどのオンラインデコーダーにコピーします。
または、Linuxマシン上で*OpenSSL*&#x200B;コマンドをローカルで使用することもできます。 詳しくは、[この外部ページ](https://www.shellhacks.com/decode-ssl-certificate/)を参照してください。
1. 共通名、SAN、発行者、有効期間を含む証明書が正しく解決されることを確認します。
1. SSL証明書の検証に成功した場合は、[このWebサイト](https://www.sslshopper.com/certificate-key-matcher.html)を使用して、証明書がCSRと一致していることを確認します。**CSRと証明書が**&#x200B;に一致するかどうかを確認し、証明書とCSRを対応するフィールドに入力します。 彼らは一致するはずです。

### 手順5 - SSL証明書のインストールを要求する

* [Campaign コントロールパネル](https://experienceleague.adobe.com/docs/control-panel/using/control-panel-home.html)にアクセスできる場合は、[このページ](https://experienceleague.adobe.com/docs/control-panel/using/subdomains-and-certificates/renewing-subdomain-certificate.html#installing-ssl-certificate)の指示に従って、Campaign コントロールパネルに証明書をアップロードします。

* それ以外の場合は、https://adminconsole.adobe.com/を介して別のサポートチケットを作成し、Adobeに対してAdobeサーバーへの証明書のインストールを要求します。

以下を指定する必要があります。

* 証明書ファイル、ルート証明書および（チケットに添付された）中間証明書（可能であればApache PEM形式）。
* CSRに対して引き上げられた以前のサポートチケットの数。
* CSRチケットに指定されたのと同じデータ（共通名、インスタンスURL、州、市区町村、組織名、組織単位名など）。

### 手順6 - SSL証明書のインストールをテストする

SSL証明書がAdobeカスタマーケアによってインストールされ、確認されたら、すべてのURLに対してSSL証明書が正常にインストールされていることを確認します。

SSLインストールチケットを閉じる前に、以下のテストを実行してください。 また、[このセクション](#update-configuration)の指示に従って、特定の設定を更新してください。

ブラウザーで次のURLに移動します（「subdomain.customer.com」をサブドメインに置き換えます）。

* https://subdomain.customer.com/r/test（[webアプリケーション](https://experienceleague.adobe.com/docs/campaign-classic/using/designing-content/web-applications/about-web-applications.html)サブドメインのみ） — 電子メールのサブドメインには適用されません。
* https://t.subdomain.customer.com/r/test
* https://m.subdomain.customer.com/r/test
* https://res.subdomain.customer.com/r/test

結果が成功すると環境情報が提供され、URLのアドレスバーに接続がセキュリティで保護されていることが示されます。 例えば、Google Chromeでは次のメッセージが表示されます。

![](../../help/assets/ssl-google-successful-result.png)

SSL証明書が正しくインストールされていない場合は、次の警告が表示されます。

![](../../help/assets/ssl-google-unsuccessful-result.png)

### 手順7 — 証明書の有効期間の確認

ブラウザーで証明書の有効期間を確認できます。 例えば、Google Chromeで、**セキュア**/**証明書**&#x200B;をクリックします。

有効期間を調べるのはあなたの責任です。 Adobeでは、証明書の有効期限を監視するプロセスを実装することをお勧めします。 SSL証明書の有効期限が[この記事](https://www.thesslstore.com/blog/what-happens-when-your-ssl-certificate-expires/)に切れた場合の動作の詳細を説明します。

* サポートチケットを作成して、証明書の有効期限日の少なくとも2週間前に、更新済み証明書をリクエストします。 CSRの詳細が変更されていない限り、追加のCSRを要求する必要はありません。

* [Campaign コントロールパネル](https://experienceleague.adobe.com/docs/control-panel/using/control-panel-home.html)にアクセスでき、環境がAWS環境のAdobeでホストされている場合は、Campaign コントロールパネルを使用して証明書の期限が切れる前に証明書を更新できます。 詳しくは、[この節](https://experienceleague.adobe.com/docs/control-panel/using/subdomains-and-certificates/monitoring-ssl-certificates.html#monitoring-certificates)を参照してください。

### 手順8 — 特定の設定を更新する{#update-configuration}

要求されたSSL証明書が正しくインストールされることが確認できたら、Adobe Campaign内のすべての参照をHTTPからHTTPSに更新できます。

>[!NOTE]
>
>Campaign Classicのため、更新するURLは主に[デプロイメントウィザード](https://experienceleague.adobe.com/docs/campaign-classic/using/installing-campaign-classic/initial-configuration/deploying-an-instance.html#deployment-wizard)と[外部アカウント](https://experienceleague.adobe.com/docs/campaign-classic/using/installing-campaign-classic/additional-configurations/external-accounts.html#installing-campaign-classic)(追跡、ミラーページ、パブリックリソースの各ドメイン)にあります。 Campaign Standardについては、[ブランディングの設定](https://experienceleague.adobe.com/docs/campaign-standard/using/administrating/application-settings/branding.html#about-brand-identity)を参照してください。

設定が更新されると、新しい電子メールはHTTPではなくHTTPS URLで送信されます。 URLがセキュリティで保護されたことを確認するために、次のテストをすばやく実行できます。

* Adobe Campaignから画像をアップロードします。 画像がアップロードされたら、返されるURLはHTTPSにする必要があります。
* ミラーページリンク、一部の画像、テキストおよび購読解除リンクを含むテスト用電子メール配信を作成します。 電子メールを外部の電子メールID（Gmailアドレスなど）に送信します。 受け取った電子メールを開き、SSL証明書の警告やエラーなしで、電子メール内のすべてのリンクが（HTTPではなく）HTTPS形式で正しく開くことを確認します。

## 製品固有のリソース

**Campaign Classic**

* [Campaign コントロールパネル:SSL証明書の追加（チュートリアル）](https://experienceleague.adobe.com/docs/campaign-classic-learn/control-panel/subdomains-and-certificates/adding-ssl-certificates.html) - SSL証明書を追加してサブドメインを保護する方法について説明します。

**Campaign Standard**

* [Campaign コントロールパネル:SSL証明書の追加（チュートリアル）](https://experienceleague.adobe.com/docs/campaign-standard-learn/control-panel/subdomains-and-certificates/adding-ssl-certificates.html) - SSL証明書を追加してサブドメインを保護する方法について説明します。