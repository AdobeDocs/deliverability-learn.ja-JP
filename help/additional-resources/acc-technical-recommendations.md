---
title: Campaign Classic - 技術的なレコメンデーション
description: Adobe Campaign Classic を使用して配信品質を向上させるために使用できるテクニック、設定およびツールを紹介します。
topics: Deliverability
doc-type: article
activity: understand
team: ACS
exl-id: 39ed3773-18bf-4653-93b6-ffc64546406b
source-git-commit: 3dc1d2f352346fa2ef7b5c883da6a3e243cb32c0
workflow-type: tm+mt
source-wordcount: '1889'
ht-degree: 56%

---

# Campaign Classic - 技術的なレコメンデーション {#technical-recommendations}

Adobe Campaign Classicを使用する際に配信品質の割合を向上させるために使用できるテクニック、設定、ツールのいくつかを以下に示します。

## 設定 {#configuration}

### リバース DNS {#reverse-dns}

Adobe Campaign は、IP アドレスに対してリバース DNS が提供されているかどうか、そのリバース DNS が正しく IP を指しているかどうかを確認します。

ネットワーク設定で重要な点は、送信メッセージの IP アドレスごとに正しいリバース DNS が必ず定義されるようにすることです。つまり、特定の IP アドレスには、最初の IP アドレスにループバックする対応 DNS（A レコード）を記述したリバース DNS レコード（PTR レコード）があるということです。

