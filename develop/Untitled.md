## 描述


> Question: What is the Audience?
> Answer:
> The audience parameter exists as part of the OAuth2.0 protocol. You can read more information from the specification here 1.0k.

> What is it?
> The audience (presented as the aud claim in the access token) defines the intended recipients of the token.

> This is typically the resource server (API, in the dashboard) that a client (Application) would like to access.

> It can be added to the request to authorize i.e. audience: 'https://test-api'

> Here is an example where an application MY_CLIENT_ID_12345 requested an access token with an audience of https://test-api.

```
{
  "header": {
    "alg": "RS256",
    "typ": "JWT",
    "kid": "123456"
  },
  "payload": {
    "iss": "https://xxxxx.auth0.com/",
    "sub": "auth0|123456789",
    "aud": "https://test-api",
    "iat": 1634332895,
    "exp": 1634419295,
    "azp": "MY_CLIENT_ID_123456",
    "scope": "openid email",
    "permissions": []
  },
  "signature": "123456"
}
```

> You will see the audience is in the token as aud.

> Although the access token is issued to the client/application (azp), it is not the intended recipient. Rather, the client is the authorized party (presented as the azp claim in the access token) and is not meant to consume the access token.



> One important claim is the aud claim. This claim defines the audience of the token, i.e., the web application that is meant to be the final recipient of the token. In the case of the ID token, its value is the client ID of the application that should consume the token.


重點：
- JWT 中的 aud 值會是 audience ，表明要將本JWT賦予給誰使用或者接收者
	- 在ID token的情況下，aud值會是指被綁定的特定身分，通常會是以該身分在Authorization Server/OpenID Provider上的client_id或者識別字
	- 在access token的情況下，aud值會是被授權使用的應用程式，也就是OAuth的client或者OpenID Connect中的Replying Party。

https://stackoverflow.com/questions/28418360/jwt-json-web-token-audience-aud-versus-client-id-whats-the-difference


The JWT will contain an aud claim that specifies which Resource Servers the JWT is valid for


JWT 将包含一个 aud 声明，指定 JWT 对哪些资源服务器有效

https://5xruby.tw/posts/what-is-jwt

-   **aud**：audience 的簡稱，用單字串(case-sensitive) 或 URI 或陣列表示這個 JWT 唯一識別的預期接收者。換句話說，當此聲明存在，則讀取此 JWT 中的數據的一方必須在 aud 中找到自己，或者無視 JWT 中包含的數據。與 iss 和 sub 要求的情況一樣，該權利要求是專用的。



## 複習
#🧠 Question :: ->->-> ``

---
Status: #🌱 
Tags:
[[Authorization]]
Links:
References: