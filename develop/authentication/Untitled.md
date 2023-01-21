## 描述


### Resource Server 脫離授權認證的可能性

[[@AccessTokenRefresh]]
> ### 资源服务如何脱离授权服务验证Access Token？

> 以JTW为例。如果Access Token是JWT形式签发，资源服务可以使用验证签名的方式判断是否合法，只需要把签名密钥在资源服务同步一份即可。也有使用非对称加密的，授权服务使用私钥签发，资源服务使用公钥验证。由于JWT允许携带一些信息，用户，权限，有效期等，因此资源服务判断JWT合法之后可以继续根据携带信息来判断是否可访问资源。仅此而已，这样的好处是可以快速验证有效性，坏处是Access Token一旦签发，将很难收回，只能通过过期来失效。

重點：
- 由於授權的發送會是以JWT製成的token，其JWT本身就存在檢測是否竄改的簽署值以及搭配特定身分資訊，所以Resource Server可以只使用特定密鑰、製作簽署值的算法、請求端夾雜的token來驗證請求端是合法的：
	-  Resource Server - Authorization Server 之間具體的雙方特定密鑰：
		- Resource Server 和 Authorization Server 皆使用相同密鑰來驗證簽署值
		- Public-key algorithm 為基礎：Authorization Server使用私鑰發放token，Resource Server使用公鑰驗證
	- 


> ### Refresh Token机制如何提升安全？

> Refresh Token的其中一个目的是让用户在较长的时间保持登录状态，那么可否直接让Access Token具有更长的有效期，从而可以省去许多没用的步骤。答案是不安全，理由参考上面问题的答案。

> 举个例子，某个用户登录成功，获得了一个可以发帖的Access Token，这时管理员发现他发布垃圾内容吊销了发帖权限，而这个信息一般属于授权服务管理，也就是说他下次向授权服务请求Access Token将不会得到发帖权限。但是如果用户之前拿到的Access Token是长期有效的，那么这个用户就可以发帖很长时间。如果Access Token在短时间内失效，那么他必须重新去授权服务请求，这时授权服务将不会颁发具备发帖权限的Access Token。

> 第二个例子，如果Access Token具有较长的有效期，一旦被盗用，攻击者就可以拿Access Token使用很长时间。聪明的你可能会想到，攻击者可以同时盗取Refresh Token。

>[RFC6749](https://link.juejin.cn?target=http%3A%2F%2Fwww.rfcreader.com%2F%23rfc6749 "http://www.rfcreader.com/#rfc6749")第10节中有说明，授权服务**必须维护Refresh Token与客户端的绑定关系**，也就是说只有合法用户的客户端（可通过IP,UA等资料判断）来请求是可以通过的。退一步讲，如果攻击者模拟了客户端可以执行刷新请求，那么就要看谁先刷。由于授权服务**可以设置Refresh Token一次有效**，因此不管哪个先刷新，另一个人刷新就会报错。如果用户先刷新，攻击者以Access Token和Refresh Token的双重失效结束游戏。如果攻击者先刷新了，合法用户就会收到报错信息，授权服务会引导用户从上图的步骤(A)重新开始认证，从而把有效的Refresh Token拿回到合法用户这里。


## 複習



---
Status: #🌱 
Tags:
[[Authorization]]
Links:
[[refresh token 是種token來讓Client或Replying Party 在不需要額外使用者帳號進行credential驗證的情況下直接向Authorization Server索要新的Access Token或ID token]]
[[Symmetric-key algorithm 概念會是加密方和解密方都使用同一個鑰匙值進行加密或解密；Public-key cryptography 概念會是加密方和解密方兩方都拿獨立不同的鑰匙值來各別做加密或者解密]]
References:
[[@AccessTokenRefresh]]