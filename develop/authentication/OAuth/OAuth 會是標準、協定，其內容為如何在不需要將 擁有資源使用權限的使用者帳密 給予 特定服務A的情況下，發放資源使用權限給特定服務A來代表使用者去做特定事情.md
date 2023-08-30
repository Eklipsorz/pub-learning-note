## 描述



### OAuth 是什麼？

[[@OAuth2023]]

> OAuth (short for "Open Authorization") is an open standard for access delegation, commonly used as a way for internet users to grant websites or applications access to their information on other websites but without giving them the passwords

> This mechanism is used by companies such as Amazon, Google, Facebook, Microsoft, and Twitter to permit the users to share information about their accounts with third-party applications or websites.

> Generally, OAuth provides clients a "secure delegated access" to server resources on behalf of a resource owner. It specifies a process for resource owners to authorize third-party access to their server resources without providing credentials.

重點：
- OAuth 完整名稱為：Open Authorization
- OAuth：
	- 屬於標準、協定
	- 定義如何在不需要將 "擁有資源使用權限的使用者帳密" 給予 特定服務A的情況下，發放資源使用權限給特定服務A來代表使用者去做特定事情：
		- 具體則是
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


[[@LiJieOAuthRuanYiFengDeWangLuoRiZhi]]

> 在详细讲解OAuth 2.0之前，需要了解几个专用名词。它们对读懂后面的讲解，尤其是几张图，至关重要。

> （1） **Third-party application**：第三方应用程序，本文中又称"客户端"（client），即上一节例子中的"云冲印"。
> 
> （2）**HTTP service**：HTTP服务提供商，本文中简称"服务提供商"，即上一节例子中的Google。
> 
> （3）**Resource Owner**：资源所有者，本文中又称"用户"（user）。
> 
> （4）**User Agent**：用户代理，本文中就是指浏览器。
> 
> （5）**Authorization server**：认证服务器，即服务提供商专门用来处理认证的服务器。
> 
> （6）**Resource server**：资源服务器，即服务提供商存放用户生成的资源的服务器。它与认证服务器，可以是同一台服务器，也可以是不同的服务器。


重點：
- OAuth 在Client-Server之間中，會有以下用語：
	- Client：以發放的Token來向Resource Server索要指定資源
		- Client 相對於Resource Server的稱呼
	- Resource Owner：在Resource Server上實際擁有資源的人
	- User Agent：代理使用者來使用特定服務的程式模組，在這裡會是指瀏覽器
	- HTTP service： HTTP 服務提供商 或者 提供API的服務供應商，主要會由Resource Server 和 Authorization Server來組成
		- Resource Server：管理資源、看本身能不能驗證Token，若不能的話就轉遞請求封包上的token至authorization server的伺服器，否則就自己驗證Token
		- Authorization Server：驗證Resource Owner輸入的credential來發放Token 、幫忙Resource Server驗證token是否為合法
####  Resource Server vs  Authorization Server 兩者是否相同
1. 可以同時是Resource Server 和 Authorization Server
2. 可以分出兩種伺服器：一個是Resource Server、另一個為Authorization Server


### OAuth 的 思路

> OAuth在"客户端"与"服务提供商"之间，设置了一个授权层（authorization layer）。"客户端"不能直接登录"服务提供商"，只能登录授权层，以此将用户与客户端区分开来。"客户端"登录授权层所用的令牌（token），与用户的密码不同。用户可以在登录的时候，指定授权层令牌的权限范围和有效期。

> "客户端"登录授权层以后，"服务提供商"根据令牌的权限范围和有效期，向"客户端"开放用户储存的资料。


重點：
- 讓特定應用程式A(客戶端)和服務提供商之間設定一個授權層，並只提供這種方式來讓客戶端進行登入和獲取資源，服務提供商拿著代表使用者特定權限的資料-token來登入授權層並獲取服務提供商的資源。
	- 授權層不接受特定身份的帳密來驗證，僅接受token來做驗證和授權
- token會是由使用者來發放給特定應用程式A，並由它決定其權限範疇和有效期，好讓授權層依據權限範疇和有效期來安全存取服務提供商的資源


![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1679061043/blog/OAuth/OAuth-Simple-Concept_vrcj0d.png)



### OAuth 的基本執行流程
> ## 四、运行流程

> OAuth 2.0的运行流程如下图，摘自RFC 6749。

