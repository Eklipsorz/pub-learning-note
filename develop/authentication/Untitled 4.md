## 描述




> Traditionally authentication involves three parties User, Relying party Web Site, and Authentication server.  The Authentication server produces some sort of token/assertion for the consumption of the Relying Party (RP).  This assertion in OpenID 2.0 and SAML 2.0 contain a way to identify who (what RP) the token was created for.  The RP only accepts tokens addressed to it.  This prevents RP's and others from replaying tokens at different RP.

傳統上，認證(authentication)過程會涉及到三方，分別為User、Relying party Web Site、Authentication server。 Authentication server會產生一些token或者assertion來代表使用特定依賴方資源的使用權利。

RP 為replying party ，指的是client主機

assertion在OpenID 2.0 和  SAML 2.0中包含一個方法來識別這個assertion 或者token是為誰而建立的，而RP只接受針對自己的token，這防止

> In OAuth the token is intended for the consumption of the protected resource, and intentionally opaque to the client (RP).  The RP has no way to tell from the token if it was generated for it or another RP.


在OAuth 中，token是用於受保護資源的使用和故意對客戶端不透明任何資訊，而RP也沒辦法說

> You could say the audience for the OAuth token is the protected resource and the audience for a authentication token is the RP.   They are not the same endpoint!



## 複習

---
Status: #🌱 
Tags:
[[Authentication]]
Links:
References: