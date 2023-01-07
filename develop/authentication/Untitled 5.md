
## 描述





### OpenID Connect 角色

[[@OpenIDConnectShiShiMo]]
>  從 OAuth 2.0 到 OpenID Connect

> 但是解決了一個問題，新的問題就又跑出來了。

> 因為 OAuth 2.0 的便利性，就出現了很多將 OAuth 2.0 用為使用者登入驗證方式的服務。 但大家千萬不能忘記 OAuth 2.0 只是一個定義如何使用 Access Token 來授權的協議，內容是沒有提到如何去認證一個使用者的登入。因此如果使用 OAuth 2.0 做為使用者登入的認證機制，就會有很多意想不到的[資安問題](http://www.thread-safe.com/2012/01/problem-with-oauth-for-authentication.html)發生。而再次的有人想出了一個在現有 OAuth 2.0 的協議基礎下發放 ID Token 的方法來解決這個問題，這就是我們今天的主題所討論的 OpenID Connect。

> ## 重新介紹今天的主角 -- OpenID Connect

![](https://hennge.com/tw/blog/1_SQQwKPMtjPJbUKP2Z0R_Aw.png)

> 因為 OpenID Connect 是以 OAuth 2.0 為基礎設計，因此使用方法上有很多的相似處。角色也是其中一個，只是在 OpenID Connect 中的 Client 有了一個新稱呼叫 Relying Party。Authorization Server 的新稱呼為 OpenID Provider，它除了可以發放 Access Token 外，同時也可以發放 ID Token。


## 複習
#🧠 Question :: ->->-> ``

---
Status: 
Tags:
[[Authentication]] - [[Authorization]]
Links:
References:
[[@OpenIDConnectShiShiMo]]