![OAuth运行流程](https://www.ruanyifeng.com/blogimg/asset/2014/bg2014051203.png)

> （A）用户打开客户端以后，客户端要求用户给予授权。
> 
> （B）用户同意给予客户端授权。
> 
> （C）客户端使用上一步获得的授权，向认证服务器申请令牌。
> 
> （D）认证服务器对客户端进行认证以后，确认无误，同意发放令牌。
> 
> （E）客户端使用令牌，向资源服务器申请获取资源。
> 
> （F）资源服务器确认令牌无误，同意向客户端开放资源。

> 不难看出来，上面六个步骤之中，B是关键，即用户怎样才能给于客户端授权。有了这个授权以后，客户端就可以获取令牌，进而凭令牌获取资源。


重點：
- OAuth 概念 的 基本實現會有的執行流程：當使用者要授權給應用程式A來獲取Resource Server的服務時
	- 使用者打開特定應用程式A (Client) ，應用程式A要求使用者給予授權
	- 使用者同意並給予授權資料至應用程式A
	- 客戶端使用上一個獲取到的授權資料來向Authorization Server申請token
	- Authorization Server認證授權資料並確認無誤，就發放其token
	- 客戶端使用token來向Resource Server來申請獲取資源
	- Resource Server 確認token 無誤就發放資源給客戶端
- 在這裡 **使用者同意並給予授權資料至應用程式A** 由於Resource Server/Authorization Server無法識別出該授權資料會是合法的使用者提供的？以及其內容是否合法？，因此不能貿然以該資料來發放token，必須得用一些值得信任的方式來識別並發放，所以具體有以下方法：


#### 實際擁有的授權方式

[[@LiJieOAuthRuanYiFengDeWangLuoRiZhi]]
> 客户端必须得到用户的授权（authorization grant），才能获得令牌（access token）。OAuth 2.0定义了四种授权方式。

> -   授权码模式（authorization code）
> -   简化模式（implicit）
> -   密码模式（resource owner password credentials）
> -   客户端模式（client credentials）

基本上會有四種授權方式：
1. authorization code grant type
2. implicit grant type
3. resource owner password credentials grant type
4. client credentials grant type


#### 不論哪一種，server驗證access token的方式

不論哪一種，Resource Server 或者 幫助Resource Server 來驗證Token是否合法時，其驗證方式為：
- 以JWT 驗證方式來驗證JWT是否被篡改
- 提取JWT的aud值並比對目前所存取的端點(由Resource Server提供Client想要存取的端點)是否一樣，若一樣就做下一步，否則報錯
- 提取JWT的scope值並比對目前所要存取的端點之對應動作(由Resource Server提供Client於存取端點想做的操作)是否允許，若允許就驗證成功，否則報錯


#### response_type vs. grant_type


response_type會是指甚麼意思?  ->->-> `客戶端指定Owner導向至認證伺服器所要獲得的授權同意形式會是甚麼?`
<!--SR:!2023-09-08,13,242-->

grant_type會是指甚麼意思? ->->-> `grant_type: 客戶端要以甚麼樣的授權同意形式來向認證伺服器索要TOKEN`
<!--SR:!2023-09-08,13,242-->



## 複習

#🧠 OAuth 完整名稱是什麼？ ->->-> `Open Authorization`
<!--SR:!2023-10-22,171,250-->

#🧠 OAuth 完整名稱是Open Authentication 嗎？為什麼？ ->->-> `不是，會是Open Authorization`
<!--SR:!2024-06-03,301,250-->

#🧠 Open Authorization 或者OAuth 會是什麼？ ->->-> `一種標準、協定。定義如何在不需要將 "擁有資源使用權限的使用者帳密" 給予 特定服務A的情況下，發放資源使用權限給特定服務A來代表使用者去做特定事情。`
<!--SR:!2023-10-25,60,230-->


#🧠 在Open Authorization 或者OAuth中，代表權限的事物會是什麼？ ->->-> `token`
<!--SR:!2023-10-30,179,250-->




#🧠 在Open Authorization 或者OAuth中，代表權限的事物會是token，那麼該token會夾雜著什麼資訊？->->-> `內容通常會是包含誰賦予誰權限、權限為何。`
<!--SR:!2023-09-22,155,250-->

#🧠 在Open Authorization 或者OAuth中，其中Resource Server 將access token轉遞至Authorization Server，驗證成功就做下一步，失敗就回報錯誤，在這裡的驗證方式是什麼？ ->->-> `	- Resource Server 將token轉遞至Authorization Server，驗證成功就做下一步，失敗就回報錯誤，其驗證方式為： - 以JWT 驗證方式來驗證JWT是否被篡改 - 提取JWT的aud值並比對目前所存取的端點是否一樣，若一樣就做下一步，否則報錯 - 提取JWT的scope值並比對目前所要存取的端點之對應動作是否允許，若允許就驗證成功，否則報錯`
<!--SR:!2023-09-15,40,170-->

#🧠 在Open Authorization 或者OAuth中，其中Resource Server 將token轉遞至Authorization Server，驗證成功就做下一步，失敗就回報錯誤，在這裡的驗證方式會是比對Client所提供的aud和scope是否正確，具體會是拿什麼比對？更準確的說，拿什麼比對aud和scope會較為信任 ->->-> `由Resource Server提供Client對於想存取的端點以及對對應端點想做的操作`
<!--SR:!2023-10-31,176,250-->

#🧠 在Open Authorization 或者OAuth的Client-Server中，會有什麼用語？ ->->-> `Resource Server、Authorization Server、Client、Resource Owner`
<!--SR:!2023-11-08,181,250-->

#🧠 在Open Authorization 或者OAuth的Client-Server中，Resource Server、Authorization Server、Client、Resource Owner各為什麼意思？ ->->-> `Resource Server：Resource Server：管理資源、看本身能不能驗證Token，若不能的話就轉遞請求封包上的token至authorization server的伺服器，否則就自己驗證Token。 Authorization Server：驗證Resource Owner輸入的credential來發放Token 、幫忙Resource Server驗證token是否為合法  - Client：以發放的Token來向Resource Server索要指定資源 - Client 相對於Resource Server的稱呼- Resource Owner：在Resource Server上實際擁有資源的人`
<!--SR:!2024-07-06,322,250-->

#🧠 在Open Authorization 或者OAuth的Client-Server中，Resource Server、Authorization Server 對應的Client 會是什麼？  ->->-> `會是代表使用者User的應用程式或者服務`
<!--SR:!2023-11-07,167,230-->

#🧠 在Open Authorization 或者OAuth的Client-Server中，Resource Server會有什麼樣的業務，請說明可能性？ ->->-> `Resource Server：管理資源、看本身能不能驗證Token，若不能的話就轉遞請求封包上的token至authorization server的伺服器，否則就自己驗證Token`
<!--SR:!2023-10-23,170,250-->

#🧠 在Open Authorization 或者OAuth的Client-Server中，若Resource Server只會管理資源，那麼Resource Server會有什麼樣的業務 ->->-> `esource Server：管理資源、若不能的話就轉遞請求封包上的token至authorization server的伺服器`
<!--SR:!2023-09-23,155,250-->

#🧠 在Open Authorization 或者OAuth的Client-Server中，若Resource會管理資源和驗證Token，那麼Resource Server會有什麼樣的業務->->-> `Resource Server：管理資源、看本身能不能驗證Token，若不能的話就轉遞請求封包上的token至authorization server的伺服器，否則就自己驗證Token`
<!--SR:!2024-07-25,334,250-->

#🧠 在Open Authorization中，response_type會是指甚麼意思?  ->->-> `客戶端指定Owner導向至認證伺服器所要獲得的授權同意形式會是甚麼?`
<!--SR:!2023-09-08,13,242-->
<!--SR:!2023-08-21,2,242-->


#🧠 在Open Authorization中，grant_type會是指甚麼意思?->->-> `grant_type: 客戶端要以甚麼樣的授權同意形式來向認證伺服器索要TOKEN`
<!--SR:!2023-09-07,12,242-->


#🧠 在Open Authorization 或者OAuth的Client-Server中，Client 和 Resource Owner 之間的差別。 ->->-> `Resource Owner 是代表擁有特定資源的擁有人或者使用者，而Client則是應用程式或者服務，會被授與Resource Owner擁有資源的權利來存取對應資源`
<!--SR:!2024-06-17,309,250-->



#🧠 在Open Authorization 或者OAuth的Client-Server中，若Client 獲取到token並向著Resource Server發送索要資料的請求，那麼Resource Server接收到會做什麼？ ->->-> `轉遞請求封包上的token至authorization server的伺服器`
<!--SR:!2024-06-14,306,250-->

#🧠 在Open Authorization 或者OAuth的Client-Server中，Authorization Server會負責什麼？ ->->-> `驗證Resource Owner輸入的credential來發放Token 、幫忙Resource Server驗證token是否為合法`
<!--SR:!2023-11-20,189,250-->

#🧠 在Open Authorization 或者OAuth的Client-Server中，Resource Server會負責什麼？ ->->-> `管理資源、轉遞請求封包上的token至authorization server的伺服器`
<!--SR:!2023-10-05,163,250-->


#🧠 在Open Authorization 或者OAuth的Client-Server中，Resource Server和Authorization Server 之間差別是什麼？ ->->-> `- Resource Server：管理資源、轉遞請求封包上的token至authorization server的伺服器 - Authorization Server：驗證Resource Owner輸入的credential來發放Token 、幫忙Resource Server驗證token是否為合法`
<!--SR:!2023-11-02,68,230-->

#🧠 在Open Authorization 或者OAuth的Client-Server中，Resource Server vs  Authorization Server 兩者在實現上是否能一台主機擔任兩個角色？ ->->-> `實作上，可以是1. 可以同時是Resource Server 和 Authorization Server 2. 可以分出兩種伺服器：一個是Resource Server、另一個為Authorization Server`
<!--SR:!2024-01-30,177,230-->

#🧠 OAuth 的授權思路會是什麼？請以特定應用程式(客服端), 服務提供商和授權層來說明 ->->-> `讓特定應用程式A(客戶端)和服務提供商之間設定一個授權層，並只提供這種方式來讓客戶端進行登入和獲取資源，服務提供商拿著代表使用者特定權限的資料-token來登入授權層並獲取服務提供商的資源。`
<!--SR:!2023-10-25,55,207-->


#🧠 OAuth 的授權思路會是什麼？其中讓特定應用程式A(客戶端)和服務提供商之間設定一個授權層，授權層會只接受什麼？面向於誰 ->->-> `僅面向於應用程式A，只接受於token來透過它獲取服務提供商的資源`
<!--SR:!2024-03-15,209,247-->

#🧠  OAuth 的 token 中的權限和有效期會是由誰來決定 ->->-> `通常是由授予權限的使用者來決定或者其發放token的server來決定`
<!--SR:!2024-01-15,153,207-->


#🧠 OAuth 的授權思路會是什麼？請以特定應用程式(客服端), 授權伺服器, 和授權層級，請畫圖來說明->->-> ![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1679061043/blog/OAuth/OAuth-Simple-Concept_vrcj0d.png)
<!--SR:!2023-11-12,131,227-->

#🧠 OAuth 概念 的 基本實現會有的執行流程，就以 **當使用者要授權給應用程式A來獲取Resource Server的服務時** 來說 ->->-> `	- 使用者打開特定應用程式A (Client) ，應用程式A要求使用者給予授權 - 使用者同意並給予授權資料至應用程式A - 客戶端使用上一個獲取到的授權資料來向Authorization Server申請token - Authorization Server認證授權資料並確認無誤，就發放其token - 客戶端使用token來向Resource Server來申請獲取資源 - Resource Server 確認token 無誤就發放資源給客戶端`
<!--SR:!2024-02-07,174,226-->


#🧠 OAuth 概念 的 基本實現會有的流程，就以 **當使用者要授權給應用程式A來獲取Resource Server的服務時** 來說，請畫圖來說明 ->->-> ``
<!--SR:!2024-03-05,205,247-->



#🧠 針對OAuth 概念 所實現的基本流程中，其中會有客戶端詢問使用者獲取授權同意的手段並以授權來申請使用resource server，普遍來說， 授權同意會不會具有一些安全性疑慮？有的話，會是什麼？ ->->-> `由於Resource Server/Authorization Server無法識別出該授權資料會是合法的使用者提供的？以及其內容是否合法？，因此不能貿然以該資料來發放token，必須得用一些值得信任的方式來識別並發放`
<!--SR:!2023-09-30,35,225-->



#🧠 OAuth 概念下的實際會有授權方式會有哪四種？ ->->-> `authorization code、implicit、resource owner password credentials、client credentials`
<!--SR:!2024-03-06,196,227-->


#🧠 OAuth 概念下的實際會有授權方式會有哪四種，其中不論哪一種，哪一個server會負責驗證客戶端傳過來的token？->->-> `resource server 或者 由resource server轉發token至authorization server來驗證`
<!--SR:!2023-10-14,49,227-->

#🧠 OAuth 概念下的實際會有授權方式會有四種，其中不論哪一種，server驗證access token是否為合法的方式為何？在這裡假定使用JWT來表示token->->-> `- 以JWT 驗證方式來驗證JWT是否被篡改 - 提取JWT的aud值並比對目前所存取的端點(由Resource Server提供Client想要存取的端點)是否一樣，若一樣就做下一步，否則報錯 - 提取JWT的scope值並比對目前所要存取的端點之對應動作(由Resource Server提供Client於存取端點想做的操作)是否允許，若允許就驗證成功，否則報錯
<!--SR:!2023-12-04,154,247-->
`

#🧠 User Agent 在網頁上會泛指什麼？ ->->-> `會是指代理使用者來獲取/發送對於網頁請求的程式模組，如瀏覽器`
<!--SR:!2024-04-18,240,247-->


---
Status: #🌱 
Tags:
[[Authentication]] - [[Authorization]]
Links:
[[authentication 是指特定事物被驗證是對、正確、合法事物之過程；authorization 是指授與權力給特定事物去做特定事情之過程]]
References:
[[@auth0ValidateAccessTokens]]
[[@OAuth2023]]
[[@LiJieOAuthRuanYiFengDeWangLuoRiZhi]]