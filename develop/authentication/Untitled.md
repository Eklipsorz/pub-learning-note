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

The second part of the token is the payload, which contains the claims. Claims are statements about an entity (typically, the user) and additional data



## 複習


---
Status: #🌱 
Tags:
[[JWT]]
Links:
References: