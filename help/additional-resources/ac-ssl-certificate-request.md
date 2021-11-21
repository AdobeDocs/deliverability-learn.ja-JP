---
title: SSL 証明書要求プロセス
description: Delegate にデリゲートしたサブドメインに SSL 証明書をインストールする方法をAdobeします。
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

E メール送信用にドメインをAdobeにデリゲートしたら ( [ドメイン名の設定](/help/additional-resources/ac-domain-name-setup.md)) の場合、Adobeは、特定の関数に対して特定のサブドメインを作成して使用します。

例えば、 *email.example.com* E メール送信のAdobeに対して、Adobeは次のようなサブドメインを作成します。
* *t.email.example.com*  — トラッキングリンク用
* *m.email.example.com*  — ミラーページの場合
* *res.email.example.com*  — ホストされているリソース（画像など）の場合

次の操作をお勧めします。 **SSL(HTTPS) を介してこれらのドメインを保護します。**. 実際、保護されていないリンク (HTTP) は傍受に対して脆弱で、最新のブラウザーでは警告がフラグアップされます。

これらのサブドメインに SSL 証明書をインストールするには、CSR ファイルをリクエストし、Adobeがインストールまたは更新するための SSL 証明書を購入する必要があります。

>[!CAUTION]
>
>SSL 証明書をインストールする前に、 [このページ](https://experienceleague.adobe.com/docs/control-panel/using/subdomains-and-certificates/renewing-subdomain-certificate.html?lang=ja#installing-ssl-certificate).
>
>Adobeは、最大 2048 ビットの証明書のみをサポートします。 4096 ビット証明書は、まだサポートされていません。

## 用語集

| 用語 | 説明 |
|--- |--- |
| CA （認証局） | DigiCert、Symantec など、組織または個人の ID を確認した後に電子証明書を発行する SSL 証明書プロバイダー。<ul><li>信頼された CA は、通常、ルート証明書を発行するサードパーティ CA と見なされます。</li><li>証明書を使用している同じ組織または会社が証明書に署名している場合、証明書が自己署名証明書などの SSL 証明書であっても、信頼されていない CA と分類されます。</li></ul> |
| チェーン証明書 | ルート証明書と 1 つ以上の中間証明書を含む証明書は、チェーン（またはチェーン）証明書と呼ばれます。 |
| CSR （証明書署名要求） | SSL 証明書の申請時に証明機関に提供される、エンコードされたテキストのブロックです。 通常、証明書がインストールされているサーバーで生成されます。 |
| DER(Distinguished Encoding Rules) | 証明書拡張のタイプ。 .der 拡張子は、バイナリ DER でエンコードされた証明書に使用されます。 これらのファイルでは、 .cer または.crt 拡張子もサポートされている場合があります。 |
| EV（拡張検証）証明書 | EV 証明書は、フィッシング攻撃を防ぐように設計された新しい種類の証明書です。 お客様のビジネスと、証明書を注文する人の拡張検証が必要です。 |
| 高保証証明書 | ドメイン名の所有権と有効なビジネス登録を確認した後、CA が高保証証明書を発行します。 |
| 中間 CA | チェーン証明書に含まれる中間証明書の証明機関。 |
| 中間証明書 | 証明機関は、ツリー構造の形式で証明書を発行します。 ルート証明書は、ツリーの最上位の証明書です。 証明書とルート証明書の間の証明書は、チェーンまたは中間証明書と呼ばれます。 |
| 低アシュランス証明書 | 低保証証明書（ドメイン検証済み証明書とも呼ばれます）には、証明書のドメイン名のみが含まれます（ビジネス名や組織名は含まれません）。 |
| PEM （プライバシー拡張メール） | ASCII(Base64) データを含む.pem 拡張子の証明書。 このような証明書は、「 - - - - - - BEGIN CERTIFICATE - - - — 」行で始まります。 |
| ルート証明書 | 証明機関は、ツリー構造の形式で証明書を発行します。 ルート証明書は、ツリーの最上位の証明書です。 |
| SAN （件名の代替名） | 件名の代替名は、追加のホスト名（サイト、IP アドレス、共通名など） これは、単一の SSL 証明書の一部として署名する必要があります。 |
| 自己署名証明書 | 信頼された証明機関ではなく、作成者が署名した証明書です。 自己署名証明書は、CA によって署名された証明書と同じレベルの暗号化を有効にすることができますが、次の 2 つの大きな欠点があります。<ul><li>訪問者の接続がハイジャックされ、攻撃者が送信されたすべてのデータを表示できるようになる（その結果、接続を暗号化する目的がなくなる）可能性があります</li><li> 信頼された証明書とは異なり、証明書を失効させることはできません。</li></ul> |
| SSL (Secure Sockets Layer) | Web サーバとブラウザとの間に暗号化されたリンクを確立するための標準的なセキュリティテクノロジ。 |
| ワイルドカード証明書 | ワイルドカード証明書により、1 つのドメイン名（*.adobe.com など）で任意の数の第 1 レベルサブドメインを保護できます。 |

## 主な手順

1. 証明書署名要求 (CSR) ファイルを要求し、必要な情報（国、都道府県、市区町村、組織名、組織単位名など）を Adobeに
1. Adobeで生成された CSR ファイルを検証し、指定したすべての情報が正しいことを確認します。
1. CSR の詳細を使用して、信頼された証明機関によって署名された証明書を生成します<!--taking care of asking for using the subjectAltName SSL extension (SAN) if it is for several domain names, and get/purchase the resulting certificate (ideally) in PEM format for Apache server-->.
1. SSL 証明書を検証し、CSR と一致することを確認します。
1. SSL 証明書をインストールするAdobeに、SSL 証明書を提供します。
1. 保護された各サブドメインに対して SSL 証明書が正常にインストールされていることをテストします。
1. SSL 証明書の有効期間を監視します。
1. Adobe Campaignの特定の設定を更新します。

## 詳細なプロセス

### 前提条件

ドメイン名と機能（トラッキング、ミラーページ、Web アプリなど）を を保護します。
>[!NOTE]
>
>Adobeは、関連付けるドメイン名や関数を定義する際に役立ちます。 詳しくは、担当のAdobeカスタマーサクセスマネージャーにお問い合わせください。

### 手順 1 - CSR ファイルを取得する

CSR（証明書署名要求）ファイルを取得するには、次の手順に従います。

* 次にアクセスできる [Campaign コントロールパネル](https://experienceleague.adobe.com/docs/control-panel/using/control-panel-home.html?lang=ja)を使用する場合は、 [このページ](https://experienceleague.adobe.com/docs/control-panel/using/subdomains-and-certificates/renewing-subdomain-certificate.html#subdomains-and-certificates) をクリックして、CSR ファイルをCampaign コントロールパネルから生成しダウンロードします。

* それ以外の場合は、 https://adminconsole.adobe.com/でサポートチケットを作成し、必要なサブドメインに対して、Adobeカスタマーケアから CSR ファイルを取得します。

以下に、従うべきベストプラクティスをいくつか示します。

* デリゲートされたサブドメインごとに 1 つのリクエストを発行します。
* 複数のサブドメインを 1 つの CSR リクエストに組み合わせることができますが、同じ環境内でのみ可能です。 例えば、Campaign Classicの場合、マーケティングサーバーの場合、 [ミッドソーシングサーバー](https://experienceleague.adobe.com/docs/campaign-classic/using/installing-campaign-classic/install-campaign-on-prem/mid-sourcing-server.html)、および [実行インスタンス](https://experienceleague.adobe.com/docs/campaign-classic/using/transactional-messaging/configure-transactional-messaging/configuring-instances.html#execution-instance) は、3 つの異なる環境です。
* SSL 証明書を更新する前に、新しい CSR を取得する必要があります。 1 年以上前の古い CSR ファイルを使用しないでください。

次の情報を入力する必要があります。

>[!CAUTION]
>
>以下の表に示すすべてのフィールドに入力する必要があります。 そうしないと、CSR リクエストを処理できません。

**情報チームの支援を受けるためのAdobe:**

| 提供する情報 | 値の例 | 注釈 |
|--- |--- |--- |
| クライアント名 | My Company Inc. | 組織の名前。このフィールドは、Adobeがリクエストの追跡に使用します（CSR/SSL 証明書には含まれません）。 |
| Adobe Campaign環境 URL | https://client-mid-prod1.campaign.adobe.com | Adobe Campaignインスタンス URL。 |
| 共通名 [CN] | t.subdomain.customer.com | 関連するドメインのいずれでもかまいませんが、通常はトラッキングドメインです。 |
| 件名の代替名 [SAN] | t.subdomain.customer.com | トラッキングサブドメインを SAN として含めてください。 |
| 件名の代替名 [SAN] | m.subdomain.customer.com |
| 件名の代替名 [SAN] | res.subdomain.customer.com |

**IT/SSL 内部チームから提供される情報：**

| 提供する情報 | 値の例 | 注釈 |
|--- |--- |--- |
| 国 [C] | US | これは 2 文字のコードにする必要があります。 国の完全なリストにアクセス [ここ](https://www.ssl.com/csrs/country_codes/).</br>*注意：英国の場合は、GB（英国ではなく）を使用します。* |
| 都道府県名 [ST] | イリノイ | 該当する場合。 値は省略されず、完全な名前にする必要があります。 |
| 市区町村名 [L] | シカゴ |
| 組織名 [O] | ACME |
| 組織単位名 [OU] | IT |

>[!NOTE]
>
>「subdomain.customer.com」をデリゲートされたサブドメインに置き換え、他の例の値を適切な値に置き換えます。

### 手順 2 - CSR ファイルの検証

関連情報を指定して要求を送信すると、Adobeが証明書署名要求 (CSR) ファイルを生成して提供します。

結果の CSR ファイルのテキストはで始まる必要があります。 **&quot; — 証明書の要求を開始します —&quot;**.

CSR ファイルをAdobeから受け取ったら、次の手順に従います。

1. CSR ファイルテキストを、https://www.sslshopper.com/csr-decoder.htmlのようなオンラインデコーダーにコピー&amp;ペーストします。 <!--https://www.certlogik.com/decoder/,--> またはhttps://www.entrust.net/ssl-technical/csr-viewer.cfm。
または、 *OpenSSL* コマンドをローカルに Linux マシン上に置く。 詳しくは、 [この外部ページ](https://www.question-defense.com/2009/09/22/use-openssl-to-verify-the-contents-of-a-csr-before-submitting-for-a-ssl-certificate).
1. すべてのチェックが正常に行われたことを確認します。
1. 正しいパラメーターとドメイン名が含まれていることを確認します。
1. その他すべてのデータが、リクエストの送信時に指定した詳細と一致することを確認します。

### 手順 3 - SSL 証明書の生成

CSR ファイルを指定したら、CSR ファイルを使用して、適切なドメインの SSL 証明書を購入し、生成する必要があります。

* SSL 証明書：
   * は Apache PEM 形式である必要があります。
   * は、2048 ビット以下にする必要があります。
   * は、有効な CA （証明機関）によって署名されている必要があります。
   * CSR ファイルで説明されているように、すべての SAN（サブジェクトの代替名）を含める必要があります。
* 1 つ以上の中間証明書がある場合は、ルート証明書とすべての中間証明書をAdobeに指定する必要があります。
* 任意の証明書の有効期間を設定できますが、Adobeは、証明書の有効期間を十分に長く（例えば 2 年）選択することをお勧めします。

>[!NOTE]
>
>独自の内部ツールまたは CA が提供するポータルを使用して証明書を要求する場合は、証明書生成プロセスで遅延や不一致が生じないよう、CSR 要求で指定したのと同じ詳細を必ず使用してください。

### 手順 4 - SSL 証明書を検証する

SSL 証明書が生成されたら、Adobeに送信する前に検証する必要があります。 これをおこなうには、以下の手順に従います。

1. 証明書の拡張子が.pem であることを確認します。 該当しない場合は、PEM 形式に変換します。 変換処理を実行するには、 *OpenSSL*.
1. 証明書が次の語句で始まっていることを確認します。 **「 — 証明書を開始 — 」**.
1. 証明書テキストをオンラインデコーダー (https://www.sslshopper.com/certificate-decoder.htmlやhttps://www.entrust.net/ssl-technical/csr-viewer.cfmなど ) にコピーします。
または、 *OpenSSL* コマンドをローカルに Linux マシン上に置く。 詳しくは、 [この外部ページ](https://www.shellhacks.com/decode-ssl-certificate/).
1. 共通名、SAN、発行者、有効期間を含む証明書が正しく解決されていることを確認します。
1. SSL 証明書の検証が成功した場合は、次を使用して、証明書が CSR と一致することを確認します。 [このウェブサイト](https://www.sslshopper.com/certificate-key-matcher.html):選択 **CSR と証明書が一致するかどうかを確認します**&#x200B;をクリックし、該当するフィールドに証明書と CSR を入力します。 一致する必要があります。

### 手順 5 - SSL 証明書のインストールを要求する

* 次にアクセスできる [Campaign コントロールパネル](https://experienceleague.adobe.com/docs/control-panel/using/control-panel-home.html)を使用する場合は、 [このページ](https://experienceleague.adobe.com/docs/control-panel/using/subdomains-and-certificates/renewing-subdomain-certificate.html#installing-ssl-certificate) 証明書をCampaign コントロールパネルにアップロード

* それ以外の場合は、https://adminconsole.adobe.com/から別のサポートチケットを作成し、Adobeに証明書をAdobeサーバーにインストールするよう要求します。

以下を指定する必要があります。

* 証明書ファイル、ルート証明書および（チケットに添付されている）中間証明書。できれば Apache PEM 形式です。
* CSR に対して引き上げた以前のサポートチケットの数。
* CSR チケットに指定されたデータと同じもの（共通名、インスタンス URL、都道府県、市区町村、組織名、組織単位名など）。

### 手順 6 - SSL 証明書のインストールのテスト

SSL 証明書がインストールされ、Adobeカスタマーケアによって確認されたら、すべての URL に対して正常にインストールされていることを確認します。

SSL インストールチケットを閉じる前に、以下のテストを実行します。 また、特定の設定を必ず更新してください ( [この節](#update-configuration).

ブラウザーで次の URL に移動します（「subdomain.customer.com」をサブドメインに置き換えます）。

* https://subdomain.customer.com/r/test [web アプリケーション](https://experienceleague.adobe.com/docs/campaign-classic/using/designing-content/web-applications/about-web-applications.html) サブドメインのみ — 電子メールのサブドメインには適用されません。
* https://t.subdomain.customer.com/r/test
* https://m.subdomain.customer.com/r/test
* https://res.subdomain.customer.com/r/test

成功した結果、環境情報が表示され、URL のアドレスバーは接続がセキュリティで保護されていることを示します。 例えば、Google Chrome では次のメッセージを表示できます。

![](../../help/assets/ssl-google-successful-result.png)

SSL 証明書が正しくインストールされていない場合は、次の警告が表示されます。

![](../../help/assets/ssl-google-unsuccessful-result.png)

### 手順 7 — 証明書の有効期間の確認

ブラウザーで証明書の有効期間を確認できます。 例えば、Google Chrome で、 **セキュア** > **証明書**.

有効期間を確認するのは、お客様の責任です。 Adobeでは、証明書の有効期限を監視するプロセスを実装することをお勧めします。 SSL 証明書の有効期限が次の期間に切れた場合の影響の詳細を説明します [この記事](https://www.thesslstore.com/blog/what-happens-when-your-ssl-certificate-expires/).

* サポートチケットを作成して、証明書の有効期限の 2 週間前以降に更新された証明書をリクエストします。 CSR の詳細が変更されていない限り、追加の CSR をリクエストする必要はありません。

* 次にアクセスできる [Campaign コントロールパネル](https://experienceleague.adobe.com/docs/control-panel/using/control-panel-home.html)AWS環境で環境がAdobeによってホストされている場合、Campaign コントロールパネルを使用して、証明書の期限が切れる前に証明書を更新できます。 詳しくは、[この節](https://experienceleague.adobe.com/docs/control-panel/using/subdomains-and-certificates/monitoring-ssl-certificates.html#monitoring-certificates)を参照してください。

### 手順 8 — 特定の設定を更新する {#update-configuration}

要求された SSL 証明書が正しくインストールされていると確信したら、Adobe Campaignのすべての参照を HTTP から HTTPS に更新できます。

>[!NOTE]
>
>Campaign Classicの場合、更新する URL は主に [デプロイウィザード](https://experienceleague.adobe.com/docs/campaign-classic/using/installing-campaign-classic/initial-configuration/deploying-an-instance.html#deployment-wizard) そして [外部アカウント](https://experienceleague.adobe.com/docs/campaign-classic/using/installing-campaign-classic/accessing-external-database/external-accounts.html) （トラッキング、ミラーページ、パブリックリソースドメイン）。 Campaign Standardについては、 [ブランディング設定](https://experienceleague.adobe.com/docs/campaign-standard/using/administrating/application-settings/branding.html#about-brand-identity).

設定が更新されると、新しい E メールは HTTP ではなく HTTPS URL で送信されます。 URL がセキュリティで保護されたことを確認するには、次のテストをすばやく実行できます。

* Adobe Campaignから画像をアップロードします。 画像がアップロードされたら、返される URL は HTTPS にする必要があります。
* ミラーページのリンク、一部の画像、テキスト、購読解除リンクを含むテスト用 E メール配信を作成します。 外部の電子メール ID（Gmail アドレスなど）に電子メールを送信します。 受け取ったら、E メールを開き、E メール内のすべてのリンクが（HTTP ではなく）HTTPS 形式で正しく開かれ、SSL 証明書の警告やエラーは表示されないことを確認します。

## 製品固有のリソース

**Campaign Classic**

* [Campaign コントロールパネル:SSL 証明書の追加（チュートリアル）](https://experienceleague.adobe.com/docs/campaign-classic-learn/control-panel/subdomains-and-certificates/adding-ssl-certificates.html) - SSL 証明書を追加してサブドメインを保護する方法を説明します。

**Campaign Standard**

* [Campaign コントロールパネル:SSL 証明書の追加（チュートリアル）](https://experienceleague.adobe.com/docs/campaign-standard-learn/control-panel/subdomains-and-certificates/adding-ssl-certificates.html?lang=ja) - SSL 証明書を追加してサブドメインを保護する方法を説明します。
