
## 描述


### OpenID 背景

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
- OpenID 是一個開放式協定和標準，定義特定應用服務A如何與分散式身份認證系統進行認證
- 主要在特定應用服務A上可用第三方認證服務來進行身份認證，以此消除應用服務內部的認證開發需求：
	- 若認證成功，就允許使用應用服務A；若認證失敗，就不允許使用
- 使用者可選擇任意的OpenID identity provider註冊帳號，並且在支援OpenID認證協定的服務上來調用OpenID實現和帳號來登入
- 稱之為分散式是因爲以任意特定應用服務A是拿多個外部伺服器來做認證系統，而非集中在應用服務A內部來建立認證系統

- OpenID Connect 標準是 OpenID 2.0 標準的下一代標準：
	- 主要以OAuth 2.0協定作為基礎來做身份驗證和權限分發，身份和權限分發會是以token為表示來分發。

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


[[@AuthenticationRelyingParty]]
> The spec seems to call the identity provider "OpenID Provider" or "OP" representing the authorization server that issues tokens and verifies credentials of users and clients

> The relying party is the client--the app that relies on the tokens and credential-validation of the OP


重點：
- OpenID / OpenID Connect 角色：
	- Replying Party：主要依賴token和token夾雜的身分證明資料和權限來向Resource Server獲取資源來加以應用的應用程式或者服務
	- OpenID Provider / OpenID identity Provider / Authorization Server：負責註冊合法使用者、驗證使用者所輸入的內容並發放token、協助Resource Server做token的驗證，發放的token種類可以是id token、access token。
	- Resource Server：管理資源、根據是否會驗證Token來決定，若不會驗證就將請求封包的token轉遞至Authorization Server來驗證的伺服器，若會驗證，就自行驗證Token

## 複習

#🧠 OpenID 是什麼？ ->->-> `是一個協定、標準，定義特定應用服務A如何與分散式身份認證系統進行認證`
<!--SR:!2023-07-03,101,247-->

#🧠 OpenID 是一個開放式協定和標準，定義特定應用服務A如何與分散式身份認證系統進行認證，為何要定義應用服務與分散式認證系統認證？->->-> `主要在特定應用服務A上可用第三方認證服務來進行身份認證，以此消除應用服務內部的認證開發需求`
<!--SR:!2023-05-17,75,250-->

#🧠 OpenID 是一個開放式協定和標準，主要在特定應用服務A上可用第三方認證服務來進行身份認證，以此消除應用服務內部的認證開發需求，具體的話，認證成與敗會是？->->-> `若認證成功，就允許使用應用服務A；若認證失敗，就不允許使用`
<!--SR:!2023-05-29,76,230-->

#🧠 OpenID 是一個開放式協定和標準，定義特定應用服務A如何與分散式身份認證系統進行認證，具體如何讓特定服務A的認證需求如同前面所說的那樣？ ->->-> `使用者可選擇任意的OpenID identity provider註冊帳號，並且在支援OpenID認證協定的服務上來調用OpenID實現和帳號來登入`
<!--SR:!2023-09-26,134,209-->

#🧠 OpenID 是一個開放式協定和標準，定義特定應用服務A如何與分散式身份認證系統進行認證，其中稱之為分散式是由於 ->->-> `是因爲以任意特定應用服務A是拿多個外部伺服器來做認證系統，而非集中在應用服務A內部來建立認證系統`
<!--SR:!2023-07-04,97,227-->

#🧠 OpenID Connect 標準是什麼？ ->->-> `主要是OpenID 2.0 標準的下一代`
<!--SR:!2023-07-06,78,230-->

#🧠 OpenID Connect 標準是OpenID 2.0 標準的下一代，其具體為？ ->->-> `主要以OAuth 2.0協定作為基礎來做身份驗證和權限分發，身份和權限分發會是以token為表示來分發。`
<!--SR:!2023-08-12,98,208-->

#🧠 OpenID / OpenID Connect 角色會有哪些？->->-> `Replying Party、OpenID Provider / OpenID identity Provider、Resource Server`
<!--SR:!2023-10-17,51,230-->

#🧠 在OpenID / OpenID Connect 角色中，其中Replying Party會是什麼？ ->->-> `主要依賴token和token夾雜的身分證明資料和權限來向Resource Server獲取資源來加以應用的應用程式或者服務`
<!--SR:!2023-11-01,179,250-->

#🧠 在OpenID / OpenID Connect 角色中，其中OpenID Provider / OpenID identity Provider / Authorization Server會是什麼？ ->->-> `負責註冊合法使用者、驗證使用者所輸入的內容並發放token、協助Resource Server做token的驗證，發放的token種類可以是id token、access token`
<!--SR:!2024-02-11,234,248-->

#🧠 在OpenID / OpenID Connect 角色中，其中Resource Server會是負責什麼？說明可能性->->-> ` Resource Server：管理資源、根據是否會驗證Token來決定，若不會驗證就將請求封包的token轉遞至Authorization Server來驗證的伺服器，若會驗證，就自行驗證Token`
<!--SR:!2024-02-10,228,245-->


#🧠 在OpenID / OpenID Connect 角色中，若Resource Server只會管理資源，其中Resource Server會是負責什麼？ ->->-> `Resource Server：管理資源、根據是否會驗證Token來決定，若不會驗證就將請求封包的token轉遞至Authorization Server來驗證的伺服器`
<!--SR:!2024-01-22,203,225-->

#🧠 在OpenID / OpenID Connect 角色中，若Resource Server會管理資源和驗證token，其中Resource Server會是負責什麼？ ->->-> ` Resource Server：管理資源、根據是否會驗證Token來決定，若不會驗證就將請求封包的token轉遞至Authorization Server來驗證的伺服器，若會驗證，就自行驗證Token`
<!--SR:!2023-10-16,51,225-->




#🧠 OpenID Connect 的 authorization server / OpenID Identity Provider 所能給予的token種類為何？ ->->-> `id token、access token`
<!--SR:!2023-05-25,81,250-->


#🧠 OpenID Connect 角色和OAuth 角色對應會是什麼，如驗證、資源、客戶端 ->->-> `客戶端應用程式：OAuth 為 client；OpenID Connect 為 Replying Party。驗證：OAuth 為 Authorization；OpenID Connect 為 OpenID Provider/OpenID identity Provider。資源則都是Resource Server`
<!--SR:!2023-05-14,74,250-->




---
Status: #🌱 
Tags:
[[Authentication]] - [[Authorization]] - [[OpenID-Connect]]
Links:
[[JWT 的  audience 在 JWT上是表明目前JWT 適用於哪個對象才能合法使用該JWT。 在ID token的情況下，是特定身分。若在access token的情況下，aud值會是Resource Server之端點]]

References:
[[@OpenIDWikipedia]]
[[@IBMDocumentation2022]]
[[@AuthenticationWhenYou]]
[[@OpenIDConnectShiShiMo]]
[[@RelyingParty2022]]
[[@AuthenticationRelyingParty]]