## 描述


### JWT 會是什麼？

[[@ShiShuiZaiQiaoDaWoChuangShiMoShiJWT]]

> JWT 的全名是 JSON Web Token，是一種基於 JSON 的開放標準(RFC 7519)，它定義了一種簡潔(compact)且自包含(self-contained)的方式，用於在雙方之間安全地將訊息作為 JSON 物件傳輸。而這個訊息是經過數位簽章(Digital Signature)，因此可以被驗證及信任。可以使用 密碼(經過 HMAC 演算法) 或用一對 公鑰/私鑰(經過 RSA 或 ECDSA 演算法) 來對 JWT 進行簽章。

> -   自包含(self-contained)：payload 裡面就有所需要的資訊，不需要再重新 query database 的資料。



[[@JSONWebToken]]
> JSON Web Token (JWT, pronounced /dʒɒt/, same as the word "jot") is a proposed Internet standard for creating data with optional signature and/or optional encryption whose payload holds JSON that asserts some number of claims. The tokens are signed either using a private secret or a public/private key.


[[@ShiShuiZaiQiaoDaWoChuangShiMoShiJWT]]

> -   **授權(Authorization)**：這是很常見 JWT 的使用方式，例如使用者從 Client 端登入後，該使用者再次對 Server 端發送請求的時候，會夾帶著 JWT，允許使用者存取該 token 有權限的資源。單一登錄(Single Sign On)是當今廣泛使用 JWT 的功能之一，因為它的成本較小並且可以在不同的網域(domain)中輕鬆使用。
> 
> -   **訊息交換(Information Exchange)**：JWT 可以透過公鑰/私鑰來做簽章，讓我們可以知道是誰發送這個 JWT，此外，由於簽章是使用 header 和 payload 計算的，因此還可以驗證內容是否遭到篡改。



重點：
- JSON Web Token 是以JSON的開放標準為基礎並定義以JSON形式來包裝訊息並傳遞，接著搭配使用簽署來確保傳遞過程不會被人篡改。
- JWT 具體是特定編碼下的JSON 形式payload 之對應編碼值和簽署值串連在一塊的字串。
- payload 主要儲存對於特定對象所宣稱的描述，具體會以JSON物件的屬性來分別描述，簽署值則是使用簽署算法＋簽署密鑰＋payload編碼後的值＋header編碼後的值
- 用途為：
	- 訊息傳遞
	- 存取特定資源的權限授權給其他對象：誰擁有token誰就能存取特定資源。
- 細節：
	- JWT 本身有self-contained 特性，這是指JWT內容本身就是資訊，不需要額外從特定伺服器獲取資訊。


#### token 

> a symbol or visible representation of something 

重點：
- token 是表達特定事物/概念的符號/字元/字串

### 概念實現

[[@auth0.comJWTIOJSON]]
> ## What is the JSON Web Token structure?

> In its compact form, JSON Web Tokens consist of three parts separated by dots (`.`), which are:

> -   Header
> -   Payload
> -   Signature

> Therefore, a JWT typically looks like the following.

`xxxxx.yyyyy.zzzzz`


重點：
- JWT 全名為JSON Web Token
- JWT 會用 "." 符號來區隔資料內容種類，分為：
	- Header
	- Payload
	- Signature
- JWT形式：
	- xxxxx 代表 Header 編碼後的內容
	- yyyyy 代表 Payload 編碼後的內容
	- zzzzz 代表簽署值
```
xxxxx.yyyyy.zzzzz
```



### header 部分


> ### Header
> The header _typically_ consists of two parts: the type of the token, which is JWT, and the signing algorithm being used, such as HMAC SHA256 or RSA.


> For example:
```
{
  "alg": "HS256",
  "typ": "JWT"
}
```
> Then, this JSON is **Base64Url** encoded to form the first part of the JWT.




重點
- Header 主要負責：
	- 定義製作token的算法
	- 定義token用何種形式來包裝
- Header 整體內容會是如下，接著採用BASE64來編碼以下內容，而編碼後的內容很容易被解碼
```
{
  "alg": "HS256",
  "typ": "JWT"
}
```


### Payload 部分

> ### Payload
> The second part of the token is the payload, which contains the claims. Claims are statements about an entity (typically, the user) and additional data

> An example payload could be:
```
{
  "sub": "1234567890",
  "name": "John Doe",
  "admin": true
}
```
> The payload is then **Base64Url** encoded to form the second part of the JSON Web Token.

重點：
- Payload 主要負責：
	- token 所要傳遞的主要內容(比如特定使用者的資料)	
	- 主要內容中的每一個屬性會是對於特定資訊的描述(claim)
