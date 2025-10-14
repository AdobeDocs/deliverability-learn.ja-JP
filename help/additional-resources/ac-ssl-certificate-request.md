---
title: SSL 証明書要求プロセス
description: Adobeにデリゲートしたサブドメインに SSL 証明書をインストールする方法を説明します。
topics: Deliverability
doc-type: article
activity: understand
team: ACS
exl-id: 8a78abd3-afba-49a7-a2ae-8b2c75326749
source-git-commit: 57016f89df54d5c74755a6a108a92db45153ec18
workflow-type: tm+mt
source-wordcount: '2124'
ht-degree: 1%

---

# SSL 証明書要求プロセス

メールを送信するためにドメインをAdobeにデリゲートすると（[&#x200B; ドメイン名の設定 &#x200B;](/help/additional-resources/ac-domain-name-setup.md) を参照）、Adobeは特定の機能に対して特定のサブドメインを作成して使用します。

例えば、メールを送信するために *email.example.com* をAdobeにデリゲートした場合、Adobeは次のようなサブドメインを作成します。
* *t.email.example.com* - トラッキングリンク用
* *m.email.example.com* - ミラーページ用
* *res.email.example.com* - ホストされているリソース（画像など）用

**これらのドメインは SSL （HTTPS）で保護** することをお勧めします。 実際、保護されていないリンク（HTTP）は傍受に対して脆弱で、最新のブラウザーでは警告がフラグアップされます。

これらのサブドメインに SSL 証明書をインストールするには、CSR ファイルを要求してから、インストールまたは更新のAdobe用の SSL 証明書を購入する必要があります。

>[!CAUTION]
>
>SSL 証明書をインストールする前に、[&#x200B; このページ &#x200B;](https://experienceleague.adobe.com/docs/control-panel/using/subdomains-and-certificates/renewing-subdomain-certificate.html?lang=ja#installing-ssl-certificate) に記載されている前提条件を認識していることを確認してください。
>
>Adobeでは、最大 2048 ビットの証明書のみをサポートしています。 4096 ビット証明書はまだサポートされていません。

## 用語集

| 用語 | 説明 |
|--- |--- |
| CA （証明機関） | DigiCert、Symantec などの ID を検証した後、組織または個人にデジタル証明書を発行する SSL 証明書プロバイダー。<ul><li>信頼される CA は、通常、ルート証明書を発行するサードパーティ CA と見なされます。</li><li>証明書を使用している同じ組織または会社によって証明書が署名されている場合は、自己署名証明書などの SSL 証明書である場合でも、信頼されていない CA として分類されます。</li></ul> |
| チェーン証明書 | ルート証明書と 1 つ以上の中間証明書を含む証明書は、チェーン （またはチェーン）証明書と呼ばれます。 |
| CSR （証明書署名要求） | SSL 証明書の申請時に認証局に提供される、エンコードされたテキストのブロック。 通常、証明書がインストールされているサーバーで生成されます。 |
| DER （Distinguished Encoding Rules） | 証明書の拡張タイプ。 .der 拡張子は、バイナリ DER でエンコードされた証明書に使用されます。 これらのファイルは、.cer または.crt 拡張子もサポートする場合があります。 |
| EV （拡張検証）証明書 | EV 証明書は、フィッシング攻撃を防ぐための新しい種類の証明書です。 ビジネスおよび証明書を注文する人物の詳細な検証が必要です。 |
| 高保証証明書 | 高保証証明書は、ドメイン名の所有権と有効なビジネス登録を確認した後、CA によって発行されます。 |
| 中間 CA | チェーン証明書に含まれる中間証明書の証明機関。 |
| 中間証明書 | 認証局は、ツリー構造の形式で証明書を発行します。 ルート証明書は、ツリーの最上位の証明書です。 証明書とルート証明書の間の証明書は、チェーン証明書または中間証明書と呼ばれます。 |
| 低保証証明書 | 低アシュランス証明書（ドメイン検証済み証明書とも呼ばれます）には、証明書のドメイン名のみが含まれます（ビジネス名や組織名は含まれません）。 |
| PEM （プライバシー強化メール） | ASCII （Base64）データを含む.pem 拡張子を持つ証明書。 このような証明書は、「- - - - – 証明書の開始 – - - -」行で始まります。 |
| ルート証明書 | 認証局は、ツリー構造の形式で証明書を発行します。 ルート証明書は、ツリーの最上位の証明書です。 |
| SAN （サブジェクトの別名） | サブジェクトの代替名は、追加のホスト名（サイト、IP アドレス、共通名など）です 単一の SSL 証明書の一部として署名する必要があります。 |
| 自己署名証明書 | 信頼された証明機関ではなく、その作成者によって署名された証明書。 自己署名証明書は、CA によって署名された証明書と同じレベルの暗号化を有効にすることができますが、大きな欠点が 2 つあります。<ul><li>訪問者の接続がハイジャックされ、攻撃者は送信されたすべてのデータを表示できる可能性があります（したがって、接続を暗号化する目的を台無しにする）</li><li> 信頼された証明書のように証明書を取り消すことはできません。</li></ul> |
| SSL （Secure Sockets Layer） | ウェブサーバとブラウザの間に暗号化されたリンクを確立するための標準的なセキュリティ技術。 |
| ワイルドカード証明書 | ワイルドカード証明書を使用すると、*.adobe.comなど、1 つのドメイン名に対して無制限の数の第 1 レベル サブドメインを保護できます。 |

## 主な手順

1. 証明書署名要求（CSR）ファイルを要求し、必要な情報（国、都道府県、市区町村、組織名、組織単位名など）を提供します。 をAdobeにします。
1. Adobeで生成された CSR ファイルを検証し、指定したすべての情報が正しいことを確認します。
1. CSR の詳細を使用して、信頼された証明機関 <!--taking care of asking for using the subjectAltName SSL extension (SAN) if it is for several domain names, and get/purchase the resulting certificate (ideally) in PEM format for Apache server--> によって署名された証明書を生成します。
1. SSL 証明書を検証し、CSR と一致することを確認します。
1. Adobeに SSL 証明書を提供し、インストールします。
1. セキュリティで保護された各サブドメインに対して SSL 証明書が正常にインストールされていることをテストします。
1. SSL 証明書の有効期間を監視します。
1. Adobe Campaignで特定の設定を更新します。

## 詳細なプロセス

### 前提条件

ドメイン名と関数（トラッキング、ミラーページ、web アプリなど）を識別する必要があります。 を保護します。
>[!NOTE]
>
>Adobeは、関連するドメイン名と関数を定義するのに役立ちます。 詳しくは、Adobeアカウントチームにお問い合わせください。

### 手順 1 - CSR ファイルの取得

CSR （証明書署名要求）ファイルを取得するには、次の手順に従います。

* [Campaign コントロールパネル](https://experienceleague.adobe.com/docs/control-panel/using/control-panel-home.html?lang=ja) にアクセスできる場合は、[&#x200B; このページ &#x200B;](https://experienceleague.adobe.com/docs/control-panel/using/subdomains-and-certificates/renewing-subdomain-certificate.html?lang=ja#subdomains-and-certificates) の手順に従って、CSR ファイルを生成し、Campaign コントロールパネルからダウンロードします。

* それ以外の場合は、https://adminconsole.adobe.com/でサポートチケットを作成し、必要なサブドメインの CSR ファイルをAdobeカスタマーケアから取得します。

従うべきベストプラクティスをいくつか示します。

* デリゲートされたサブドメインごとに 1 つのリクエストを発生させます。
* 複数のサブドメインを 1 つの CSR リクエストに組み合わせることができますが、それは同じ環境内だけです。 例えば、Campaign Classicでは、マーケティングサーバー、[&#x200B; ミッドソーシングサーバー &#x200B;](https://experienceleague.adobe.com/docs/campaign-classic/using/installing-campaign-classic/install-campaign-on-prem/mid-sourcing-server.html?lang=ja) および [&#x200B; 実行インスタンス &#x200B;](https://experienceleague.adobe.com/docs/campaign-classic/using/transactional-messaging/configure-transactional-messaging/configuring-instances.html?lang=ja#execution-instance) は 3 つの異なる環境となります。
* SSL 証明書を更新するには、新しい CSR を取得する必要があります。 1 年以上前の古い CSR ファイルは使用しないでください。

次の情報を入力する必要があります。

>[!CAUTION]
>
>以下の表に示されているすべてのフィールドに入力する必要があります。 追加されていない場合、CSR リクエストを処理できません。

**Adobeチームの支援に関する情報提供資料：**

| 提供する情報 | 値の例 | 注意 |
|--- |--- |--- |
| クライアント名 | 私の会社 | 組織の名前。 このフィールドは、Adobeがリクエストをトラッキングするために使用します（CSR/SSL 証明書には含まれません）。 |
| Adobe Campaign環境 URL | https://client-mid-prod1.campaign.adobe.com | Adobe Campaign インスタンスの URL。 |
| 共通名 [CN] | t.subdomain.customer.com | 関連する任意のドメインを指定できますが、通常はトラッキングドメインを指定します。 |
| サブジェクトの別名 [SAN] | t.subdomain.customer.com | トラッキングサブドメインを SAN として必ず含めてください。 |
| サブジェクトの別名 [SAN] | m.subdomain.customer.com |
| サブジェクトの別名 [SAN] | res.subdomain.customer.com |

**IT/SSL 社内チームから提供される情報：**

| 提供する情報 | 値の例 | 注意 |
|--- |--- |--- |
| 国 [C] | US | これは 2 文字のコードでなければなりません。 国全体のリスト [&#x200B; こちら &#x200B;](https://www.ssl.com/csrs/country_codes/) にアクセスします。</br>*メモ：英国の場合は、（英国ではなく） GB を使用します。* |
| 都道府県 [ST] | イリノイ | 該当する場合。 値は、省略せずにフルネームにする必要があります。 |
| 市区町村名/地域名 [L] | シカゴ |
| 組織名 [O] | ACME |
| 組織単位名 [OU] | 0.45111884 |

>[!NOTE]
>
>「subdomain.customer.com」をデリゲートされたサブドメインに、他の例の値を適切な値に置き換えます。

### 手順 2 - CSR ファイルを検証

関連情報と共にリクエストを送信すると、Adobeがを生成し、証明書署名リクエスト（CSR）ファイルを提供します。

結果の CSR ファイルのテキストは、「– ----BEGIN CERTIFICATE REQUEST-----**&#x200B;** で始める必要があります。

Adobeから CSR ファイルを受け取ったら、次の手順に従います。

1. CSR ファイルのテキストをコピーして、https://www.sslshopper.com/csr-decoder.html、<!--https://www.certlogik.com/decoder/,-->、https://www.entrust.net/ssl-technical/csr-viewer.cfmなどのオンラインデコーダに貼り付けます。
または、Linux マシン上でローカルに *OpenSSL* コマンドを使用できます。
1. すべてのチェックが正常に完了していることを確認します。
1. 正しいパラメーターとドメイン名が含まれていることを確認します。
1. 他のすべてのデータがリクエストの送信時に指定した詳細と一致していることを確認します。

### 手順 3 - SSL 証明書の生成

CSR ファイルを指定したら、CSR ファイルを使用して、適切なドメインの SSL 証明書を購入して生成する必要があります。

* SSL 証明書：
   * Apache PEM 形式である必要があります。
   * は 2048 ビット以下にする必要があります。
   * 有効な CA （証明機関）によって署名されている必要があります。
   * csr ファイルに記載されているすべての SAN （サブジェクト代替名）を含める必要があります。
* 1 つ以上の中間証明書がある場合、ルート証明書とすべての中間証明書をAdobeに提供する必要があります。
* 証明書の有効期間は任意に設定できますが、Adobeでは十分な長さ（例えば 2 年）を選択することをお勧めします。

>[!NOTE]
>
>独自の内部ツールまたは CA が提供するポータルを使用して証明書を要求する場合は、証明書の生成プロセスで遅延や不一致が発生しないように、CSR 要求で提供される詳細と同じ詳細を使用してください。

### 手順 4 - SSL 証明書を検証

SSL 証明書を生成したら、Adobeに送信する前に検証する必要があります。 これを行うには、以下の手順に従います。

1. 証明書に.pem 拡張子が付いていることを確認します。 そうでない場合は、PEM 形式に変換します。 *OpenSSL* を使用して変換を行うことができます。
1. 証明書が **&quot;-----BEGIN CERTIFICATE-----&quot;** で始まっていることを確認します。
1. 証明書テキストをhttps://www.sslshopper.com/certificate-decoder.htmlやhttps://www.entrust.net/ssl-technical/csr-viewer.cfmなどのオンラインデコーダにコピーします。
または、Linux マシン上でローカルに *OpenSSL* コマンドを使用できます。 詳しくは、[&#x200B; この外部ページ &#x200B;](https://www.shellhacks.com/decode-ssl-certificate/) を参照してください。
1. 共通名、SAN、発行者、有効期間など、証明書が正しく解決されていることを確認します。
1. SSL 証明書の検証に成功した場合は、証明書が CSR と一致することを確認します [&#x200B; この web サイト &#x200B;](https://www.sslshopper.com/certificate-key-matcher.html):「**CSR と証明書が一致するかどうかを確認**」を選択し、対応するフィールドに証明書と CSR を入力します。 一致する必要があります。

### 手順 5 - SSL 証明書のインストールのリクエスト

* [Campaign コントロールパネル](https://experienceleague.adobe.com/docs/control-panel/using/control-panel-home.html?lang=ja) にアクセスできる場合は、[&#x200B; このページ &#x200B;](https://experienceleague.adobe.com/docs/control-panel/using/subdomains-and-certificates/renewing-subdomain-certificate.html?lang=ja#installing-ssl-certificate) の手順に従って、証明書をCampaign コントロールパネルにアップロードしてください。

* それ以外の場合は、https://adminconsole.adobe.com/で別のサポートチケットを作成し、Adobeをリクエストして、Adobeサーバーに証明書をインストールします。

以下を指定する必要があります。

* 証明書ファイル、ルート証明書および中間証明書（チケットに添付）（できれば Apache PEM 形式）。
* CSR に対して発生した以前のサポートチケットの番号。
* CSR チケットに提供されたのと同じデータ（共通名、インスタンス URL、状態、市区町村/地域、組織名、組織単位名など）。

### 手順 6 - SSL 証明書のインストールのテスト

SSL 証明書をインストールしてAdobeカスタマーケアで確認したら、すべての URL に正常にインストールされていることを確認します。

SSL インストールチケットを閉じる前に、以下のテストを実行してください。 また、[&#x200B; この節 &#x200B;](#update-configuration) の指示に従って、特定の設定を必ず更新してください。

ブラウザーで次の URL に移動します（「subdomain.customer.com」をサブドメインに置き換えます）。

* https://subdomain.customer.com/r/test（[web アプリケーション &#x200B;](https://experienceleague.adobe.com/docs/campaign-classic/using/designing-content/web-applications/about-web-applications.html?lang=ja) サブドメインのみ – メールサブドメインには適用されません）
* https://t.subdomain.customer.com/r/test
* https://m.subdomain.customer.com/r/test
* https://res.subdomain.customer.com/r/test

正常な結果では環境情報が提供され、URL のアドレスバーは接続が安全であることを示します。 例えば、Google Chromeには次のメッセージが表示されます。

![](../../help/assets/ssl-google-successful-result.png)

SSL 証明書が正しくインストールされていない場合は、次の警告が表示されます。

![](../../help/assets/ssl-google-unsuccessful-result.png)

### 手順 7 – 証明書の有効期間の確認

ブラウザーで証明書の有効期間を確認できます。 例えば、Google Chromeでは、**セキュア**/**証明書** をクリックします。

有効期間を確認するのはユーザーの責任です。 Adobeでは、証明書の有効期限を監視するプロセスを実装することをお勧めします。 SSL 証明書の有効期限が切れるとどうなるかについて詳しくは、[&#x200B; この記事 &#x200B;](https://www.thesslstore.com/blog/what-happens-when-your-ssl-certificate-expires/) を参照してください。

* サポートチケットを作成して、証明書の有効期限の 2 週間前までに、更新された証明書をリクエストします CSR の詳細が変更されていない限り、追加の CSR をリクエストする必要はありません。

* [&#x200B; 環境 &#x200B;](https://experienceleague.adobe.com/docs/control-panel/using/control-panel-home.html?lang=ja) にアクセスでき、Campaign コントロールパネルがAdobeによってAWS環境でホストされている場合は、Campaign コントロールパネルを使用して有効期限が切れる前に証明書を更新できます。 詳しくは、[この節](https://experienceleague.adobe.com/docs/control-panel/using/subdomains-and-certificates/monitoring-ssl-certificates.html?lang=ja#monitoring-certificates)を参照してください。

### 手順 8 – 特定の設定の更新 {#update-configuration}

要求された SSL 証明書が正しくインストールされていることを確認したら、Adobe Campaign内のすべての参照を HTTP から HTTPS に更新できます。

>[!NOTE]
>
>Campaign Classicについては、更新する URL は主に [&#x200B; デプロイメントウィザード &#x200B;](https://experienceleague.adobe.com/docs/campaign-classic/using/installing-campaign-classic/initial-configuration/deploying-an-instance.html?lang=ja#deployment-wizard) と [&#x200B; 外部アカウント &#x200B;](https://experienceleague.adobe.com/docs/campaign-classic/using/installing-campaign-classic/accessing-external-database/external-accounts.html?lang=ja) （トラッキング、ミラーページ、パブリックリソースドメイン）にあります。 Campaign Standardについては、[&#x200B; ブランディング設定 &#x200B;](https://experienceleague.adobe.com/docs/campaign-standard/using/administrating/application-settings/branding.html?lang=ja#about-brand-identity) を参照してください。

設定が更新されると、新しいメールは HTTP ではなく HTTPS URL で送信されます。 URL が保護されていることを確認するには、次のテストをすばやく実行できます。

* Adobe Campaignから画像をアップロードします。 画像がアップロードされると、返される URL は HTTPS になります。
* ミラーページのリンク、一部の画像、テキスト、購読解除リンクなどのテストメール配信を作成します。 外部のメール ID （Gmail アドレスなど）にメールを送信します。 受信したら、メールを開き、メール内のすべてのリンクが HTTPS フォーム（HTTP ではない）で正しく開いていることを、SSL 証明書の警告やエラーがないことを確認します。

## 製品固有のリソース

**Campaign Classic**

* [Campaign コントロールパネル: SSL 証明書の追加（チュートリアル） &#x200B;](https://experienceleague.adobe.com/docs/campaign-classic-learn/control-panel/subdomains-and-certificates/adding-ssl-certificates.html?lang=ja) - SSL 証明書を追加してサブドメインを保護する方法を説明します。

**Campaign Standard**

* [Campaign コントロールパネル: SSL 証明書の追加（チュートリアル） &#x200B;](https://experienceleague.adobe.com/docs/campaign-standard-learn/control-panel/subdomains-and-certificates/adding-ssl-certificates.html?lang=ja) - SSL 証明書を追加してサブドメインを保護する方法を説明します。
