---
title: Campaign Classic - 技術的なレコメンデーション
description: Adobe Campaign Classic を使用して配信品質を向上させるために使用できるテクニック、設定およびツールを紹介します。
topics: Deliverability
doc-type: article
activity: understand
team: ACS
exl-id: 39ed3773-18bf-4653-93b6-ffc64546406b
source-git-commit: b163628adde1e4d7225a1c2c54d29b24e2b2a352
workflow-type: tm+mt
source-wordcount: '2128'
ht-degree: 48%

---

# Campaign Classic - 技術的なレコメンデーション {#technical-recommendations}

Adobe Campaign Classicを使用する際に、配信品質を向上させるために使用できるテクニック、設定およびツールを以下に示します。

## 設定 {#configuration}

### 逆引き DNS {#reverse-dns}

Adobe Campaign は、IP アドレスに対してリバース DNS が提供されているかどうか、そのリバース DNS が正しく IP を指しているかどうかを確認します。

ネットワーク設定で重要な点は、送信メッセージの IP アドレスごとに正しいリバース DNS が必ず定義されるようにすることです。つまり、特定の IP アドレスには、最初の IP アドレスにループバックする対応 DNS（A レコード）を記述したリバース DNS レコード（PTR レコード）があるということです。

特定の ISP を扱う場合には、リバース DNS のドメイン選択が影響を及ぼします。特に、AOL は、リバース DNS と同じドメインに属するアドレスのフィードバックループのみを受け付けます（[フィードバックループ](#feedback-loop)を参照）。

>[!NOTE]
>
>[ この外部ツール ](https://mxtoolbox.com/SuperTool.aspx) を使用して、ドメインの設定を検証できます。

### MX ルール {#mx-rules}

MX（Mail eXchanger）ルールは、送信サーバーと受信サーバーの間の通信を管理するルールです。

より正確には、Adobe Campaign MTA （Message Transfer Agent）が個々のメールドメインまたは ISP （例：hotmail.com、comcast.net）にメールを送信する速度を制御するために使用されます。 これらのルールは通常、ISP によって公開された制限に基づいています（例えば、各 SMTP 接続ごとに 20 を超えるメッセージを含めないようにします）。

>[!NOTE]
>
>Adobe Campaign Classicの MX 管理について詳しくは、[ この節 ](https://experienceleague.adobe.com/docs/campaign-classic/using/installing-campaign-classic/additional-configurations/email-deliverability.html#mx-configuration) を参照してください。

### TLS {#tls}

TLS（トランスポート層セキュリティ）は、暗号化プロトコルで、2 つのメールサーバー間の接続を保護したり、メールのコンテンツを保護して意図された受信者以外によって読まれないようにするために使用できます。

### 送信者のドメイン {#sender-domain}

HELO コマンドに使用するドメインを定義するには、インスタンスの設定ファイル（conf/config-instance.xml）を編集し、「localDomain」属性を次のように定義します。

```
<serverConf>
  <shared>
    <dnsConfig localDomain="mydomain.net"/>
  </shared>
</serverConf>
```

MAIL FROM ドメインは、技術的なバウンスメッセージで使用されるドメインです。 このアドレスは、デプロイメントウィザードで、または NmsEmail_DefaultErrorAddr オプションを使用して定義します。

### SPF レコード {#dns-configuration}

SPF レコードは、現在、DNS サーバーで TXT タイプのレコード（コード 16）または SPF タイプのレコード（コード 99）として定義できます。 SPF レコードは、文字列の形式を取ります。 例：

```
v=spf1 ip4:12.34.56.78/32 ip4:12.34.56.79/32 ~all
```

ドメインのメールを送信するために許可される 2 つの IP アドレス（12.34.56.78 と 12.34.56.79）を定義します。 **～all** は、その他のアドレスは SoftFail として解釈される必要があることを意味します。

SPF レコードを定義するためのRecommendations:

* 定義されたサーバー以外のすべてのサーバーを拒否するには、末尾に **～all** （SoftFail）または **-all** （Fail）を追加します。 これがないと、サーバーはこのドメインを（中立的な評価で）偽造することができます。
* **ptr** を追加しないでください（openspf.orgでは、コストがかかり信頼性が低いとしてこれを推奨しています）。

>[!NOTE]
>
>SPF について詳しくは、[ この節 ](/help/additional-resources/authentication.md#spf) を参照してください。

## 認証

>[!NOTE]
>
>様々なメール認証フォームについて詳しくは、[ この節 ](/help/additional-resources/authentication.md) を参照してください。

### DKIM {#dkim-acc}

>[!NOTE]
>
>ホストインストールまたはハイブリッドインストールで [Enhanced MTA](https://experienceleague.adobe.com/docs/campaign-classic/using/sending-messages/sending-emails/sending-an-email/sending-with-enhanced-mta.html#sending-messages) にアップグレードした場合、すべてのドメインのすべてのメッセージに対する DKIM のメール認証署名は、Enhanced MTA がおこないます。

Adobe Campaign Classicで [DKIM](/help/additional-resources/authentication.md#dkim) を使用するには、次の前提条件が必要です。

**Adobe Campaign オプション宣言**: Adobe Campaignでは、DKIM 秘密鍵は DKIM セレクターおよびドメインに基づいています。 同じドメイン／サブドメインに対して、セレクターの異なる複数の秘密鍵を作成することは、現時点ではできません。プラットフォームでもメールでも、どのセレクタードメイン／サブドメインを認証に使用すべきかを定義することはできません。プラットフォームでは、その代わりに、秘密鍵のいずれか 1 つを選択します。つまり、認証は失敗する可能性が高くなります。

* お使いの Adobe Campaign インスタンスに DomainKeys を設定してある場合は、[ドメイン管理ルール](https://experienceleague.adobe.com/docs/campaign-classic/using/sending-messages/monitoring-deliveries/understanding-delivery-failures.html#email-management-rules)で **dkim** を選択するだけです。そうでない場合は、DomainKeys （DKIM の代わり）と同じ設定手順（秘密鍵/公開鍵）に従います。
* DKIM は DomainKeys の改良版なので、同じドメインに DomainKeys と DKIM の両方を有効にする必要はありません。
* 現在 DKIM が有効になっているドメインは、AOL および Gmail です。

## フィードバックループ {#feedback-loop-acc}

メッセージの送信に使用される IP アドレスの範囲に対して、特定のメールアドレスを ISP レベルで宣言することにより、フィードバックループが機能します。ISP では、受信者からスパムとして報告されたメッセージを、バウンスメッセージの場合と同様の方法で、このメールボックスに送信します。苦情を訴えたユーザーへの今後の配信をブロックするように、プラットフォームを設定する必要があります。これらのユーザーが正しいオプトアウトリンクを使用しなかったとしても、そうしたユーザーにはもう連絡しないことが重要です。ISP がブロックリストに IP アドレスを追加するのは、これらの苦情に基づいています。 ISP によっては、苦情率がおよそ 1％になると、IP アドレスがブロックリストに登録されます。

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

配信品質の最適な管理を実現するには、**List-Unsubscribe** という SMTP ヘッダーを付けることが不可欠です。

このヘッダーは、「スパムとして報告」アイコンの代わりに使用できます。これは、ISP のメールインターフェイスに「購読解除」リンクとして表示されます。

この機能を使用すると、苦情の発生率が低下し、評判を保護するのに役立ちます。 フィードバックは、登録解除として実行されます。

Gmail、Outlook.com、Yahoo! Microsoft Outlook では、この方法をサポートしています。 「登録解除」リンクは、インターフェイスで直接使用できます。 例：

![画像](../assets/List-Unsubscribe-example-Gmail.png)

>[!NOTE]
>
>「購読解除」リンクは常に表示されるとは限りません。 実際には、各 ISP の特定の基準とポリシーに依存する可能性があります。 したがって、メッセージが送信者によって送信されていることを確認します。
>
>* 評判の良い
>* ISP のスパム報告しきい値の下
>* 完全認証済み

List-Unsubscribe ヘッダー機能には、次の 2 つのバージョンがあります。

* **「mailto」 List-Unsubscribe** – このメソッドで **購読解除** リンクをクリックすると、メールヘッダーで指定された購読解除アドレスに事前入力されたメールが送信されます。 [詳細情報](#mailto-list-unsubscribe)

* **「ワンクリック」リスト – 購読解除** – このメソッドで、**購読解除** リンクをクリックすると、ユーザーの購読が直接解除されます。 [詳細情報](#one-click-list-unsubscribe)

>[!NOTE]
>
>2024 年 6 月 1 日（PT）以降、主要な ISP は、送信者に対して、**ワンクリックリスト – 登録解除** に準拠するよう求めるようになります。

### 「mailto」リスト – 購読解除 {#mailto-list-unsubscribe}

このメソッドでは、「購読解除 **リンクをクリックすると、メール** ヘッダーで指定された購読解除アドレスに事前入力されたメールが送信されます。

「mailto」 List-Unsubscribe を使用するには、メールアドレスを指定するコマンドラインを入力する必要があります。例：`List-Unsubscribe: <mailto:client@newsletter.example.com?subject=unsubscribe?body=unsubscribe>`

>[!CAUTION]
>
>上記の例は受信者テーブルに基づいています。データベースの実装が別のテーブルに基づいておこなわれている場合は、正しい情報を反映するようにコマンドラインを修正する必要があります。

`List-Unsubscribe: <mailto:<%=errorAddress%>?subject=unsubscribe%=message.mimeMessageId%>` のようなコマンドラインを使用して、動的な「mailto」 List-Unsubscribe を作成することもできます。

Campaign に **mailto」 List-Unsubscribe** を実装するには、次のいずれかを実行します。

* 配信または配信テンプレートへのコマンドラインの直接追加 – [ 詳細 ](#adding-a-command-line-in-a-delivery-template)

* タイポロジルールの作成 – [ 詳細 ](#creating-a-typology-rule)

#### 配信またはテンプレートへのコマンドラインの追加 {#adding-a-command-line-in-a-delivery-template}

コマンドラインをメールの SMTP ヘッダーの **[!UICONTROL 追加の SMTP ヘッダー]** セクションに追加する必要があります。

この追加はメールごとにおこなうこともできますし、既存の配信テンプレートでおこなうこともできます。また、この機能を組み込んだ配信テンプレートを新しく作成することもできます。

例えば、「**[!UICONTROL 追加の SMTP ヘッダー]**」フィールドに次のスクリプトを入力します。`List-Unsubscribe: mailto:unsubscribe@domain.com`。 **登録解除** リンクをクリックすると、unsubscribe@domain.com アドレスにメールが送信されます。

また、動的アドレスを使用することもできます。 例えば、プラットフォーム用に定義されたエラーアドレスにメールを送信するには、次のスクリプトを使用できます。`List-Unsubscribe: <mailto:<%=errorAddress%>?subject=unsubscribe%=message.mimeMessageId%>`

![画像](../assets/List-Unsubscribe-template-SMTP.png)

#### タイポロジルールの作成 {#creating-a-typology-rule}

ルールには、コマンドラインを生成するスクリプトが含まれている必要があり、このルールをメールヘッダーに組み込む必要があります。

Adobe Campaign v7/v8 でタイポロジルールを作成する方法については、[ この節 ](https://experienceleague.adobe.com/docs/campaign-classic/using/orchestrating-campaigns/campaign-optimization/about-campaign-typologies.html#typology-rules) を参照してください。

>[!NOTE]
>
>タイポロジルールを作成することをお勧めします。このタイポロジルールを使用すると、各メールにリスト – 購読解除機能が自動的に追加されます。

### ワンクリックリスト – 登録解除 {#one-click-list-unsubscribe}

このメソッドを使用すると、「購読解除 **リンクをクリックすると、ユーザーの購読が直接解除され** す。購読解除には 1 つのアクションのみが必要です。

2024 年 6 月 1 日（PT）以降、主要な ISP は、送信者に対して、**ワンクリックリスト – 登録解除** に準拠するよう求めるようになります。

この要件に準拠するには、送信者は次の操作を行う必要があります。

* コマンドライン `List-Unsubscribe-Post: List-Unsubscribe=One-Click` を追加します。
* URI 登録解除リンクを含めます。
* Adobe Campaignがサポートする、受信者からの HTTP POST応答の受信をサポートします。 外部サービスを使用することもできます。

Adobe Campaign v7/v8 で直接ワンクリックリスト – 登録解除POST応答をサポートするには、「受信者の登録解除 – クリックなし」 web アプリケーションにを追加する必要があります。 それには、以下の手順を実行します。

1. **[!UICONTROL リソース]**/**[!UICONTROL オンライン]**/**[!UICONTROL web アプリケーション]** に移動します。

1. 「受信者の登録解除のクリックなし」 [XML](/help/assets/WebAppUnsubNoClick.xml.zip) ファイルをアップロードします。

Campaign で **ワンクリックリスト – 登録解除** を設定するには、次のいずれかを実行します。

* 配信または配信テンプレートへのコマンドラインの追加 – [ 詳細 ](#one-click-delivery-template)
* タイポロジルールの作成 – [ 詳細 ](#one-click-typology-rule)

#### 配信またはテンプレートでのワンクリックリスト – 購読解除の設定 {#one-click-delivery-template}

配信または配信テンプレートでワンクリックリスト – 購読解除を設定するには、次の手順に従います。

1. 配信プロパティの「**[!UICONTROL SMTP]**」セクションに移動します。

1. **[!UICONTROL 追加の SMTP ヘッダー]** の下に、次の例のようなコマンドラインを入力します。 各ヘッダーは、別々の行にする必要があります。

例：

```
List-Unsubscribe-Post: List-Unsubscribe=One-Click
List-Unsubscribe: <https://domain.com/webApp/unsubNoClick?id=<%= recipient.cryptedId %> >, < mailto:<%@ include option='NmsEmail_DefaultErrorAddr' %>?subject=unsubscribe<%=escape(message.mimeMessageId) %> >
```

![画像](../assets/List-Unsubscribe-1-click-template-SMTP.png)

上記の例では、ワンクリックをサポートしている ISP に対してワンクリックリスト – 登録解除を有効にしますが、「mailto」をサポートしていない受信者も、メールを介して登録解除を引き続きリクエストできます。

#### ワンクリックリスト – 購読解除をサポートするタイポロジルールの作成 {#one-click-typology-rule}

タイポロジルールを使用してワンクリックリスト – 購読解除を設定するには、次の手順に従います。

1. ナビゲーションツリーで、**[!UICONTROL タイポロジルール]** に移動し、**[!UICONTROL 新規]** をクリックします。

   ![画像](../assets/CreatingTypologyRules1.png)


1. 次のような新しいタイポロジルールを設定します。

   * **[!UICONTROL ルールタイプ]**: **[!UICONTROL コントロール]**
   * **[!UICONTROL フェーズ]**:**[!UICONTROL ターゲティングの開始時]**
   * **[!UICONTROL チャネル]**: **[!UICONTROL メール]**
   * **[!UICONTROL レベル]**：自分で選ぶ
   * **[!UICONTROL アクティブ]**


   ![画像](../assets/CreatingTypologyRules2.png)

1. 次の例のように、タイポロジルールの Javascript をコーディングします。

   >[!NOTE]
   >
   >以下で説明するコードは、例としてのみ参照してください。

   この例では、次の方法を詳しく説明します。
   * 「mailto」リストの購読解除を設定します。 ヘッダーを追加するか、既存の「mailto:」パラメーターを追加して、&lt;mailto...に置き換えます。>、https://...
   * ワンクリックリスト – 登録解除ヘッダーにを追加します。 `var headerUnsubUrl = "https://campmomentumv7-mkt-prod3.campaign.adobe.com/webApp/unsubNoClick?id=<%= recipient.cryptedId %>"÷` を使用します

   >[!NOTE]
   >
   >その他のパラメーター（例：&amp;service =...）を追加できます。

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
   var headerUnsubUrl = "https://campmomentumv7-mkt-prod3.campaign.adobe.com/webApp/unsubNoClick?id=<%= recipient.cryptedId %>"; 
     
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


   ![画像](../assets/CreatingTypologyRules3.png)

1. メールに適用するタイポロジに新しいルールを追加します。

   >[!NOTE]
   >
   >これをデフォルトのタイポロジに追加できます。

   ![画像](../assets/CreatingTypologyRules4.png)

1. 新しい配信を準備します。

   >[!CAUTION]
   >
   >配信プロパティの **[!UICONTROL 追加の SMTP ヘッダー]** フィールドが空であることを確認します。

   ![画像](../assets/CreatingTypologyRules5.png)

1. 配信準備中に、新しいタイポロジルールが適用されていることを確認します。

   ![画像](../assets/CreatingTypologyRules6.png)

1. 購読解除リンクが存在することを確認します。

   ![画像](../assets/CreatingTypologyRules7.png)

## メールの最適化 {#email-optimization}

### SMTP {#smtp}

SMTP（Simple Mail Transfer Protoco）は、メール送信のインターネット標準です。

ルールでチェックされない SMTP エラーは、**[!UICONTROL 管理]**／**[!UICONTROL キャンペーン管理]**／**[!UICONTROL 配信不能件数の管理]**／**[!UICONTROL 配信ログの検証]**&#x200B;フォルダーにリスト表示されます。これらのエラーメッセージは、デフォルトでは到達不能ソフトエラーとして解釈されます。

SMTP サーバーからのフィードバックを正しく検証する場合は、最もよく起こるエラーを特定し、それに対応するルールを&#x200B;**[!UICONTROL 管理]**／**[!UICONTROL キャンペーン管理]**／**[!UICONTROL 配信不能件数の管理]**／**[!UICONTROL メールルールセット]**&#x200B;に追加する必要があります。これをおこなわないと、プラットフォームは不要な再試行を実行したり（不明ユーザーの場合）、一定回数のテストの後に特定の受信者を誤って強制隔離したりすることになります。

### 専用 IP {#dedicated-ips}

アドビは、高いレピュテーションを得て配信パフォーマンスを最適化するために、ランプアップ IP を持つ各顧客に専用の IP 戦略を提供します。