- Payload  整體內容會是如下，接著採用BASE64來編碼以下內容，而編碼後的內容很容易被解碼
```
{
  "sub": "1234567890",
  "name": "John Doe",
  "admin": true
}
```

### Signature 部分

> ### Signature

> To create the signature part you have to take the encoded header, the encoded payload, a secret, the algorithm specified in the header, and sign that.

> For example if you want to use the HMAC SHA256 algorithm, the signature will be created in the following way:
```
HMACSHA256(
  base64UrlEncode(header) + "." +
  base64UrlEncode(payload),
  secret)
```


重點：
- 簽署值會是採用hashing算法，其算法結果會是以下的處理結果，主要檢測JWT是否被人篡改內部資料：
	- header：JWT夾雜的header內容，會用BASE64編碼
	- payload：JWT夾雜的payload內容，會用BASE64編碼
	- secret：伺服器用來執行hashing算法的密鑰
```
HMACSHA256(
  base64UrlEncode(header) + "." +
  base64UrlEncode(payload),
  secret)
```

## 複習

#🧠 JWT 全名為何？ ->->-> `JSON Web Token`
<!--SR:!2023-01-12,3,250-->

#🧠 JWT 會用什麼符號來區隔資料內容種類？->->-> `"." `
<!--SR:!2023-01-12,3,250-->


#🧠  JWT 會用 "." 符號來區隔資料內容種類，分為哪些？->->-> `	- Header - Payload - Signature`
<!--SR:!2023-01-12,3,250-->


#🧠 JWT 會用 "." 符號來區隔資料內容種類，其完整形式會是？ ->->-> `xxxxx.yyyyy.zzzzz - xxxxx 代表 Header 編碼後的內容 - yyyyy 代表 Payload 編碼後的內容- zzzzz 代表簽署值`
<!--SR:!2023-01-12,3,250-->

#🧠 JWT的header部分是負責？ ->->-> `	- 定義製作token的算法 - 定義token用何種形式來包裝`
<!--SR:!2023-01-12,3,250-->

#🧠 JWT的header內容會用什麼算法來編碼？ ->->-> `使用base64`
<!--SR:!2023-01-12,3,250-->

#🧠 JWT的payload部分是負責？->->-> `token 所要傳遞的主要內容(比如特定使用者的資料)	`
<!--SR:!2023-01-12,3,250-->

#🧠 在JWT的payload部分中，以物件來看那部分內容，每個屬性可以被當作什麼？ ->->-> `對於特定資訊的描述(claim)`
<!--SR:!2023-01-12,3,250-->


#🧠 JWT的payload內容會用什麼算法來編碼？ ->->-> `使用base64`
<!--SR:!2023-01-12,3,250-->

#🧠 JWT的Signature部分是負責？ ->->-> `檢測JWT是否被人篡改內部資料的簽署值`
<!--SR:!2023-01-12,3,250-->

#🧠 JWT的Signature部分是檢測JWT是否被人篡改內部資料的簽署值，那麼簽署值算法的流程會是什麼？->->-> `HMACSHA256( base64UrlEncode(header) + "." + base64UrlEncode(payload),secret) 	- header：JWT夾雜的header內容，會用BASE64編碼 - payload：JWT夾雜的payload內容，會用BASE64編碼 - secret：伺服器用來執行hashing算法的密鑰`
<!--SR:!2023-01-12,3,250-->


#🧠 JSON Web Token 概念是什麼？ ->->-> `是以JSON的開放標準為基礎並定義以JSON形式來包裝訊息並傳遞，接著搭配使用簽署來確保傳遞過程不會被人篡改`

#🧠 JSON Web Token 概念是以JSON的開放標準為基礎並定義以JSON形式來包裝訊息並傳遞，接著搭配使用簽署來確保傳遞過程不會被人篡改，具體實現會是？ ->->-> `JWT 具體是特定編碼下的JSON 形式payload 之對應編碼值和簽署值串連在一塊的字串。`


#🧠  JSON Web Token 的payload會是什麼形式以及什麼內容？ ->->-> ` payload 主要儲存對於特定對象所宣稱的描述，具體會以JSON物件的屬性來分別描述`


#🧠 JSON Web Token 用途為何？ ->->-> `	- 訊息傳遞 - 存取特定資源的權限授權給其他對象`

#🧠 JWT本身有self-contained 特性，這是指什麼？ ->->-> `JWT內容本身就是資訊，不需要額外從特定伺服器獲取資訊。`

---
Status: #🌱 
Tags:
[[JWT]]
Links:
References:
[[@JSONWebToken]]
[[@auth0.comJWTIOJSON]]
[[@ShiShuiZaiQiaoDaWoChuangShiMoShiJWT]]