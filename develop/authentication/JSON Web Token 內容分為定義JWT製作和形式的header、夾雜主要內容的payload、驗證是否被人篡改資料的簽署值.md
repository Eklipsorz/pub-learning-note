## 描述


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

#🧠 JWT 會用什麼符號來區隔資料內容種類？->->-> `"." `


#🧠  JWT 會用 "." 符號來區隔資料內容種類，分為哪些？->->-> `	- Header - Payload - Signature`


#🧠 JWT 會用 "." 符號來區隔資料內容種類，其完整形式會是？ ->->-> `xxxxx.yyyyy.zzzzz - xxxxx 代表 Header 編碼後的內容 - yyyyy 代表 Payload 編碼後的內容- zzzzz 代表簽署值`

#🧠 JWT的header部分是負責？ ->->-> `	- 定義製作token的算法 - 定義token用何種形式來包裝`

#🧠 JWT的header內容會用什麼算法來編碼？ ->->-> `使用base64`

#🧠 JWT的payload部分是負責？->->-> `token 所要傳遞的主要內容(比如特定使用者的資料)	`

#🧠 在JWT的payload部分中，以物件來看那部分內容，每個屬性可以被當作什麼？ ->->-> `對於特定資訊的描述(claim)`
<!--SR:!2023-01-12,3,250-->


#🧠 JWT的payload內容會用什麼算法來編碼？ ->->-> `使用base64`

#🧠 JWT的Signature部分是負責？ ->->-> `檢測JWT是否被人篡改內部資料的簽署值`

#🧠 JWT的Signature部分是檢測JWT是否被人篡改內部資料的簽署值，那麼簽署值算法的流程會是什麼？->->-> `HMACSHA256( base64UrlEncode(header) + "." + base64UrlEncode(payload),secret) 	- header：JWT夾雜的header內容，會用BASE64編碼 - payload：JWT夾雜的payload內容，會用BASE64編碼 - secret：伺服器用來執行hashing算法的密鑰`




---
Status: #🌱 
Tags:
[[JWT]]
Links:
References:
[[@auth0.comJWTIOJSON]]