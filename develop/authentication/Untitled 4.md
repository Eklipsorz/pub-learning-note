## 描述

> Token-based replay used to be the standard way to conduct conformance checking





> Traditionally authentication involves three parties User, Relying party Web Site, and Authentication server.  The Authentication server produces some sort of token/assertion for the consumption of the Relying Party (RP).  This assertion in OpenID 2.0 and SAML 2.0 contain a way to identify who (what RP) the token was created for.  The RP only accepts tokens addressed to it.  This prevents RP's and others from replaying tokens at different RP.

傳統上，認證(authentication)過程會涉及到三方，分別為User、Relying party Web Site、Authentication server。 Authentication server會產生一些token或者assertion來代表使用特定依賴方資源的使用權利。

RP 為replying party ，指的是client主機

assertion在OpenID 2.0 和  SAML 2.0中包含一個方法來識別這個assertion 或者token是為誰/哪個RP而建立的，而RP只接受針對自己的token，這防止

> In OAuth the token is intended for the consumption of the protected resource, and intentionally opaque to the client (RP).  The RP has no way to tell from the token if it was generated for it or another RP.


在OAuth 中，token是用於受保護資源的使用和故意對客戶端不透明任何資訊，而RP也沒辦法從token判別該token是為誰而建立的


> You could say the audience for the OAuth token is the protected resource and the audience for a authentication token is the RP.   They are not the same endpoint!

你可以說OAuth Token 的audience 是指受保護資源，而authentication token的audience會是指RP。兩者是不同端點。



> How is Connect Different from plain OAuth?

> We needed to add the appropriate security and semantics for authentication without compromising OAuth's functionality as a Authorization protocol.

我們需要在不影響OAuthㄐ

> One idea we explored was adding a audience claim to the protected resource(User Info Endpoint).
> This requires communicating the OAuth client_id from the authorization endpoint to the protected resource.  The biggest problem is that the RP is required to do a network operation in the background to get the user_id before logging the user in.

> Many RP including Facebook stated that the extra latency in the network round trip was unacceptable.

> Now you are thinking how can that be if that is way Facebook is doing?

> Well it turns out that they have some undocumented enhancements to get around the latency issue. They are using something they call signed-request.

> The idea is that they are encapsulating the OAuth code token inside a "signed" JSON object.

> The SDK they provide is looking for user_id in the signed request and using that to log the user in before doing any back channel OAuth requests. This provides an implicit audience restriction by the client verifying a symmetric client password used to generate a HMAC over the token.

> To be clear Facebook is NOT using the signed_request as the access_token they are extracting code from the signed_request and exchanging that for a access_token at the Token Endpoint.

> One thing OAuth 2.0 allows is defining new Response Types. Based on OAuth 2.0 Multiple Response Type Encoding Practices by Google and Facebook, we decided to use a separate id_token parameter in the response rather than overload the access_token. That allows the tokens to have separate audience restrictions and formats. Facebook is doing the same thing but are using signed_request rather than id_token as the response type. We both return the extra token fragment encoded win an additional parameter, in Facebooks case signed_request and in openID's id_token.


## 複習

---
Status: #🌱 
Tags:
[[Authentication]]
Links:
References: