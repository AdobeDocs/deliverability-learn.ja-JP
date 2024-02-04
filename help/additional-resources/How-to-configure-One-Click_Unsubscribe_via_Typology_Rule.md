---
source-git-commit: 945a7ba5e3c3ac9544199e1bb62273933a82f04a
workflow-type: tm+mt
source-wordcount: '168'
ht-degree: 8%

---
# ワンクリック List-Unsubscribe をサポートするタイポロジルールを作成する：

**1.新しいタイポロジルールを作成します。**
* ナビゲーションツリーで「新規」をクリックし、新しいタイポロジを作成します。

![画像](/help/assets/CreatingTypologyRules1.png)

**2. 次の手順で、タイポロジルールを設定します。**
* ルールタイプ：コントロール
* フェーズ：ターゲティングの開始時
* チャネル： E メール
* レベル：選択
* アクティブ


![画像](/help/assets/CreatingTypologyRules2.png)


**タイポロジルールの JavaScript をコード化します。**


>[!NOTE]
>
>以下で説明するコードは、例としてのみ参照する必要があります。
>この例では、次の方法を詳しく説明します。
>* URL List-Unsubscribe を設定し、ヘッダーを追加するか、既存の mailto：パラメーターを追加して、次と置き換えます。 &lt;mailto..>>, https://...
>* List-Unsubscribe-Post ヘッダーにを追加する
>投稿 URL の例では、var headerUnsubUrl = &quot;https://campmomentumv7-mkt-prod3.campaign.adobe.com/webApp/unsubNoClick?id=&lt;%= recipient.cryptedId %>&quot;÷を使用します。
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


![画像](/help/assets/CreatingTypologyRules3.png)

**3.新しいルールをタイポロジに追加して E メールに追加します（デフォルトのタイポロジは ok です）。**

![画像](/help/assets/CreatingTypologyRules4.png)

**4. 新しい配信を準備します（配信プロパティの追加の SMTP ヘッダーが空であることを確認します）。**

![画像](/help/assets/CreatingTypologyRules5.png)

**5. 配信の準備中に、新しいタイポロジルールが適用されていることを確認します。**

![画像](/help/assets/CreatingTypologyRules6.png)



**6.List-Unsubscribe が存在することを検証します。**

![画像](/help/assets/CreatingTypologyRules7.png)
