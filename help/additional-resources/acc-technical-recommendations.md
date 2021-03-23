---
title: Campaign Classic — 技術的な推奨事項
description: Adobe Campaign Classic を使用して配信品質を向上させるために使用できるテクニック、設定およびツールを紹介します。
feature: 実際に使う
topics: Deliverability
kt: null
thumbnail: null
doc-type: article
activity: understand
team: ACS
translation-type: tm+mt
source-git-commit: 1e539b5df54250a5927701009e7a9c84e5d73fae
workflow-type: tm+mt
source-wordcount: '1579'
ht-degree: 66%

---


# Campaign Classic — 技術的な推奨事項{#technical-recommendations}

Adobe Campaign Classicを使用する場合の配信品質を向上させるために使用できるテクニック、設定、ツールを以下に示します。

## 設定 {#configuration}

### リバース DNS {#reverse-dns}

Adobe Campaign は、IP アドレスに対してリバース DNS が提供されているかどうか、そのリバース DNS が正しく IP を指しているかどうかを確認します。

ネットワーク設定で重要な点は、送信メッセージの IP アドレスごとに正しいリバース DNS が必ず定義されるようにすることです。つまり、特定の IP アドレスには、最初の IP アドレスにループバックする対応 DNS（A レコード）を記述したリバース DNS レコード（PTR レコード）があるということです。

