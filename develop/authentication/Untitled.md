## 描述


> ## What is the JSON Web Token structure?

> In its compact form, JSON Web Tokens consist of three parts separated by dots (`.`), which are:

> -   Header
> -   Payload
> -   Signature

> Therefore, a JWT typically looks like the following.

`xxxxx.yyyyy.zzzzz`


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

- Header 編碼前會是
	- 定義製作token的算法
	- 定義token用何種形式來包裝
- Header 整體內容會是如下，接著採用BASE64加密來以下內容，但其內容
```
{
  "alg": "HS256",
  "typ": "JWT"
}
```




## 複習


---
Status: #🌱 
Tags:
[[JWT]]
Links:
References: