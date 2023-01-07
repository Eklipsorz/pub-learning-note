## 描述


###

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

### OAuth 2.0 角色
[[@OpenIDConnectShiShiMo]]
> Access Token 就像是一張兌換卷，每一張 Access Token 上都有寫**「誰」「對誰」「給予什麼樣的權限」**，如此一來就可以在不告訴對方帳號密碼的情況下，給予對方最低限度需要的權限。這就是為什麼 OAuth 2.0 被稱為是一個授權的協議。

![](https://hennge.com/tw/blog/1_vL6Fi0RFSHvtxkkDQKAr9w.png)

> 在 OAuth 2.0 的世界中，我這個使用者被稱為 Resource Owner；第三方行事曆服務被稱之為 Client；有放我行事曆資訊的 Google Calendar 稱為 Resource Server；幫忙發 Access Token 的伺服器稱之為 Authorization Server，在這例子中就會是 Google。

重點：
- OAuth 在Client-Server之間中，會有以下用語：
	- Resource Server：儲存資源的伺服器
	- Authorization Server：


## 複習


---
Status: #🌱 
Tags:
[[Authentication]]
Links:
[[authentication 是指特定事物被驗證是對、正確、合法事物之過程；authorization 是指授與權力給特定事物去做特定事情之過程]]
References:
[[@OAuth2023]]
[[@OpenIDConnectShiShiMo]]