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
- refresh token 是一種token，該token來讓Client/Replying Party **在不需要額外使用者帳號進行credential驗證的情況下** 直接向Authorization Server索要新的Access Token/ID token
- 其出現目的為：
	- 盡可能在減緩惡意使用者使用合法token 機會的情況下，讓獲取合法token的client保持更長的合法時間來獲取資源
	- 讓獲取合法token的client 能從Authorization Server/OpenID Provider中獲取最新資訊的token 
- 其壽命來說：
	- refresh token > access token / ID token 
	- 其原因如目的。


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
- refresh 作為動詞，會是重新再將特定事物轉變成新的事物，在網頁開發上會是指將畫面轉變成最新版本的畫面。



### refresh token 獲取/使用流程


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

流程為：Resource Server被假定成具有驗證Access Token、回傳資源的功能
A. Client 向 Authorization Server 索要Access Token
B. Authorization Server 驗證客戶端身份無誤且請求資源是合理的，就頒發Access Token 和Refresh Token (這兩種Token都各綁定過期時間)
C. Client 用Access Token向Resource Server 發送受保護資源的請求
D. Resource Server 驗證Access Token有效並回傳受保護資源給Client
E. 當 Client 想使用 Access Token 向Resource Server 發送受保護資源的請求時，就能發現Token過期或者快過期就跳到G，否則Client 就以過期或者快過期的Token 向Resource Server 發送
F. Resource Server 檢驗Token時發現過期，就拒絕回傳受保護資源
G. Client 自行使用Refresh Token 來向Authorization Server來獲取最新內容的Access Token
H. Authorization Server驗證Refresh Token，若驗證成功就簽發新的Access Token(或者也會簽發一個新的Refresh Token)給Client

## 複習

#🧠 fresh 作為動詞用的意思會是什麼？ ->->-> ` 作為動詞，會是指將特定事物變成新的事物`
<!--SR:!2023-10-24,169,250-->

#🧠 fresh 作為形容詞用的意思會是什麼？ ->->-> `fresh 作為形容詞，會是指新的或者不同的`
<!--SR:!2023-10-22,56,230-->

#🧠 refresh 作為動詞用的意思會是什麼？->->-> `會是重新再將特定事物轉變成新的事物`
<!--SR:!2023-10-26,60,210-->

#🧠 refresh 作為動詞，會是重新再將特定事物轉變成新的事物，在網頁開發上會是什麼？ ->->-> `在電腦科學上會是指將畫面轉變成最新版本的畫面`
<!--SR:!2023-09-16,148,250-->


#🧠 refresh token 會是什麼？ ->->-> ` 是一種token，該token來讓Client/Replying Party **在不需要額外使用者帳號進行credential驗證的情況下** 直接向Authorization Server索要新的Access Token/ID token`
<!--SR:!2023-10-21,55,230-->

#🧠 refresh token 是一種token，該token來讓Client/Replying Party **在不需要額外使用者帳號進行credential驗證的情況下** 直接向Authorization Server索要新的Access Token/ID token，其出現目的為何？ ->->-> `- 盡可能在減緩惡意使用者使用合法token 機會的情況下，讓獲取合法token的client保持更長的合法時間來獲取資源 - 讓獲取合法token的client 能從Authorization Server/OpenID Provider中獲取最新資訊的token `
<!--SR:!2023-09-04,6,247-->


#🧠 refresh token目的只有 **盡可能在減緩惡意使用者使用合法token 機會的情況下，讓獲取合法token的client保持更長的合法時間來獲取資源** 嗎? 還有什麼？->->-> `讓獲取合法token的client 能從Authorization Server/OpenID Provider中獲取最新資訊的token `
<!--SR:!2023-09-15,12,243-->


#🧠 refresh token目的只有 **讓獲取合法token的client 能從Authorization Server/OpenID Provider中獲取最新資訊的token** 嗎? 還有什麼？ ->->-> `盡可能在減緩惡意使用者使用合法token 機會的情況下，讓獲取合法token的client保持更長的合法時間來獲取資源`
<!--SR:!2023-09-14,11,247-->



#🧠 refresh token 和 access token/id token 相比較壽命來說會是什麼？為什麼？ ->->-> `	- refresh token > access token / ID token  - 其原因如目的。`
<!--SR:!2023-10-14,161,250-->

#🧠 以下為access token 和 refresh token 獲取過程，請仔細說明，另外Resource Server被假定成具有驗證Access Token、回傳資源的功能![https://res.cloudinary.com/dqfxgtyoi/image/upload/v1674049658/blog/authentication/refresh-token-and-token-flow_fhv9nl.png](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1674049658/blog/authentication/refresh-token-and-token-flow_fhv9nl.png) ->->-> `A. Client 向 Authorization Server 索要Access Token。B. Authorization Server 驗證客戶端身份無誤且請求資源是合理的，就頒發Access Token 和Refresh Token (這兩種Token都各綁定過期時間) 。C. Client 用Access Token向Resource Server 發送受保護資源的請求 。D. Resource Server 驗證Access Token有效並回傳受保護資源給Client。E. 當 Client 想使用 Access Token 向Resource Server 發送受保護資源的請求時，就能發現Token過期或者快過期就跳到G，否則Client 就以過期或者快過期的Token 向Resource Server 發送 。F. Resource Server 檢驗Token時發現過期，就拒絕回傳受保護資源。G. Client 自行使用Refresh Token 來向Authorization Server來獲取最新內容的Access Token。H. Authorization Server驗證Refresh Token，若驗證成功就簽發新的Access Token(或者也會簽發一個新的Refresh Token)給Client`
<!--SR:!2023-10-16,50,230-->





#🧠 請畫圖來簡單描述access token 和 refresh token 獲取過程以及使用他們的過程 ->->-> ![https://res.cloudinary.com/dqfxgtyoi/image/upload/v1674049658/blog/authentication/refresh-token-and-token-flow_fhv9nl.png](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1674049658/blog/authentication/refresh-token-and-token-flow_fhv9nl.png)
<!--SR:!2023-09-19,23,189-->

#🧠 以下為access token 和 refresh token 獲取過程，請仔細說明其中(E)、(F)驗證token是否過期的負責業務還可以是誰？，另外Resource Server被假定成具有驗證Access Token、回傳資源的功能。![https://res.cloudinary.com/dqfxgtyoi/image/upload/v1674049658/blog/authentication/refresh-token-and-token-flow_fhv9nl.png](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1674049658/blog/authentication/refresh-token-and-token-flow_fhv9nl.png) ->->-> `Client 可以在內部驗證是否過期再來決定發送、Client 並不會驗證而轉由Authorization Server驗證是否過期`
<!--SR:!2024-02-07,230,250-->



---
Status: #🌱 
Tags:
[[Authentication]]
Links:
[[id token 本身是用來證明特定使用者是受過認證的資訊，使用者或者Relying Party 向OpenID Provider提供特定身份的證明資訊，接著由OpenID Provider對其進行驗證，若驗證成功就會發放對應token]]

References:
[[@WhatAreRefresh]]
[[@AccessTokenRefresh]]