## 描述


### 後端的任一服務端點是否回傳新id token和refresh token

> returnSecureToken 為 true
> whether or not to return an ID and refresh token
> but it could be true if we want to get a new token in response

考量到服務端點可能會修改到伺服器內部對於特定事物的credential，所以基於credential而製作的token勢必會出現token新舊問題，所以會替端點增加請求封包的參數來指定是否產生新的token和refresh token



[[@WhatAreRefresh]]
> As mentioned, for security purposes, access tokens may be valid for a short amount of time. Once they expire, client applications can use a refresh token to "refresh" the access token. That is, a refresh token is a credential artifact that lets a client application get new access tokens without having to ask the user to log in again.

> An application system where a SPA uses a refresh token to obtain a new access token
![](https://images.ctfassets.net/cdy7uua7fh8z/3sf7RRsy81bt3zcXMnHUSe/2171fdab4ffeb0987c329aa897038abc/rt-and-at.png)
> In the diagram above, SPA = Single-Page Application; AS = Authorization Server; RS = Resource Server; AT = Access Token; RT = Refresh Token.

> The client application can get a new access token as long as the refresh token is valid and unexpired. Consequently, a refresh token that has a very long lifespan could theoretically give infinite power to the token bearer to get a new access token to access protected resources anytime. The bearer of the refresh token could be a legitimate user or a malicious user. As such, security companies, such as Auth0, create mechanisms to ensure that this powerful token is mainly held and used continuously by the intended parties.

重點：
- refresh token 主要是提供Client/Replying Party向Authorization Server索要新的Token

#### refresh 命名緣由

refresh ：
>  to become fresh again

> computing
> to display the latest updated version (of a web page or document)



fresh 作為動詞用
> to make or become fresh

fresh 作為形容詞
> new or different

重點：
- fresh 作為形容詞，會是指新的或者不同的； 作為動詞，會是指將特定事物變成新的事物
- refresh 作為動詞，會是重新再將特定事物轉變成新的事物，在電腦科學上會是指將畫面轉變成最新版本的畫面。



##


[[@AccessTokenRefresh]]

![https://res.cloudinary.com/dqfxgtyoi/image/upload/v1674049658/blog/authentication/refresh-token-and-token-flow_fhv9nl.png](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1674049658/blog/authentication/refresh-token-and-token-flow_fhv9nl.png)

> 上图中Authorization Server翻译为授权服务，负责Token的签发。Resource Server翻译为资源服务，也就是被授权访问的资源，比如API接口。在分布式应用中，他们应该分属不同的服务。 值得注意的是，资源服务器不签发Token，但是可以具备独立验证Access Token的能力。

> 上面的流程图包括了下面的步骤。

> -   (A) 客户端向授权服务器请求Access Token（整个认证授权的流程，可以是多次请求完成该步骤）
> -   (B) 授权服务器验证客户端身份无误，且请求的资源是合理的，则颁发Access Token 和 Refresh Token，可以同时返回Access Token的过期时间等附加属性。
> -   (C) 带着Access Token请求资源
> -   (D) 资源服务器验证Access Token有效则返回请求的内容。
> -   (E) **注意：** 上面的(C)(D)步骤可以反复进行，直到Access Token过期。 如果客户端在请求之前就能判断Access Token已过期或临近过期（下发过期时间），就可以直接跳到步骤(G)。否则，就会再请求一次，也就产生了本步骤。
> -   (F) 当Access Token无效的时候，资源服务器会拒绝响应资源并返回Token无效的错误。
> -   (G) 客户端重新向授权服务器请求Access Token，但是这次只需带着Refresh Token即可，而不需要用户再执行认证和授权的流程。这样就可以做到用户无感。
> -   (H) 授权服务器验证Refresh Token，如果有效，则签发新的Access Token（或者同时下发一个新的Refresh Token）。

> 我们总结几个点，Access Token作为请求资源的凭证，是使用最频繁的，但是有效期比较短，Refresh Token有效期较长，只会发给授权服务器，用来获取新的Access Token。

  


## 複習


---
Status: #🌱 
Tags:
[[Authentication]]
Links:
[[id token 本身是用來證明特定使用者是受過認證的資訊，使用者或者Relying Party 向OpenID Provider提供特定身份的證明資訊，接著由OpenID Provider對其進行驗證，若驗證成功就會發放對應token]]

References:
[[@WhatAreRefresh]]