特定の ISP を扱う場合には、リバース DNS のドメイン選択が影響を及ぼします。特に、AOL は、リバース DNS と同じドメインに属するアドレスのフィードバックループのみを受け付けます（[フィードバックループ](#feedback-loop)を参照）。

>[!NOTE]
>
>[この外部ツール](https://mxtoolbox.com/SuperTool.aspx)を使用して、ドメインの構成を検証できます。

### MX ルール {#mx-rules}

MX（Mail eXchanger）ルールは、送信サーバーと受信サーバーの間の通信を管理するルールです。

より正確には、Adobe CampaignMTA(Message Transfer Agent)が個々の電子メールドメインまたはISP（hotmail.com、comcast.netなど）に電子メールを送信する速度を制御するために使用されます。 これらの規則は、通常、ISPが発行する制限に基づいています（例えば、各SMTP接続に含めるメッセージの数が20件を超えないようにします）。

>[!NOTE]
>
>Adobe Campaign ClassicのMX管理についての詳細は、[](https://experienceleague.adobe.com/docs/campaign-classic/using/installing-campaign-classic/additional-configurations/email-deliverability.html#mx-configuration)を参照してください。

### TLS {#tls}

TLS（トランスポート層セキュリティ）は、暗号化プロトコルで、2 つの E メールサーバー間の接続を保護したり、E メールのコンテンツを保護して意図された受信者以外によって読まれないようにするために使用できます。

### 送信者のドメイン{#sender-domain}

HELOコマンドに使用するドメインを定義するには、インスタンスの設定ファイル(conf/config-instance.xml)を編集し、「localDomain」属性を次のように定義します。

```
<serverConf>
  <shared>
    <dnsConfig localDomain="mydomain.net"/>
  </shared>
</serverConf>
```

MAIL FROMドメインは、技術的なバウンスメッセージで使用されるドメインです。 このアドレスは、デプロイメントウィザードで、またはNmsEmail_DefaultErrorAddrオプションを使用して定義されます。

### SPFレコード{#dns-configuration}

SPFレコードは、現在、DNSサーバ上でTXTタイプのレコード（コード16）またはSPFタイプのレコード（コード99）として定義できます。 SPFレコードは、文字列の形式をとります。 次に例を示します。

```
v=spf1 ip4:12.34.56.78/32 ip4:12.34.56.79/32 ~all
```

は、ドメインに電子メールを送信する権限を持つ12.34.56.78と12.34.56.79という2つのIPアドレスを定義します。 **～** allは、他のアドレスをSoftFailとして解釈する必要があることを意味します。

SPFレコードを定義するRecommendations:

* 追加&#x200B;**～all** (SoftFail)または&#x200B;**-all** (Fail)が最後に表示され、定義された以外のサーバがすべて拒否されます。 この機能がないと、サーバはこのドメインを（中立評価で）構築できます。
* **ptr**&#x200B;は追加しないでください（openspf.orgでは、コストと信頼性が低くなります）。

>[!NOTE]
>
>SPFの詳細については、[このセクション](/help/additional-resources/authentication.md#spf)を参照してください。

## 認証

>[!NOTE]
>
>電子メール認証の様々な形式について詳しくは、[このセクション](/help/additional-resources/authentication.md)を参照してください。

### DKIM {#dkim-acc}

>[!NOTE]
>
>ホストインストールまたはハイブリッドインストールで [Enhanced MTA](https://experienceleague.adobe.com/docs/campaign-classic/using/sending-messages/sending-emails/sending-an-email/sending-with-enhanced-mta.html#sending-messages) にアップグレードした場合、すべてのドメインのすべてのメッセージに対する DKIM の E メール認証署名は、Enhanced MTA がおこないます。

[DKIM](/help/additional-resources/authentication.md#dkim)をAdobe Campaign Classicと併用するには、次の前提条件が必要です。

**Adobe Campaignオプションの宣言**:Adobe Campaignでは、DKIM秘密鍵は、DKIMセレクターとドメインに基づいています。同じドメイン／サブドメインに対して、セレクターの異なる複数の秘密鍵を作成することは、現時点ではできません。プラットフォームでも E メールでも、どのセレクタードメイン／サブドメインを認証に使用すべきかを定義することはできません。プラットフォームでは、その代わりに、秘密鍵のいずれか 1 つを選択します。つまり、認証は失敗する可能性が高くなります。

* お使いの Adobe Campaign インスタンスに DomainKeys を設定してある場合は、[ドメイン管理ルール](https://experienceleague.adobe.com/docs/campaign-classic/using/sending-messages/monitoring-deliveries/understanding-delivery-failures.html#email-management-rules)で **dkim** を選択するだけです。そうでない場合は、DomainKeys（DKIMを置き換える）と同じ設定手順（秘密鍵/公開鍵）に従います。
* DKIM は DomainKeys の改良版なので、同じドメインに DomainKeys と DKIM の両方を有効にする必要はありません。
* 現在 DKIM が有効になっているドメインは、AOL および Gmail です。

## フィードバックループ {#feedback-loop-acc}

メッセージの送信に使用される IP アドレスの範囲に対して、特定の E メールアドレスを ISP レベルで宣言することにより、フィードバックループが機能します。ISP では、受信者からスパムとして報告されたメッセージを、バウンスメッセージの場合と同様の方法で、このメールボックスに送信します。苦情を訴えたユーザーへの今後の配信をブロックするように、プラットフォームを設定する必要があります。これらのユーザーが正しいオプトアウトリンクを使用しなかったとしても、そうしたユーザーにはもう連絡しないことが重要です。これは、ISPがIPアドレスをに追加するという苦情に基づブロックリストいています。 ISP によっては、苦情率がおよそ 1％になると、IP アドレスがブロックリストに登録されます。

フィードバックループメッセージの形式を定義する標準 [Abuse Feedback Reporting Format（ARF）](https://tools.ietf.org/html/rfc6650)が現在策定中です。

インスタンスのフィードバックループを実装するには、次が必要です。

* 対象インスタンス専用のメールボックス（バウンスメールボックスとなる場合があります）
* 対象インスタンス専用の IP 送信アドレス

Adobe Campaign でシンプルなフィードバックループを実装する場合は、バウンスメッセージ機能が使用されます。フィードバックループメールボックスは、バウンスメールボックスとして使用され、これらのメッセージを検出するためのルールが定義されます。メッセージをスパムとして報告した受信者の E メールアドレスは、強制隔離リストに追加されます。

* **拒否**、タイプ&#x200B;**ハード**&#x200B;の理由で、**[!UICONTROL Administration > Campaign Management > Non deliverables Management > Mail rule sets]**&#x200B;内にバウンスメールルール&#x200B;**Feedback_loop**&#x200B;を作成または変更します。
* フィードバックループ用にメールボックスが特別に定義されている場合は、**[!UICONTROL Administration > Platform > External accounts]**&#x200B;に新しい外部バウンスメールアカウントを作成して、そのメールボックスにアクセスするためのパラメータを定義します。

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

配信品質の最適な管理を実現するには、**List-Unsubscribe** という SMTP ヘッダーを付けることが不可欠です。

このヘッダーは、「スパムとして報告」アイコンの代わりに使用できます。これを付けると、E メールインターフェイスに購読解除リンクが表示されます。

この機能を使用すると、評判を守ることができ、フィードバックは購読解除として実行されます。

List-Unsubscribe を使用するには、次のようなコマンドラインを入力する必要があります。

```
List-Unsubscribe: mailto: client@newsletter.example.com?subject=unsubscribe?body=unsubscribe
```

>[!CAUTION]
>
>上記の例は受信者テーブルに基づいています。データベースの実装が別のテーブルに基づいておこなわれている場合は、正しい情報を反映するようにコマンドラインを修正する必要があります。

次のコマンドラインは、動的な **List-Unsubscribe** の作成に使用できます。

```
List-Unsubscribe: mailto: %=errorAddress%?subject=unsubscribe%=message.mimeMessageId%
```

Gmail、Outlook.com、Microsoft Outlookでは、このメソッドがサポートされており、Outlookのインターフェイスから直接購読解除ボタンを使用できます。 この手法を利用すると、苦情率が下がります。

**リスト — 登録解除**&#x200B;は、次のいずれかを使用して実装できます。

* 直接[配信テンプレート](#adding-a-command-line-in-a-delivery-template)にコマンドラインを追加
* [タイポロジルールの作成](#creating-a-typology-rule)

### 配信テンプレートへのコマンドラインの追加 {#adding-a-command-line-in-a-delivery-template}

コマンドラインは、E メールの SMTP ヘッダーの追加セクションに追加する必要があります。

この追加は E メールごとにおこなうこともできますし、既存の配信テンプレートでおこなうこともできます。また、この機能を組み込んだ配信テンプレートを新しく作成することもできます。

### タイポロジルールの作成 {#creating-a-typology-rule}

ルールには、コマンドラインを生成するスクリプトが含まれている必要があり、このルールを E メールヘッダーに組み込む必要があります。

>[!NOTE]
>
>タイポロジルールを作成することをお勧めします。各 E メールに List-Unsubscribe 機能が自動的に追加されます。

1. List-Unsubscribe: &lt;mailto:unsubscribe@domain.com>

   ユーザーが&#x200B;**購読解除**&#x200B;リンクをクリックすると、デフォルトの E メールクライアントが開きます。このタイポロジルールは、E メールの作成に使用されるタイポロジに追加する必要があります。

1. List-Unsubscribe: `<https://domain.com/unsubscribe.jsp>`

   ユーザーが&#x200B;**購読解除**&#x200B;リンクをクリックすると、購読解除フォームにリダイレクトされます。

   例：

   ![](../assets/s_tn_del_unsubscribe_param.png)

>[!NOTE]
>
>[このセクション](https://experienceleague.adobe.com/docs/campaign-classic/using/orchestrating-campaigns/campaign-optimization/about-campaign-typologies.html#typology-rules)で、Adobe Campaign Classicでタイポロジルールを作成する方法を説明します。

## E メールの最適化 {#email-optimization}

### SMTP {#smtp}

SMTP（Simple Mail Transfer Protoco）は、E メール送信のインターネット標準です。

ルールでチェックされないSMTPエラーは、**[!UICONTROL Administration]** > **[!UICONTROL Campaign Management]** > **[!UICONTROL Non deliverables Management]** > **[!UICONTROL Delivery log qualification]**&#x200B;フォルダーに一覧表示されます。 これらのエラーメッセージは、デフォルトでは、到達不能なソフトエラーと解釈されます。

SMTPサーバーからのフィードバックを正しく認証したい場合、最も一般的なエラーを識別し、**[!UICONTROL Administration]** > **[!UICONTROL Campaign Management]** > **[!UICONTROL Non deliverables Management]** > **[!UICONTROL Mail rule sets]**&#x200B;に対応する規則を追加する必要があります。 これをおこなわないと、プラットフォームは不要な再試行を実行したり（不明ユーザーの場合）、一定回数のテストの後に特定の受信者を誤って強制隔離したりすることになります。

### 専用の IP {#dedicated-ips}

アドビは、高いレピュテーションを得て配信パフォーマンスを最適化するために、ランプアップ IP を持つ各顧客に専用の IP 戦略を提供します。
