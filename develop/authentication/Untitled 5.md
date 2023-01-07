
## 描述


###

[[@OpenIDWikipedia]]
> OpenID is an open standard and decentralized authentication protocol promoted by the non-profit OpenID Foundation. 
> 
> It allows users to be authenticated by co-operating sites (known as relying parties, or RP) using a third-party identity provider (IDP) service, eliminating the need for webmasters to provide their own ad hoc login systems, and allowing users to log in to multiple unrelated websites without having to have a separate identity and password for each.[1] 
> 
> Users create accounts by selecting an OpenID identity provider,[1] and then use those accounts to sign on to any website that accepts OpenID authentication. Several large organizations either issue or accept OpenIDs on their websites

> OpenID Connect (OIDC)

> Published in February 2014 by the OpenID Foundation, OpenID Connect is the third generation of OpenID technology. It is an authentication layer on top of the [OAuth 2.0](https://en.wikipedia.org/wiki/OAuth#OAuth_2.0 "OAuth") authorization framework


[[@IBMDocumentation2022]]
> OpenID Connect 是一種簡式身分通訊協定和開放式標準，以 OAuth 2.0 通訊協定為建置基礎，可讓用戶端應用程式根據「OpenID Connect 提供者」執行的鑑別，來驗證使用者的身分。

> OpenID Connect 使用 OAuth 2.0 來進行鑑別和授權，然後建置用來唯一識別使用者的身份

重點：
- OpenID 是一個開放式協定和標準，定義如何建構分散式身份認證系統
- 主要在特定應用服務A上可用第三方認證服務來進行身份認證，以此消除應用服務本身對於認證的建構需求以及使用第三方認證服務來認證：
	- 若認證成功，就允許使用應用服務A；若認證失敗，就不允許使用
- 使用者可選擇任意的OpenID identity provider註冊帳號，並且在支援OpenID認證協定的服務上來調用OpenID實現和帳號來登入
- 稱之為分散式是因爲以任意特定應用服務A是拿多個外部伺服器來做認證系統，而非以應用服務A內部來建立認證系統

- OpenID Connect 標準是 OpenID 2.0 標準的下一代標準：
	- 主要以OAuth 2.0協定作為基礎來做驗證和權限分發，權限分發會是以token為表示來分發。

#### OpenID Connect vs. OpenID
[[@AuthenticationWhenYou]]
> OpenID Connect improved naming and structure of `OpenID 2.0` fields and parameters in order to be easier to use. I can easily read the `OpenID Connect` specification and understand what all the values are used for and what to set them to, but trying to read the `OpenID 2.0` specification is a bit more difficult and convoluted.

> At this point the choice is easy, `OpenID 2.0` is deprecated. You should use `OpenID Connect`.





### OpenID Connect 角色

[[@OpenIDConnectShiShiMo]]
>  從 OAuth 2.0 到 OpenID Connect

> 但是解決了一個問題，新的問題就又跑出來了。

> 因為 OAuth 2.0 的便利性，就出現了很多將 OAuth 2.0 用為使用者登入驗證方式的服務。 但大家千萬不能忘記 OAuth 2.0 只是一個定義如何使用 Access Token 來授權的協議，內容是沒有提到如何去認證一個使用者的登入。因此如果使用 OAuth 2.0 做為使用者登入的認證機制，就會有很多意想不到的[資安問題](http://www.thread-safe.com/2012/01/problem-with-oauth-for-authentication.html)發生。而再次的有人想出了一個在現有 OAuth 2.0 的協議基礎下發放 ID Token 的方法來解決這個問題，這就是我們今天的主題所討論的 OpenID Connect。

> ## 重新介紹今天的主角 -- OpenID Connect

![](https://hennge.com/tw/blog/1_SQQwKPMtjPJbUKP2Z0R_Aw.png)

> 因為 OpenID Connect 是以 OAuth 2.0 為基礎設計，因此使用方法上有很多的相似處。角色也是其中一個，只是在 OpenID Connect 中的 Client 有了一個新稱呼叫 Relying Party。Authorization Server 的新稱呼為 OpenID Provider，它除了可以發放 Access Token 外，同時也可以發放 ID Token。

[[@RelyingParty2022]]
> An identity provider (abbreviated IdP or IDP) is a system entity that creates, maintains, and manages identity information for principals and also provides authentication services to relying applications within a federation or distributed network



重點：
- OpenID / OpenID Connect 角色：
	- Replying Party：
	- OpenID Provider / OpenID identity Provider：負責

## 複習
#🧠 Question :: ->->-> ``

---
Status: 
Tags:
[[Authentication]] - [[Authorization]]
Links:
References:
[[@OpenIDWikipedia]]
[[@IBMDocumentation2022]]
[[@AuthenticationWhenYou]]
[[@OpenIDConnectShiShiMo]]
[[@RelyingParty2022]]