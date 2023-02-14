## 描述




[[@OpenIDConnectShiShiMo]]


> 先讓我來舉一個簡單的例子。

> 現在有一個使用者，就假定是我自己本身。我的行事曆資訊都放在我的 Google Calendar 上。我現在想要使用一個可以做到比 Google Calendar 還要多功能的第三方行事曆服務。這時候我就會想要讓這第三方行事曆服務得到我在 Google Calendar 上的行事曆資訊。

![](https://hennge.com/tw/blog/1_X0LkXQ0w5JxyZP5zPmATlg.png)

> 而如果是在一個只有帳號跟密碼的世界上，我就必須要把我的 Google 帳號和密碼告訴給這第三方服務行事曆服務，它才有辦法取得這些資訊。但如果我把帳號密碼告訴了第三方，它可能就可以在暗地裡竊取行事曆以外的資訊，像是在 Gmail 裡的機密資訊。這時候就出現了使用 Access Token 來解決這個問題的協議，OAuth 2.0。

![](https://hennge.com/tw/blog/1_KkGjPLwd-FibZnYcKsAnAw.png)

> ＊關於此途中的 Access Token 的發放方式，為幫助理解細節有做簡化，敬請見諒。

> Access Token 就像是一張兌換卷，每一張 Access Token 上都有寫**「誰」「對誰」「給予什麼樣的權限」**，如此一來就可以在不告訴對方帳號密碼的情況下，給予對方最低限度需要的權限。這就是為什麼 OAuth 2.0 被稱為是一個授權的協議。


### OAuth 是什麼？

[[@OAuth2023]]

> OAuth (short for "Open Authorization") is an open standard for access delegation, commonly used as a way for internet users to grant websites or applications access to their information on other websites but without giving them the passwords

> This mechanism is used by companies such as Amazon, Google, Facebook, Microsoft, and Twitter to permit the users to share information about their accounts with third-party applications or websites.

> Generally, OAuth provides clients a "secure delegated access" to server resources on behalf of a resource owner. It specifies a process for resource owners to authorize third-party access to their server resources without providing credentials.

重點：
- OAuth 完整名稱為：Open Authorization
- OAuth：
	- 屬於標準、協定
	- 定義如何在不需要將 "擁有資源使用權限的使用者帳密" 給予 特定服務A的情況下，發放資源使用權限給特定服務A來代表使用者去做特定事情。
	- 代表權限的事物會是token，內容通常會是包含誰賦予誰權限、權限為何。


### OAuth 2.0 角色
[[@OpenIDConnectShiShiMo]]
> Access Token 就像是一張兌換卷，每一張 Access Token 上都有寫**「誰」「對誰」「給予什麼樣的權限」**，如此一來就可以在不告訴對方帳號密碼的情況下，給予對方最低限度需要的權限。這就是為什麼 OAuth 2.0 被稱為是一個授權的協議。

![](https://hennge.com/tw/blog/1_vL6Fi0RFSHvtxkkDQKAr9w.png)

> 在 OAuth 2.0 的世界中，我這個使用者被稱為 Resource Owner；第三方行事曆服務被稱之為 Client；有放我行事曆資訊的 Google Calendar 稱為 Resource Server；幫忙發 Access Token 的伺服器稱之為 Authorization Server，在這例子中就會是 Google。


[[@auth0ValidateAccessTokens]] ：當client使用JWT存取resource server所要做的驗證：
>1.  Perform standard JWT validation. Because the access token is a JWT, you need to perform the standard JWT validation steps. See Validate JSON Web Tokens for details.
> 2. Verify token audience claims. If you've performed the standard JWT validation, you have already decoded the JWT's payload and looked at its standard claims. The token audience claim (aud, array of strings) depends on the initial token request. The aud field could contain both an audience corresponding to your custom API and an audience corresponding to the /userinfo endpoint. At least one of the audience values for the token must match the unique identifier of the target API as defined in your API's Settings in the Identifier field. See Get Access Tokens for details.
> 3. Verify permissions (scopes). Verify that the application has been granted the permissions required to access your API. To do so, you will need to check the scope claim (scope, space-separated list of strings) in the decoded JWT's payload. It should match the permissions required for the endpoint being accessed. For example, if your custom API provides three endpoints to read, create, or delete a user record, when you registered your API with Auth0, you created three corresponding permissions:

重點：
- OAuth 在Client-Server之間中，會有以下用語：
	- Resource Server：管理資源、看本身能不能驗證Token，若不能的話就轉遞請求封包上的token至authorization server的伺服器，否則就自己驗證Token
	- Authorization Server：驗證Resource Owner輸入的credential來發放Token 、幫忙Resource Server驗證token是否為合法
	- Client：以發放的Token來向Resource Server索要指定資源
		- Client 相對於Resource Server的稱呼
	- Resource Owner：在Resource Server上實際擁有資源的人
- 流程會是：這裡假定Resource Server 只會管理資源，不會驗證Token
	- 由Resource Owner 輸入credential至 Authorization Server 來做驗證，成功就做下一步，失敗就回報錯誤
	- Authorization Server發送token給予Resource Owner
	- 由Resource Owner賦予token至Client
	- 由Client夾雜token來向Resource Server 發送請求以此代表Resource Owner發送
	- Resource Server 將token轉遞至Authorization Server，驗證成功就做下一步，失敗就回報錯誤，其驗證方式為：
		- 以JWT 驗證方式來驗證JWT是否被篡改
		- 提取JWT的aud值並比對目前所存取的端點(由Resource Server提供Client想要存取的端點)是否一樣，若一樣就做下一步，否則報錯
		- 提取JWT的scope值並比對目前所要存取的端點之對應動作(由Resource Server提供Client於存取端點想做的操作)是否允許，若允許就驗證成功，否則報錯
	- Resource Server 將指定Resource傳遞給Client使用

####  Resource Server vs  Authorization Server 兩者是否相同
1. 可以同時是Resource Server 和 Authorization Server
2. 可以分出兩種伺服器：一個是Resource Server、另一個為Authorization Server

### 案例



![](https://docs.oracle.com/cd/E74890_01/books/RestAPI/images/OAuth2leg_V.gif)

> The steps in client credentials grant authentication flow process shown in Figure 2 are:

> 1. The business client application makes a call to the Siebel Server to request some business information by passing an access token. Since there is no end user intervention, the client is pre-authorized to have access to the resource.
> 2. The request is redirected to the OAuth server for authentication.
> 3. The OAuth server returns an access token.
> 4. The client server sends a request to the resource server. The request includes the access token in the HTTP header. Siebel looks for USERID from the token to establish a Siebel Server session.
> 5. The Siebel server validates the access token with the OAuth server.
> 6. If the access token is authorized by the OAuth server, then access is granted to the Siebel resource.
> 7. The Siebel Server returns the requested resource.


## 複習

#🧠 OAuth 完整名稱是什麼？ ->->-> `Open Authorization`
<!--SR:!2023-02-22,25,250-->

#🧠 OAuth 完整名稱是Open Authentication 嗎？為什麼？ ->->-> `不是，會是Open Authorization`
<!--SR:!2023-03-27,44,250-->

#🧠 Open Authorization 或者OAuth 會是什麼？ ->->-> `一種標準、協定。定義如何在不需要將 "擁有資源使用權限的使用者帳密" 給予 特定服務A的情況下，發放資源使用權限給特定服務A來代表使用者去做特定事情。`
<!--SR:!2023-03-29,44,250-->


#🧠 在Open Authorization 或者OAuth中，代表權限的事物會是什麼？ ->->-> `token`
<!--SR:!2023-02-22,25,250-->




#🧠 在Open Authorization 或者OAuth中，代表權限的事物會是token，那麼該token會夾雜著什麼資訊？->->-> `內容通常會是包含誰賦予誰權限、權限為何。`
<!--SR:!2023-02-18,22,250-->

#🧠 在Open Authorization 或者OAuth中，其中Resource Server 將access token轉遞至Authorization Server，驗證成功就做下一步，失敗就回報錯誤，在這裡的驗證方式是什麼？ ->->-> `	- Resource Server 將token轉遞至Authorization Server，驗證成功就做下一步，失敗就回報錯誤，其驗證方式為： - 以JWT 驗證方式來驗證JWT是否被篡改 - 提取JWT的aud值並比對目前所存取的端點是否一樣，若一樣就做下一步，否則報錯 - 提取JWT的scope值並比對目前所要存取的端點之對應動作是否允許，若允許就驗證成功，否則報錯`
<!--SR:!2023-02-24,10,210-->

#🧠 在Open Authorization 或者OAuth中，其中Resource Server 將token轉遞至Authorization Server，驗證成功就做下一步，失敗就回報錯誤，在這裡的驗證方式會是比對Client所提供的aud和scope是否正確，具體會是拿什麼比對？更準確的說，拿什麼比對aud和scope會較為信任 ->->-> `由Resource Server提供Client對於想存取的端點以及對對應端點想做的操作`
<!--SR:!2023-02-23,24,250-->

#🧠 在Open Authorization 或者OAuth的Client-Server中，會有什麼用語？ ->->-> `Resource Server、Authorization Server、Client、Resource Owner`
<!--SR:!2023-02-23,26,250-->

#🧠 在Open Authorization 或者OAuth的Client-Server中，Resource Server、Authorization Server、Client、Resource Owner各為什麼意思？ ->->-> `Resource Server：Resource Server：管理資源、看本身能不能驗證Token，若不能的話就轉遞請求封包上的token至authorization server的伺服器，否則就自己驗證Token。 Authorization Server：驗證Resource Owner輸入的credential來發放Token 、幫忙Resource Server驗證token是否為合法  - Client：以發放的Token來向Resource Server索要指定資源 - Client 相對於Resource Server的稱呼- Resource Owner：在Resource Server上實際擁有資源的人`
<!--SR:!2023-02-15,20,250-->

#🧠 在Open Authorization 或者OAuth的Client-Server中，Resource Server、Authorization Server 對應的Client 會是什麼？  ->->-> `會是代表使用者User的應用程式或者服務`
<!--SR:!2023-03-11,28,230-->

#🧠 在Open Authorization 或者OAuth的Client-Server中，Resource Server會有什麼樣的業務，請說明可能性？ ->->-> `Resource Server：管理資源、看本身能不能驗證Token，若不能的話就轉遞請求封包上的token至authorization server的伺服器，否則就自己驗證Token`
<!--SR:!2023-02-26,26,250-->

#🧠 在Open Authorization 或者OAuth的Client-Server中，若Resource Server只會管理資源，那麼Resource Server會有什麼樣的業務 ->->-> `esource Server：管理資源、若不能的話就轉遞請求封包上的token至authorization server的伺服器`
<!--SR:!2023-02-21,22,250-->

#🧠 在Open Authorization 或者OAuth的Client-Server中，若Resource會管理資源和驗證Token，那麼Resource Server會有什麼樣的業務->->-> `Resource Server：管理資源、看本身能不能驗證Token，若不能的話就轉遞請求封包上的token至authorization server的伺服器，否則就自己驗證Token`
<!--SR:!2023-02-17,19,250-->



#🧠 在Open Authorization 或者OAuth的Client-Server中，Client 和 Resource Owner 之間的差別。 ->->-> `Resource Owner 是代表擁有特定資源的擁有人或者使用者，而Client則是應用程式或者服務，會被授與Resource Owner擁有資源的權利來存取對應資源`
<!--SR:!2023-04-02,48,250-->

#🧠 在Open Authorization 或者OAuth的Client-Server中，其流程會是什麼？ ->->-> `	- 由Resource Owner 輸入credential至 Authorization Server 來做驗證，成功就做下一步，失敗就回報錯誤 - Authorization Server發送token給予Resource Owner - 由Resource Owner賦予token至Client - 由Client夾雜token來向Resource Server 發送請求以此代表Resource Owner發送 - Resource Server 將token轉遞至Authorization Server，驗證成功就做下一步，失敗就回報錯誤 - Resource Server 將指定Resource傳遞給Client使用`
<!--SR:!2023-02-18,21,250-->

#🧠 在Open Authorization 或者OAuth的Client-Server中，若Client 獲取到token並向著Resource Server發送索要資料的請求，那麼Resource Server接收到會做什麼？ ->->-> `轉遞請求封包上的token至authorization server的伺服器`
<!--SR:!2023-03-22,41,250-->

#🧠 在Open Authorization 或者OAuth的Client-Server中，Authorization Server會負責什麼？ ->->-> `驗證Resource Owner輸入的credential來發放Token 、幫忙Resource Server驗證token是否為合法`
<!--SR:!2023-02-26,28,250-->

#🧠 在Open Authorization 或者OAuth的Client-Server中，Resource Server會負責什麼？ ->->-> `管理資源、轉遞請求封包上的token至authorization server的伺服器`
<!--SR:!2023-02-19,23,250-->


#🧠 在Open Authorization 或者OAuth的Client-Server中，Resource Server和Authorization Server 之間差別是什麼？ ->->-> `- Resource Server：管理資源、轉遞請求封包上的token至authorization server的伺服器 - Authorization Server：驗證Resource Owner輸入的credential來發放Token 、幫忙Resource Server驗證token是否為合法`
<!--SR:!2023-02-15,20,250-->

#🧠 在Open Authorization 或者OAuth的Client-Server中，Resource Server vs  Authorization Server 兩者在實現上是否能一台主機擔任兩個角色？ ->->-> `實作上，可以是1. 可以同時是Resource Server 和 Authorization Server 2. 可以分出兩種伺服器：一個是Resource Server、另一個為Authorization Server`
<!--SR:!2023-04-03,48,250-->

#🧠 在Open Authorization 或者OAuth的Client-Server中，其流程會是什麼？以圖來表示？->->-> ``
<!--SR:!2023-02-24,26,250-->




---
Status: #🌱 
Tags:
[[Authentication]] - [[Authorization]]
Links:
[[authentication 是指特定事物被驗證是對、正確、合法事物之過程；authorization 是指授與權力給特定事物去做特定事情之過程]]
References:
[[@auth0ValidateAccessTokens]]
[[@OAuth2023]]
[[@OpenIDConnectShiShiMo]]