## 描述


### JWT 

[[@jonesJSONWebToken2015]]
> The "aud" (audience) claim identifies the recipients that the JWT is
   intended for.  Each principal intended to process the JWT MUST
   identify itself with a value in the audience claim.  If the principal
   processing the claim does not identify itself with a value in the
   "aud" claim when this claim is present, then the JWT MUST be
   rejected.




[[@ShiShuiZaiQiaoDaWoChuangShiMoShiJWT]]
-   **aud**：audience 的簡稱，用單字串(case-sensitive) 或 URI 或陣列表示這個 JWT 唯一識別的預期接收者。換句話說，當此聲明存在，則讀取此 JWT 中的數據的一方必須在 aud 中找到自己，或者無視 JWT 中包含的數據。與 iss 和 sub 要求的情況一樣，該權利要求是專用的。

重點：
- audience 在 JWT上是表明目前JWT 適用於哪個對象才能合法使用該JWT
- 每一個要求處理JWT驗證的principal 必須要能夠在audience claim存在對應principal的識別字才能使用JWT來驗證成功並獲取對應資源，否則就驗證失敗並拒絕讓對方使用JWT獲取對應資源。


### access token 上的aud claim

[[@WhatAudienceAuth0]]
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
- 由於 audience 在 JWT上是表明目前JWT 適用於哪個對象才能合法使用該JWT，該audience claim在ID token 和 access token都有各自的內容和檢測方式
	- 在ID token的情況下，aud值會是指token綁定的特定身分所對應的識別字，通常會是以該身分在Authorization Server/OpenID Provider上的client_id或者識別字
	- 在access token的情況下，aud值會是指允許能夠讀取JWT的Resource Server之端點，端點會是以路徑字串來表示，而端點又會是client當初註冊使用的Resource Server和其端點的路徑


[[@swainAnswerJWTJson2015]]
> The JWT will contain an aud claim that specifies which Resource Servers the JWT is valid for
> JWT 将包含一个 aud 声明，指定 JWT 对哪些资源服务器有效



#### 檢測方式

- Access Token
```
客戶端使用token向resource server發送請求，該server將token和客戶端要求的對應端點傳送給authorization server，authorization server此時會提取token的aud是否為對應端點，若是的話就合法；否則為不合法
```

- ID Token
```
client-id 並非是指使用者在資料庫上的識別字，而是經由JWT發送而產生出來的對應id
客戶端使用token向resource server發送請求，該server將token和客戶端要求的對應端點傳送給authorization server，authorization server就會從token提取aud的client_id是否存在於server中，若還存在的話，就合法；否則就不合法
```



### audience 命名緣由

[[@SpectatorHeaudienceDeQuBieZhiHu]]
> refer to readers of a newspaper, magazine, etc.

重點：
- 報章雜誌的閱讀者，也可以引申為讀取特定事物內容的一方。

### principal 命名緣由

> a person who engages another to act as his or her agent

重點：
- 委託他人代理他做事情的人

## 複習

#🧠 audience 命名緣由為何？ ->->-> `報章雜誌的閱讀者`
<!--SR:!2023-01-21,3,250-->

#🧠 audience 命名緣由為報章雜誌的閱讀者，還可以引申為什麼？ ->->-> `也可以引申為讀取特定事物內容的一方`
<!--SR:!2023-01-21,3,250-->

#🧠 principal 命名緣由為何？ ->->-> ` 委託他人代理他做事情的人`
<!--SR:!2023-01-21,3,250-->

#🧠 JWT 技術中的audience 是表明什麼？->->-> ` audience 在 JWT上是表明目前JWT 適用於哪個對象才能合法使用該JWT`


#🧠 由於 audience 在 JWT上是表明目前JWT 適用於哪個對象才能合法使用該JWT，該audience claim在ID token 和 access token都有各自的內容，其中access token的情況下，aud值會是什麼形式以及內容？->->-> `字串，aud值會是指允許能夠讀取JWT的Resource Server之端點，端點會是以路徑字串來表示，而端點又會是client當初註冊使用的Resource Server和其端點的路徑`
<!--SR:!2023-01-21,3,250-->

#🧠 由於 audience 在 JWT上是表明目前JWT 適用於哪個對象才能合法使用該JWT，該audience claim在ID token 和 access token都有各自的內容，其中ID token的情況下，aud值會是什麼形式以及內容？ ->->-> `字串，aud值會是指token綁定的特定身分所對應的識別字`


#🧠 audience 在 JWT上是表明目前JWT 適用於哪個對象才能合法使用該JWT，其合不合法實現概念會是？ ->->-> ` 每一個要求處理JWT驗證的principal 必須要能夠在audience claim存在對應principal的識別字才能使用JWT來驗證成功並獲取對應資源，否則就驗證失敗並拒絕讓對方使用JWT獲取對應資源`

#🧠 由於 audience 在 JWT上是表明目前JWT 適用於哪個對象才能合法使用該JWT，該audience claim在ID token 和 access token都有各自的內容和檢測方式，請問其內容會各為什麼？->->-> `	- 在ID token的情況下，aud值會是指token綁定的特定身分所對應的識別字，通常會是以該身分在Authorization Server/OpenID Provider上的client_id或者識別字 - 在access token的情況下，aud值會是指允許能夠讀取JWT的Resource Server之端點，端點會是以路徑字串來表示，而端點又會是client當初註冊使用的Resource Server和其端點的路徑`

#🧠 由於 audience 在 JWT上是表明目前JWT 適用於哪個對象才能合法使用該JWT，該audience claim在ID token 和 access token都有各自的內容和檢測方式，請問其檢測會各為什麼？->->-> `- Access Token：客戶端使用token向resource server發送請求，該server將token和客戶端要求的對應端點傳送給authorization server，authorization server此時會提取token的aud是否為對應端點，若是的話就合法；否則為不合法 - ID Token： 客戶端使用token向resource server發送請求，該server將token和客戶端要求的對應端點傳送給authorization server，authorization server就會從token提取aud的client_id是否存在於server中，若還存在的話，就合法；否則就不合法`
<!--SR:!2023-01-21,3,250-->


#🧠 ID Token中的client-id是如何產生的？ ->->-> `client-id 並非是指使用者在資料庫上的識別字，而是經由JWT發送而產生出來的對應id`



---
Status: #🌱 
Tags:
[[Authorization]]
Links:
References:
[[@jonesJSONWebToken2015]]
[[@ShiShuiZaiQiaoDaWoChuangShiMoShiJWT]]
[[@WhatAudienceAuth0]]
[[@swainAnswerJWTJson2015]]
[[@SpectatorHeaudienceDeQuBieZhiHu]]