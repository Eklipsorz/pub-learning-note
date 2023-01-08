## 描述


[[@IDTokenAccess]]
> What Is an ID Token?

> An ID token is an artifact that proves that the user has been authenticated. It was introduced by OpenID Connect (OIDC), an open standard for authentication used by many identity providers such as Google, Facebook, and, of course, Auth0. Check out this document for more details on OpenID Connect. Let's take a quick look at the problem OIDC wants to resolve.


ID token 是一個用來證明使用者是受過認證的資訊，其概念是由OIDC 這個驗證標準。

![](https://images.ctfassets.net/23aumh6u8s0i/4x34jgYBU7vjBYLumNr9Sg/57e0b420de0d27568981af4aef0ab27f/id-token-scenario.png)
> Here, a user with their browser authenticates against an OpenID provider and gets access to a web application.

在這裡，使用者會會透過他們的瀏覽器來對openid provider進行驗證並獲取網頁應用程式的存取權限

> The result of that authentication process based on OpenID Connect is the ID token, which is passed to the application as proof that the user has been authenticated.

基於OpenID Connect的認證程序的結果就是ID token，它會以作為被驗證的使用者證明來轉遞給應用程式

> This provides a very basic idea of what an ID token is: proof of the user's authentication. Let’s see some other details.

這提供一個最基本的id token 概念：
- 使用者身分驗證證明

> An ID token is **encoded as a JSON Web Token** (JWT), a standard format that allows your application to easily inspect its content, and make sure it comes from the expected issuer and that no one else changed it

- id token 是使用JWT 技術來編碼，一個標準格式來允許你的應用程式輕易獲取內部內容並確保token的發行人是誰以及沒有人能夠改變JWT


> To put it simply, an example of ID token looks like this:

```
eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJpc3MiOiJodHRwOi8vbXktZG9tYWluLmF1dGgwLmNvbSIsInN1YiI6ImF1dGgwfDEyMzQ1NiIsImF1ZCI6IjEyMzRhYmNkZWYiLCJleHAiOjEzMTEyODE5NzAsImlhdCI6MTMxMTI4MDk3MCwibmFtZSI6IkphbmUgRG9lIiwiZ2l2ZW5fbmFtZSI6IkphbmUiLCJmYW1pbHlfbmFtZSI6IkRvZSJ9.bql-jxlG9B_bielkqOnjTY9Di9FillFb6IMQINXoYsw
```

> Of course, this isn't readable to the human eye, so you have to decode it to see what content the JWT holds. By the way, the ID token is not encrypted but just Base 64 encoded. You can use one of the many available libraries to decode it, or you can examine it yourself with the jwt.io debugger.


> Without going deeper into the details, the relevant information carried by the ID token above looks like the following:

```json
{ 
  "iss": "http://my-domain.auth0.com", 
  "sub": "auth0|123456", 
  "aud": "1234abcdef", 
  "exp": 1311281970, 
  "iat": 1311280970, 
  "name": "Jane Doe", 
  "given_name": "Jane", 
  "family_name": "Doe"
}
```

> These JSON properties are called **claims**, and they are **declarations about the user** and the token itself. The claims about the user define the user’s identity

這些JSON屬性被稱之claim ，他們是宣告使用者的資訊和token資訊，


aud => token的接收者，會用特定獨特識別字來表示特定使用方，


    Actually, the OpenID Connect specifications don't require the ID token to have user's claims. In its minimal structure, it has no data about the user; just info about the authentication operation.

實際上來說，OpenID Connect 規格書不需要ID token 去擁有使用者的資訊，在最小的token架構中，是token內的資訊是沒有任何有關於使用者資訊，就只是關於驗證操作的資訊。


> One important claim is the aud claim. This claim defines the audience of the token, i.e., the web application that is meant to be the final recipient of the token. In the case of the ID token, its value is the client ID of the application that should consume the token.

最重要的claim是aud claim，這定義token的audience，換言之就是網頁應用程式

在ID token的情況，它的值會是能夠使用這個token的client_id。


    Remember this small detail about the audience claim because it will help you better understand what its correct use is later on.

> The ID token may have additional information about the user, such as their email address, picture, birthday, and so on.


id token 可能擁有額外資訊來包含使用者資訊，如email、圖片、生日。

> Finally, maybe the most important thing: the ID token is signed by the issuer with its private key. This guarantees you the origin of the token and ensures that it has not been tampered with. You can verify these things by using the issuer's public key.

最後：

> Cool! Now you know what an ID token is. But what can you do with an ID token?

> First, it demonstrates that the user has been authenticated by an entity you trust (the OpenID provider) and so you can trust the claims about their identity.


> Also, your application can personalize the user’s experience by using the claims about the user that are included in the ID token. For example, you can show their name on the UI, or display a "best wishes" message on their birthday. The fun part is that you don’t need to make additional requests, so you may get a little gain in performance for your application.





id token：可以拿來做什麼？
1. 由於驗證使用者是合法的實物，所以你可以信任他們所說的事情
2. 你的應用程式可以藉由增加更多使用資訊在token內來替應用者增加使用者體驗，比如你可以在特定UI展現出名字。


重點：
- 使用者或者Relying Party 向OpenID Provider提供特定身份的證明資訊，接著由OpenID Provider對其進行驗證，若驗證成功就會發放對應token來代表其權限和使用者：
	- 若token本身夾雜特定身分證明資訊 和 代表特定資源之使用權限的資訊，那麼就會是同時代表權限和使用者的id token
	- 若token本身只有特定資源之使用權限的資訊，那麼就只能代表權限的access token
- id token夾雜的身分證明資訊會是：
	- client_id：特定身份在OpenID Provider所註冊的id
	- 特定身分對應的email、圖片、生日等個人資料



### id token 構成
[[JSON Web Token 內容分為定義JWT製作和形式的header、夾雜主要內容的payload、驗證是否被人篡改資料的簽署值]]
id token 的構成會是以JWT 的Header、payload、Signature所構成：
	- payload 夾雜著特定身分的驗證資料


#### payload 中的 aud claim

- aud 本身是指audience ，在這裡是用觀眾、聽眾的比喻來描述最後接收到特定資源權限的那一方，通常會是：
	- 若是id token，aud 值會是代表特定身份的識別字，在這裡會是client_id
	- 若是access token，aud 值會是代表relying party所要存取端點之識別字
- aud claim 最主要是進行身份驗證，通常會拿JWT裡頭的aud claim 從openID Provider或者Authorization Server 中找到對應設定，若沒有就失效；若有就繼續生效




### 驗證方式

[[@auth0ValidateIDTokens]]

> If any of these checks fail, the token is considered invalid, and the request must be rejected.

> 1. Validate the JWT.

> 2. Check additional standard claims. If you've performed the standard JWT validation, you have already decoded the JWT's Payload and looked at its standard claims. Additional claims to verify for ID tokens include:
		- Token audience (aud, string): The audience value for the token must match the client ID of the application as defined in your Application's Settings in the Client ID field.
		- Nonce (nonce, string): Passing a nonce in the token request is recommended (required for the Implicit Flow) to help prevent replay attacks. The nonce value in the token must exactly match the original nonce sent in the request. See Mitigate Replay Attacks for details.

重點：
- id token 驗證方式：若有任一步驟失敗，就會將token視為非法
	- 驗證JWT
	- 驗證解碼後的payload，如aud claim，就驗證其值是否還存在Authorization Server或者openID Provider的驗證資料用的空間，還存在就繼續生效；否則失效

####  驗證aud claim 方式
https://juejin.cn/post/7131956073472196621

> 我这里有两种方案：

> 第一种，是颁发token的时候有一个受众人aud ，也就是颁发给谁 ，我们颁发token的时候，每个用户根据 username+pwd+datetime.now() 的规则作为颁发受众人。

> 这样如果更改了用户名或者密码则受众人就会变更，此时的token已经无效了需要刷新token。另外datetime.now()也可以存在缓存或者用户表，当用户退出登录，或者管理员取消其token有效，则只需更改用户的datetime时间即可，受众人发生变更，token无效。后台需配置ValidateAudience = true,进行认证受众人是否一致。

> 第二种，上篇文章提到过payload载体是可以添加自己的逻辑的，那么我们可以赋予一个 version 作为token的版本信息。例如默认正常产生的token版，也可以是当前时间的时间戳，并记录到用户表或者用户缓存。当token被用户强制失效，或者管理员强制失效，则只需更改这个版本信息即可。认证的时候如果发现版本不一致，则token失效。

  
1. 在Authorization Server或者openID Provider 中建立一個表格來儲存，查找是否存在時，就透過客戶端給予的aud claim來從表格找到對應token的aud是否還有原有的aud或者對應token是否存在
```
token | aud
------------
token1  aud1
token1  aud2
```
2. 紀錄特定時間戳作為是版本分別在客戶端空間儲存和JWT儲存，接著拿兩地的時間戳內容進行比對，若一樣就繼續生效；若不一樣就失效，基於這點：
	 - 客戶端若要自行失效，就修改客戶端空間內的時間戳內容
	 - 伺服器若要自行失效，就修改JWT中的時間戳內容

###  claim 命名緣由
claim：
> a statement that something is true or is a fact, although other people might not believe it

重點：
- 以特定角度來說明特定事物是對的描述，但對於其他人來說可能會不相信
## 複習


---
Status: #🌱 
Tags:
[[Authentication]] - [[Authorization]]
Links:
[[authentication 是指特定事物被驗證是對、正確、合法事物之過程；authorization 是指授與權力給特定事物去做特定事情之過程]]
[[JSON Web Token 內容分為定義JWT製作和形式的header、夾雜主要內容的payload、驗證是否被人篡改資料的簽署值]]
References:
[[@IDTokenAccess]]
[[@OpenIDConnectShiShiMo]]
[[@auth0ValidateIDTokens]]
