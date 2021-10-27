---
title: SSL 証明書要求プロセス
description: Delegation にデリゲートしたサブドメインに SSL 証明書をインストールするAdobe。
topics: Deliverability
doc-type: article
activity: understand
team: ACS
exl-id: 8a78abd3-afba-49a7-a2ae-8b2c75326749
source-git-commit: d6094cd2ef0a8a7741e7d8aa4db15499fad08f90
workflow-type: tm+mt
source-wordcount: '2265'
ht-degree: 3%

---

# SSL 証明書要求プロセス

E メール送信用にドメインをAdobeにデリゲートしたら（[ ドメイン名の設定 ](/help/additional-resources/ac-domain-name-setup.md) を参照）、Adobeは特定の機能に対して特定のサブドメインを作成し、使用します。

例えば、電子メールの送信用にAdobeに *email.example.com* をデリゲートした場合、Adobeは次のようなサブドメインを作成します。
* *t.email.example.com*  — トラッキングリンク用
* *m.email.example.com*  — ミラーページ用
* *res.email.example.com*  — ホストされているリソース（画像など）の場合

SSL(HTTPS)**を介してこれらのドメインを** 保護することをお勧めします。 実際、セキュリティで保護されていないリンク (HTTP) は傍受に対して脆弱で、最新のブラウザーでは警告がフラグアップされます。

これらのサブドメインに SSL 証明書をインストールするには、CSR ファイルをリクエストし、その後、Adobeがインストールまたは更新する SSL 証明書を購入する必要があります。