特定の ISP を扱う場合には、リバース DNS のドメイン選択が影響を及ぼします。特に、AOL は、リバース DNS と同じドメインに属するアドレスのフィードバックループのみを受け付けます（[フィードバックループ](#feedback-loop)を参照）。

>[!NOTE]
>
>以下を使用できます。 [この外部ツール](https://mxtoolbox.com/SuperTool.aspx) をクリックして、ドメインの設定を検証します。

### MX ルール {#mx-rules}

MX（Mail eXchanger）ルールは、送信サーバーと受信サーバーの間の通信を管理するルールです。

より正確に言えば、Adobe Campaign MTA(Message Transfer Agent) が E メールを個々の E メールドメインまたは ISP(hotmail.com、comcast.netなど ) に送信する速度を制御するために使用されます。 これらのルールは、通常、ISP によって公開された制限に基づいています（例えば、各 SMTP 接続につき 20 を超えるメッセージを含めないようにします）。

>[!NOTE]
>
>Adobe Campaign Classicでの MX 管理について詳しくは、 [この節](https://experienceleague.adobe.com/docs/campaign-classic/using/installing-campaign-classic/additional-configurations/email-deliverability.html#mx-configuration).

### TLS {#tls}

TLS（トランスポート層セキュリティ）は、暗号化プロトコルで、2 つのメールサーバー間の接続を保護したり、メールのコンテンツを保護して意図された受信者以外によって読まれないようにするために使用できます。

### 送信者のドメイン {#sender-domain}

HELO コマンドに使用するドメインを定義するには、インスタンスの設定ファイル (conf/config-instance.xml) を編集し、次のように「localDomain」属性を定義します。

```
<serverConf>
  <shared>
    <dnsConfig localDomain="mydomain.net"/>
  </shared>
</serverConf>
```

MAIL FROM ドメインは、技術的なバウンスメッセージで使用されるドメインです。 このアドレスは、デプロイウィザードで、または NmsEmail_DefaultErrorAddr オプションを使用して定義されます。

### SPF レコード {#dns-configuration}

SPF レコードは、現在、DNS サーバー上で TXT タイプのレコード（コード 16）または SPF タイプのレコード（コード 99）として定義できます。 SPF レコードは、文字列の形式を取ります。 以下に例を示します。

```
v=spf1 ip4:12.34.56.78/32 ip4:12.34.56.79/32 ~all
```

は、ドメイン用の e メールを送信する権限を持つ 2 つの IP アドレス (12.34.56.78と12.34.56.79) を定義します。 **～すべて** は、その他のアドレスが SoftFail と解釈される必要があることを意味します。

Recommendations :SPF レコードを定義します。

* 追加 **～すべて** (SoftFail) または **-all** （失敗）最後に、定義された以外のすべてのサーバーを拒否します。 これがなければ、サーバは（Neutral 評価を使用して）このドメインを構築できます。
* 追加しない **ptr** (openspf.orgは、コストが高く信頼できないとして、これに対するお勧めです )。

>[!NOTE]
>
>での SPF の詳細 [この節](/help/additional-resources/authentication.md#spf).

## 認証

>[!NOTE]
>
>様々な形式の E メール認証について詳しくは、 [この節](/help/additional-resources/authentication.md).

### DKIM {#dkim-acc}

>[!NOTE]
>
>ホストインストールまたはハイブリッドインストールで [Enhanced MTA](https://experienceleague.adobe.com/docs/campaign-classic/using/sending-messages/sending-emails/sending-an-email/sending-with-enhanced-mta.html#sending-messages) にアップグレードした場合、すべてのドメインのすべてのメッセージに対する DKIM のメール認証署名は、Enhanced MTA がおこないます。

使用 [DKIM](/help/additional-resources/authentication.md#dkim) Adobe Campaign Classicを使用するには、次の前提条件が必要です。

**Adobe Campaignオプション宣言**:Adobe Campaignでは、DKIM 秘密鍵は DKIM セレクターとドメインに基づきます。 同じドメイン／サブドメインに対して、セレクターの異なる複数の秘密鍵を作成することは、現時点ではできません。プラットフォームでもメールでも、どのセレクタードメイン／サブドメインを認証に使用すべきかを定義することはできません。プラットフォームでは、その代わりに、秘密鍵のいずれか 1 つを選択します。つまり、認証は失敗する可能性が高くなります。

* お使いの Adobe Campaign インスタンスに DomainKeys を設定してある場合は、[ドメイン管理ルール](https://experienceleague.adobe.com/docs/campaign-classic/using/sending-messages/monitoring-deliveries/understanding-delivery-failures.html#email-management-rules)で **dkim** を選択するだけです。そうでない場合は、DomainKeys（DKIM に代わる）と同じ設定手順（秘密鍵/公開鍵）に従います。
* DKIM は DomainKeys の改良版なので、同じドメインに DomainKeys と DKIM の両方を有効にする必要はありません。
* 現在 DKIM が有効になっているドメインは、AOL および Gmail です。

## フィードバックループ {#feedback-loop-acc}

メッセージの送信に使用される IP アドレスの範囲に対して、特定のメールアドレスを ISP レベルで宣言することにより、フィードバックループが機能します。ISP では、受信者からスパムとして報告されたメッセージを、バウンスメッセージの場合と同様の方法で、このメールボックスに送信します。苦情を訴えたユーザーへの今後の配信をブロックするように、プラットフォームを設定する必要があります。これらのユーザーが正しいオプトアウトリンクを使用しなかったとしても、そうしたユーザーにはもう連絡しないことが重要です。ISP が苦情に基づいて、IP アドレスをそのに追加すブロックリストに加えるる。 ISP によっては、苦情率がおよそ 1％になると、IP アドレスがブロックリストに登録されます。

フィードバックループメッセージの形式を定義する標準 [Abuse Feedback Reporting Format（ARF）](https://tools.ietf.org/html/rfc6650)が現在策定中です。

インスタンスのフィードバックループを実装するには、次が必要です。

* 対象インスタンス専用のメールボックス（バウンスメールボックスとなる場合があります）
* 対象インスタンス専用の IP 送信アドレス

Adobe Campaign でシンプルなフィードバックループを実装する場合は、バウンスメッセージ機能が使用されます。フィードバックループメールボックスは、バウンスメールボックスとして使用され、これらのメッセージを検出するためのルールが定義されます。メッセージをスパムとして報告した受信者のメールアドレスは、強制隔離リストに追加されます。

* **[!UICONTROL 管理／キャンペーン管理／配信不能件数の管理／メールルールセット]**&#x200B;で、理由として「**拒否**」、タイプとして「**ハード**」を指定してバウンスメールルール **Feedback_loop** を作成または変更します。
* メールボックスが特にフィードバックループ用に定義されている場合は、**[!UICONTROL 管理／プラットフォーム／外部アカウント]**&#x200B;で新しい外部バウンスメールアカウントを作成することにより、メールボックスにアクセスするためのパラメーターを定義します。

苦情の通知を処理するメカニズムが直ちに有効になります。このルールが正しく機能していることを確認するには、これらのメッセージが収集されないようにアカウントを一時的に無効にした後、フィードバックループメールボックスの内容を手動で確認します。サーバー上で、次のコマンドを順に実行します。

```
nlserver stop inMail@instance,
nlserver inMail -instance:instance -verbose.
```

複数のインスタンスに単一のフィードバックループアドレスを使用せざるを得ない場合は、次をおこなう必要があります。

* 受信したメッセージをインスタンスと同数のメールボックス上に複製します。
* インスタンスごとに各メールボックスが選択されるようにします。
* 関係するメッセージだけを処理するようにインスタンスを設定します。インスタンス情報は、Adobe Campaign から送信されるメッセージの Message-ID ヘッダーに含まれているので、フィードバックループメッセージにも含まれています。インスタンス設定ファイルの **checkInstanceName** パラメーターを指定するだけです（デフォルトでは、インスタンスは検証されず、その結果、特定のアドレスが誤って強制隔離される可能性があります）。

  ```
  <serverConf>
    <inMail checkInstanceName="true"/>
  </serverConf>
  ```

Adobe Campaign の配信品質サービスは、以下の ISP のフィードバックループサービスへのサブスクリプションを管理します。AOL、BlueTie、Comcast、Cox、EarthLink、FastMail、Gmail、Hotmail、HostedEmail、Libero、Mail.ru、MailTrust、OpenSRS、QQ、RoadRunner、Synacor、Telenor、Terra、UnitedOnline、USA、XS4ALL、Yahoo、Yandex、Zoho。

## List-Unsubscribe {#list-unsubscribe}

### List-Unsubscribe について {#about-list-unsubscribe}

という名前の SMTP ヘッダーを追加しています **List-Unsubscribe** は、最適な配信品質管理を確保するために必須です。2024 年 6 月 1 日以降、Yahoo および Gmail では、送信者がワンクリックリスト配信停止に準拠する必要があります。 One-Click List-Unsubscribe の設定方法については、以下を参照してください。


このヘッダーは、「スパムとして報告」アイコンの代わりに使用できます。E メールインターフェイスに配信停止リンクとして表示されます。

この機能を使用すると、評判を守ることができ、フィードバックは購読解除として実行されます。

List-Unsubscribe を使用するには、次のようなコマンドラインを入力する必要があります。

```
List-Unsubscribe: <mailto: client@newsletter.example.com?subject=unsubscribe?body=unsubscribe>
```

>[!CAUTION]
>
>上記の例は受信者テーブルに基づいています。データベースの実装が別のテーブルに基づいておこなわれている場合は、正しい情報を反映するようにコマンドラインを修正する必要があります。

次のコマンドラインは、動的な **List-Unsubscribe** の作成に使用できます。

```
List-Unsubscribe: <mailto: %=errorAddress%?subject=unsubscribe%=message.mimeMessageId%>
```

Gmail、Outlook.comおよびMicrosoft Outlook はこの方法をサポートしており、Outlook のインターフェイスで直接購読解除ボタンを使用できます。 この手法を利用すると、苦情率が下がります。

以下を実装できます。 **List-Unsubscribe** 次のいずれかを指定します。

* 直接 [配信テンプレートへのコマンドラインの追加](#adding-a-command-line-in-a-delivery-template)
* [タイポロジルールの作成](#creating-a-typology-rule)

### 配信テンプレートへのコマンドラインの追加 {#adding-a-command-line-in-a-delivery-template}

コマンドラインは、メールの SMTP ヘッダーの追加セクションに追加する必要があります。

この追加はメールごとにおこなうこともできますし、既存の配信テンプレートでおこなうこともできます。また、この機能を組み込んだ配信テンプレートを新しく作成することもできます。

* List-Unsubscribe: <mailto:unsubscribe@domain.com>
ユーザーが購読解除リンクをクリックすると、デフォルトの E メールクライアントが開きます。 このタイポロジルールは、メールの作成に使用されるタイポロジに追加する必要があります。

* List-Unsubscribe: <https://domain.com/unsubscribe.jsp>
ユーザーが購読解除リンクをクリックすると、購読解除フォームにリダイレクトされます。
  ![画像](/help/assets/UTF-8-1.png)


### タイポロジルールの作成 {#creating-a-typology-rule}

ルールには、コマンドラインを生成するスクリプトが含まれている必要があり、このルールをメールヘッダーに組み込む必要があります。

>[!NOTE]
>
>タイポロジルールを作成することをお勧めします。各メールに List-Unsubscribe 機能が自動的に追加されます。

>[!NOTE]
>
>Adobe Campaign Classicでタイポロジルールを作成する方法については、 [この節](https://experienceleague.adobe.com/docs/campaign-classic/using/orchestrating-campaigns/campaign-optimization/about-campaign-typologies.html#typology-rules).

### ワンクリックリスト配信停止

2024 年 6 月 1 日以降、Yahoo および Gmail では、送信者がワンクリックリスト配信停止に準拠する必要があります。 ワンクリックリスト配信停止要件の送信者に準拠するには、次の要件を満たす必要があります。

* &quot;List-Unsubscribe-Post: List-Unsubscribe=One-Click&quot;に追加します。
* URI 配信停止リンクを含める
* Adobe Campaignがサポートするレシーバーからの HTTPPOST応答の受信をサポートします。

One-Click List-Unsubscribe を直接設定するには：

* 次の「受信者の購読解除 (no-click)」Web アプリケーションを追加します。 
   1. リソース/オンライン/Web アプリケーションに移動します。
   2. 「受信者の購読解除 (no-click)」をアップロード [XML](/help/assets/WebAppUnsubNoClick.xml.zip)
* List-Unsubscribe および List-Unsubscribe-Post の設定
   1. 配信プロパティの「 SMTP 」セクションに移動します。
   2. 「 Additional SMTP Headers 」で、コマンドラインにを入力します（各ヘッダーは別々の行に記述する必要があります）。

```
List-Unsubscribe-Post: List-Unsubscribe=One-Click
List-Unsubscribe: <https//domain.com/webApp/unsubNoClick?id=<%= recipient.cryptidcamp %>>, <mailto: %=errorAddress%?
subject=unsubscribe%=message.mimeMessageId%>
```

上記の例では、One-Click をサポートする ISP で One-Click List-Unsubscribe を有効にします。一方、URL list-unsubscribe をサポートしていない受信者は、引き続き E メールで配信停止を要求できます。


### ワンクリック List-Unsubscribe をサポートするタイポロジルールを作成する：

新しいタイポロジルールを作成します。

* ナビゲーションツリーで「新規」をクリックし、新しいタイポロジを作成します。

![画像](/help/assets/CreatingTypologyRules1.png)

次の手順で、タイポロジルールを設定します。

* ルールタイプ：コントロール
* チャネル： E メール
* フェーズ：パーソナライゼーションの開始時
* レベル：選択した項目
* アクティブ

![画像](/help/assets/CreatingTypologyRules2.png)

タイポロジルールの JavaScript をコード化します。

>[!NOTE]
>
>以下で説明するコードは、例としてのみ参照する必要があります。
>この例では、次の方法を詳しく説明します。
>* URL List-Unsubscribe を設定し、ヘッダーを追加するか、既存の mailto：パラメーターを追加して、次と置き換えます。 &lt;mailto..>, <http://…>
>* List-Unsubscribe-Post ヘッダーにを追加する
>投稿 URL の例では、var headerUnsubUrl = &quot;http://campmomentumv7-mkt-prod3.campaign.adobe.com/webApp/unsubNoClick?id=&lt;%= recipient.cryptedId %>&quot;を使用します。
>* 他のパラメーター（&amp;service = ...など）を追加できます。
>


```
// Function to add or replace a header in the provided headers 
function addHeader(headers, header, value)  { 
    
  // Create the new header line 
  var headerLine = header + ": " + value; 
    
  // Create a regular expression to find the specified header 
  var regExp = new RegExp(header + ":(.*)$", "i") 
    
  // Split the headers into individual lines 
  var headerLines = headers.split("\n"); 
    
  // Loop through each line 
  for (var i=0; i < headerLines.length; i++) { 
      
    // Check if the specified header exists 
    var match = headerLines[i].match(regExp) 
      
    // If it exists 
    if ( match != null ) { 
        
      // Replace the existing header line 
      headerLines[i] = headerLine; 
        
      // Return the modified headers 
      return headerLines.join("\n"); 
    } 
  } 
    
  // If the header does not exist, add the new header line 
  headerLines.push(headerLine); 
    
  // Return the modified headers 
  return headerLines.join("\n"); 
} 
  
// Function to get the value of a specified header from the provided headers 
function getHeader(headers, header) { 
    
  // Create a regular expression to find the specified header 
  var regExp = new RegExp(header + ":(.*)$", "i") 
    
  // Split the headers into individual lines 
  var headerLines = headers.split("\n"); 
    
  // Loop each line 
  for each (line in headerLines) { 
      
    // Check if the specified header exists 
    var match = line.match(regExp); 
      
    // If it exists 
    if ( match != null ) { 
        
      // Return the header value, removing leading whitespace 
      return match[1].replace(/^\s*/, ""); 
    } 
  } 
    
  // If the header does not exist, return an empty string 
  return ""; 
} 
  
  
// Define the unsubscribe URL 
var headerUnsubUrl = "http://campmomentumv7-mkt-prod3.campaign.adobe.com/webApp/unsubNoClick?id=<%= recipient.cryptedId %>"; 
  
// Get the value of the List-Unsubscribe header 
var headerUnsub = getHeader(delivery.mailParameters.headers, "List-Unsubscribe"); 
  
// If the List-Unsubscribe header does not exist 
if ( headerUnsub === "" ) { 
  // Add the List-Unsubscribe header 
  delivery.mailParameters.headers = addHeader(delivery.mailParameters.headers, "List-Unsubscribe", "<"+headerUnsubUrl+">"); 
} 
// If the List-Unsubscribe header exists and contains 'mailto' 
else if(headerUnsub.search('mailto')){ 
  // Replace the existing List-Unsubscribe header 
  delivery.mailParameters.headers = addHeader(delivery.mailParameters.headers, "List-Unsubscribe", "<"+headerUnsubUrl+">"); 
} 
  
// Get the value of the List-Unsubscribe-Post header 
var headerUnsubPost = getHeader(delivery.mailParameters.headers, "List-Unsubscribe-Post"); 
  
// If the List-Unsubscribe-Post header does not exist 
if ( headerUnsubPost === "" ) { 
  // Add the List-Unsubscribe-Post header 
  delivery.mailParameters.headers = addHeader(delivery.mailParameters.headers, "List-Unsubscribe-Post", "List-Unsubscribe=One-Click"); 
} 
  
// Return true to indicate success 
return true; 
```

![画像](/help/assets/CreatingTypologyRules3.png)

新しいルールをタイポロジに追加します（デフォルトのタイポロジは ok です）。

![画像](/help/assets/CreatingTypologyRules4.png)

新しい配信を準備します（配信プロパティの追加の SMTP ヘッダーが空であることを確認します）。

![画像](/help/assets/CreatingTypologyRules5.png)

配信の準備中に、新しいタイポロジルールが適用されていることを確認します。

![画像](/help/assets/CreatingTypologyRules6.png)

List-Unsubscribe が存在することを検証します。

![画像](/help/assets/CreatingTypologyRules7.png)

## E メールの最適化 {#email-optimization}

### SMTP {#smtp}

SMTP（Simple Mail Transfer Protoco）は、メール送信のインターネット標準です。

ルールでチェックされない SMTP エラーは、**[!UICONTROL 管理]**／**[!UICONTROL キャンペーン管理]**／**[!UICONTROL 配信不能件数の管理]**／**[!UICONTROL 配信ログの検証]**&#x200B;フォルダーにリスト表示されます。これらのエラーメッセージは、デフォルトでは、到達不能なソフトエラーと解釈されます。

SMTP サーバーからのフィードバックを正しく検証する場合は、最もよく起こるエラーを特定し、それに対応するルールを&#x200B;**[!UICONTROL 管理]**／**[!UICONTROL キャンペーン管理]**／**[!UICONTROL 配信不能件数の管理]**／**[!UICONTROL メールルールセット]**&#x200B;に追加する必要があります。これをおこなわないと、プラットフォームは不要な再試行を実行したり（不明ユーザーの場合）、一定回数のテストの後に特定の受信者を誤って強制隔離したりすることになります。

### 専用 IP {#dedicated-ips}

アドビは、高いレピュテーションを得て配信パフォーマンスを最適化するために、ランプアップ IP を持つ各顧客に専用の IP 戦略を提供します。
