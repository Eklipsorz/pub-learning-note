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


https://juejin.cn/post/6859572307505971213
[[@AccessTokenRefresh]]

## 複習


---
Status: #🌱 
Tags:
[[Authentication]]
Links:
[[id token 本身是用來證明特定使用者是受過認證的資訊，使用者或者Relying Party 向OpenID Provider提供特定身份的證明資訊，接著由OpenID Provider對其進行驗證，若驗證成功就會發放對應token]]

References:
[[@WhatAreRefresh]]