>[!CAUTION]
>
>SSL 証明書をインストールする前に、[ このページ ](https://experienceleague.adobe.com/docs/control-panel/using/subdomains-and-certificates/renewing-subdomain-certificate.html?lang=ja#installing-ssl-certificate) に記載されている前提条件を確認してください。
>
>Adobeは、最大 2048 ビットの証明書のみをサポートします。 4096 ビット証明書は、まだサポートされていません。

## 用語集

| 用語 | 説明 |
|--- |--- |
| CA （認証局） | DigiCert、Symantec など、組織や個人の ID を確認した後に電子証明書を発行する SSL 証明書プロバイダー。<ul><li>信頼できる CA は、通常、ルート証明書を発行するサードパーティ CA と見なされます。</li><li>証明書を使用している同じ組織または会社が証明書に署名している場合、自己署名証明書などの SSL 証明書であっても、その証明書は信頼されていない CA と分類されます。</li></ul> |
| チェーン証明書 | ルート証明書と 1 つ以上の中間証明書を含む証明書は、チェーン（またはチェーン）証明書と呼ばれます。 |
| CSR（証明書署名要求） | SSL 証明書の申請時に認証局に提供される、エンコードされたテキストのブロック。 通常は、証明書がインストールされているサーバーで生成されます。 |
| DER（識別エンコーディング規則） | 証明書の拡張の種類。 .der 拡張子は、バイナリ DER でエンコードされた証明書に使用されます。 これらのファイルは、 .cer または.crt 拡張子もサポートしている場合があります。 |
| EV (Extended Validation) 証明書 | EV 証明書は、フィッシング攻撃を防ぐように設計された新しい種類の証明書です。 お客様のビジネスと、証明書の注文者の拡張検証が必要です。 |
| 高保証証明書 | ドメイン名の所有権と有効なビジネス登録を確認した後、CA によって高保証証明書が発行されます。 |
| 中間 CA | チェーン証明書に含まれる中間証明書の認証局。 |
| 中間証明書 | 認証局は、ツリー構造の形式で証明書を発行します。 ルート証明書は、ツリーの最上位の証明書です。 証明書とルート証明書の間の証明書は、チェーン証明書または中間証明書と呼ばれます。 |
| 低保証証明書 | 低保証証明書（ドメイン検証証明書とも呼ばれます）は、証明書にドメイン名のみを含みます（ビジネス名/組織名は含みません）。 |
| PEM（プライバシー強化メール） | ASCII(Base64) データを含む、拡張子が.pem の証明書。 このような証明書は、「 - - - - - - - BEGIN CERTIFICATE - - — 」行で始まります。 |
| ルート証明書 | 認証局は、ツリー構造の形式で証明書を発行します。 ルート証明書は、ツリーの最上位の証明書です。 |
| SAN（サブジェクトの別名） | 件名の代替名は、追加のホスト名（サイト、IP アドレス、共通名など） これらは、単一の SSL 証明書の一部として署名する必要があります。 |
| 自己署名証明書 | 信頼された証明機関ではなく、作成者が署名した証明書です。 自己署名証明書は、CA によって署名された証明書と同じレベルの暗号化を有効にできますが、次の 2 つの大きな欠点があります。<ul><li>訪問者の接続がハイジャックされ、攻撃者が送信されたすべてのデータを表示できる（したがって、接続を暗号化する目的を破る）可能性があります</li><li> 信頼された証明書とは異なり、証明書は失効できません。</li></ul> |
| SSL (Secure Sockets Layer) | Web サーバとブラウザとの間に暗号化リンクを確立するための標準的なセキュリティ技術。 |
| ワイルドカード証明書 | ワイルドカード証明書により、1 つのドメイン名（*.adobe.com など）で無制限の数の第 1 レベルサブドメインを保護できます。 |

## 主な手順

1. 証明書署名要求 (CSR) ファイルを要求し、必要な情報（国、都道府県、市区町村、組織名、組織単位名など）を Adobe
1. Adobeで生成された CSR ファイルを検証し、入力した情報がすべて正しいことを確認します。
1. CSR の詳細を使用して、信頼できる証明機関 <!--taking care of asking for using the subjectAltName SSL extension (SAN) if it is for several domain names, and get/purchase the resulting certificate (ideally) in PEM format for Apache server--> によって署名された証明書を生成します。
1. SSL 証明書を検証し、CSR と一致することを確認します。
1. SSL 証明書をインストールするAdobeに指定します。
1. 保護された各サブドメインに対して SSL 証明書が正常にインストールされていることをテストします。
1. SSL 証明書の有効期間を監視します。
1. Adobe Campaignの特定の設定を更新します。

## 詳細なプロセス

### 前提条件

ドメイン名と機能（トラッキング、ミラーページ、Web アプリなど）を をセキュアに設定します。
>[!NOTE]
>
>Adobeは、関連付けるドメイン名と関数の定義に役立ちます。 詳しくは、担当のAdobeカスタマーサクセスマネージャーにお問い合わせください。

### 手順 1 - CSR ファイルの取得

CSR（証明書署名要求）ファイルを取得するには、次の手順に従います。

* [Campaign コントロールパネル](https://experienceleague.adobe.com/docs/control-panel/using/control-panel-home.html?lang=ja) にアクセスできる場合は、[ このページ ](https://experienceleague.adobe.com/docs/control-panel/using/subdomains-and-certificates/renewing-subdomain-certificate.html#subdomains-and-certificates) の手順に従って、Campaign コントロールパネルから CSR ファイルを生成してダウンロードします。

* それ以外の場合は、 https://adminconsole.adobe.com/でサポートチケットを作成し、必要なサブドメインに対してAdobeカスタマーケアから CSR ファイルを取得します。

以下に、従うべきベストプラクティスをいくつか示します。

* デリゲートされたサブドメインごとに 1 つの要求を発行します。
* 複数のサブドメインを 1 つの CSR リクエストに組み合わせることができますが、同じ環境内でのみ可能です。 例えば、Campaign Classicでは、マーケティングサーバー、[ ミッドソーシングサーバー ](https://experienceleague.adobe.com/docs/campaign-classic/using/installing-campaign-classic/install-campaign-on-prem/mid-sourcing-server.html)、[ 実行インスタンス ](https://experienceleague.adobe.com/docs/campaign-classic/using/transactional-messaging/configure-transactional-messaging/configuring-instances.html#execution-instance) の 3 つの異なる環境が使用されます。
* SSL 証明書を更新する前に、新しい CSR を取得する必要があります。 1 年以上前の古い CSR ファイルは使用しないでください。

次の情報を入力する必要があります。

>[!CAUTION]
>
>以下の表に示すすべてのフィールドに入力する必要があります。 そうしないと、CSR リクエストを処理できません。

**情報チームの支援を受けるためのAdobe:**

| 提供する情報 | 値の例 | 注釈 |
|--- |--- |--- |
| クライアント名 | マイカンパニー | 組織の名前。このフィールドは、Adobeがリクエストの追跡に使用します（CSR/SSL 証明書の一部ではありません）。 |
| Adobe Campaign環境 URL | https://client-mid-prod1.campaign.adobe.com | Adobe Campaignインスタンスの URL。 |
| 共通名 [CN] | t.subdomain.customer.com | これは、関連する任意のドメインでもかまいませんが、通常はトラッキングドメインです。 |
| サブジェクトの代替名 [SAN] | t.subdomain.customer.com | SAN としてトラッキングサブドメインを必ず含めてください。 |
| サブジェクトの代替名 [SAN] | m.subdomain.customer.com |
| サブジェクトの代替名 [SAN] | res.subdomain.customer.com |

**IT/SSL 社内チームから提供される情報：**

| 提供する情報 | 値の例 | 注釈 |
|--- |--- |--- |
| 国 [C] | 米国 | これは 2 文字のコードにする必要があります。 [ ここ ](https://www.ssl.com/csrs/country_codes/) から国名の一覧にアクセスします。</br>*注意：英国の場合は、GB（英国ではない）を使用します。* |
| 都道府県名 [ST] | イリノイ | 該当する場合。 値は省略されず、完全な名前にする必要があります。 |
| 市区町村名 [L] | シカゴ |
| 組織名 [O] | ACME |
| 組織単位名 [OU] | IT |

>[!NOTE]
>
>「subdomain.customer.com」をデリゲートされたサブドメインに置き換え、他のサンプル値を適切な値に置き換えます。

### 手順 2 - CSR ファイルの検証

関連情報を使用して要求を送信すると、Adobeが証明書署名要求 (CSR) ファイルを生成して提供します。

結果の CSR ファイルのテキストは、**&quot;—BEGIN CERTIFICATE REQUEST—&quot;** で始まる必要があります。

CSR ファイルをAdobeから受け取ったら、次の手順に従います。

1. CSR ファイルのテキストを、https://www.sslshopper.com/csr-decoder.html、<!--https://www.certlogik.com/decoder/,-->、https://www.entrust.net/ssl-technical/csr-viewer.cfmなどのオンラインデコーダーにコピーして貼り付けます。
または、Linux マシン上で *OpenSSL* コマンドをローカルで使用できます。 詳しくは、[ この外部ページ ](https://www.question-defense.com/2009/09/22/use-openssl-to-verify-the-contents-of-a-csr-before-submitting-for-a-ssl-certificate) を参照してください。
1. すべてのチェックが正常に実行されたことを確認します。
1. 正しいパラメーターとドメイン名が含まれていることを確認します。
1. その他すべてのデータが、リクエストの送信時に指定した詳細と一致することを確認します。

### 手順 3 - SSL 証明書の生成

CSR ファイルを指定したら、CSR ファイルを使用して、適切なドメインの SSL 証明書を購入し、生成する必要があります。

* SSL 証明書：
   * は Apache PEM 形式である必要があります。
   * は 2048 ビット以下にする必要があります。
   * は、有効な CA（証明機関）によって署名されている必要があります。
   * CSR ファイルに記載されているように、すべての SAN(Subject Alternative Name) を含める必要があります。
* 1 つ以上の中間証明書がある場合は、ルート証明書とすべての中間証明書をAdobeに指定する必要があります。
* 証明書の有効期間は任意に設定できますが、Adobeは、証明書の有効期間を十分に長く（例えば 2 年）選択することをお勧めします。

>[!NOTE]
>
>独自の内部ツールまたは CA が提供するポータルを使用して証明書を要求する場合は、CSR 要求で指定したのと同じ詳細を使用して、証明書生成プロセスでの遅延や不一致を避けてください。

### 手順 4 - SSL 証明書の検証

SSL 証明書が生成されたら、SSL 証明書をAdobeに送信する前に検証する必要があります。 これをおこなうには、以下の手順に従います。

1. 証明書の拡張子が.pem であることを確認します。 そうでない場合は、PEM 形式に変換します。 *OpenSSL* を使用して変換を行うことができます。
1. 証明書が **&quot;—BEGIN CERTIFICATE—&quot;** で始まっていることを確認します。
1. 証明書のテキストを、オンラインのデコーダー (https://www.sslshopper.com/certificate-decoder.htmlやhttps://www.entrust.net/ssl-technical/csr-viewer.cfmなど ) にコピーします。
または、Linux マシン上で *OpenSSL* コマンドをローカルで使用できます。 詳しくは、[ この外部ページ ](https://www.shellhacks.com/decode-ssl-certificate/) を参照してください。
1. 共通名、SAN、発行者、有効期間を含む証明書が正しく解決されていることを確認します。
1. SSL 証明書の検証が成功した場合は、[ この Web サイト ](https://www.sslshopper.com/certificate-key-matcher.html) を使用して、証明書が CSR と一致していることを確認します。**CSR と証明書が一致するかどうかを確認し**、該当するフィールドに証明書と CSR を入力します。 一致するはずです。

### 手順 5 - SSL 証明書のインストールを要求する

* [Campaign コントロールパネル](https://experienceleague.adobe.com/docs/control-panel/using/control-panel-home.html) にアクセスできる場合は、[ このページ ](https://experienceleague.adobe.com/docs/control-panel/using/subdomains-and-certificates/renewing-subdomain-certificate.html#installing-ssl-certificate) の手順に従って、Campaign コントロールパネルに証明書をアップロードします。

* それ以外の場合は、 https://adminconsole.adobe.com/から別のサポートチケットを作成して、Adobeに証明書をAdobeサーバーにインストールするよう要求します。

以下を指定する必要があります。

* 証明書ファイル、ルート証明書および（チケットに添付された）中間証明書。できれば Apache PEM 形式です。
* CSR に対して引き上げられた以前のサポートチケットの数。
* CSR チケットに指定されたデータ（共通名、インスタンス URL、状態、市区町村、組織名、組織単位名など）と同じ。

### 手順 6 - SSL 証明書のインストールのテスト

SSL 証明書がインストールされ、Adobeカスタマーケアによって確認されたら、すべての URL に対して正常にインストールされていることを確認します。

SSL インストールチケットを閉じる前に、以下のテストを実行します。 また、[ この節 ](#update-configuration) の説明に従って、特定の設定を更新してください。

ブラウザーで次の URL に移動します（「subdomain.customer.com」をサブドメインに置き換えます）。

* https://subdomain.customer.com/r/test （[web アプリケーション ](https://experienceleague.adobe.com/docs/campaign-classic/using/designing-content/web-applications/about-web-applications.html) サブドメインのみ — 電子メールのサブドメインには適用されません）
* https://t.subdomain.customer.com/r/test
* https://m.subdomain.customer.com/r/test
* https://res.subdomain.customer.com/r/test

成功すると、環境情報が表示され、URL のアドレスバーに接続がセキュリティで保護されていることが示されます。 例えば、Google Chrome で次のメッセージを表示できます。

![](../../help/assets/ssl-google-successful-result.png)

SSL 証明書が正しくインストールされていない場合は、次の警告が表示されます。

![](../../help/assets/ssl-google-unsuccessful-result.png)

### 手順 7 — 証明書の有効期間の確認

ブラウザーで証明書の有効期間を確認できます。 例えば、Google Chrome で、**セキュア** / **証明書** をクリックします。

有効期間を確認するのは、お客様の責任です。 Adobeでは、証明書の有効期限を監視するプロセスを実装することをお勧めします。 [ この記事 ](https://www.thesslstore.com/blog/what-happens-when-your-ssl-certificate-expires/) で、SSL 証明書の有効期限が切れた場合の動作を確認してください。

* サポートチケットを作成して、証明書の有効期限の少なくとも 2 週間前に更新済み証明書を要求します。 CSR の詳細が変更されていない限り、追加の CSR をリクエストする必要はありません。

* [Campaign コントロールパネル](https://experienceleague.adobe.com/docs/control-panel/using/control-panel-home.html) にアクセスでき、環境がAWS環境のAdobeによってホストされている場合は、Campaign コントロールパネルを使用して、証明書の有効期限が切れる前に証明書を更新できます。 詳しくは、[この節](https://experienceleague.adobe.com/docs/control-panel/using/subdomains-and-certificates/monitoring-ssl-certificates.html#monitoring-certificates)を参照してください。

### 手順 8 — 特定の設定を更新する {#update-configuration}

要求された SSL 証明書が正しくインストールされると確信できたら、Adobe Campaignのすべての参照を HTTP から HTTPS に更新できます。

>[!NOTE]
>
>Campaign Classicの場合、更新する URL は主に [ デプロイウィザード ](https://experienceleague.adobe.com/docs/campaign-classic/using/installing-campaign-classic/initial-configuration/deploying-an-instance.html#deployment-wizard) と [ 外部アカウント ](https://experienceleague.adobe.com/docs/campaign-classic/using/installing-campaign-classic/accessing-external-database/external-accounts.html)（トラッキング、ミラーページ、パブリックリソースドメイン）にあります。 Campaign Standardについては、[ ブランディング設定 ](https://experienceleague.adobe.com/docs/campaign-standard/using/administrating/application-settings/branding.html#about-brand-identity) を参照してください。

設定が更新されると、HTTP ではなく HTTPS の URL を使用して新しい電子メールが送信されます。 URL がセキュリティで保護されたことを確認するには、次のテストをすばやく実行できます。

* Adobe Campaignから画像をアップロードします。 画像がアップロードされたら、返される URL は HTTPS にする必要があります。
* ミラーページのリンク、一部の画像、テキスト、購読解除リンクを含むテスト用 E メール配信を作成します。 外部の電子メール ID（Gmail アドレスなど）に電子メールを送信します。 電子メールを受け取ったら、電子メールを開き、SSL 証明書の警告やエラーなしで、電子メール内のすべてのリンクが（HTTP ではなく）HTTPS 形式で正しく開いていることを確認します。

## 製品固有のリソース

**Campaign Classic**

* [Campaign コントロールパネル:SSL 証明書の追加（チュートリアル）](https://experienceleague.adobe.com/docs/campaign-classic-learn/control-panel/subdomains-and-certificates/adding-ssl-certificates.html)  - SSL 証明書を追加してサブドメインを保護する方法を説明します。

**Campaign Standard**

* [Campaign コントロールパネル:SSL 証明書の追加（チュートリアル）](https://experienceleague.adobe.com/docs/campaign-standard-learn/control-panel/subdomains-and-certificates/adding-ssl-certificates.html)  - SSL 証明書を追加してサブドメインを保護する方法を説明します。
