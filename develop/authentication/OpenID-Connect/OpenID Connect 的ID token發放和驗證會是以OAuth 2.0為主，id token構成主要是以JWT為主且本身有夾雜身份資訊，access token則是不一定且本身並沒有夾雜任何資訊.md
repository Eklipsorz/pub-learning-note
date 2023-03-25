

## 描述




### id token 的發放和驗證流程


由於id token 是基於OpenID Connenct 協議，該協議會是以OAuth 2.0的token發放和驗證流程為主，只是token會是以夾雜特定身份資訊的token。

[[implicit grant type 在OAuth 上是以與Authorization code grant type版本來說相對簡化的模式，該模式主要不通過第三方應用程式或Client來進行授權碼，並直接在瀏覽器上向認證服務器上申請token]]
[[OAuth 中 的 Authentication Code Grant Type 是以authorization code和申請其code來分別作為認證授權伺服器能夠認可使用者授權的的結果物和流程]]
[[Resource Owner Password Credentials Grant 會是由使用者以特定系統的帳密來當作授權許來給客戶端索要特定系統下之授權伺服器的token]]
[[client credentials grant type 是指客戶端以自己的名義授權自己來向認證伺服器進行認證和索要token，並非由使用者名義來向]]

### id token vs. access token


[[@TokenTypesAuthentication]]
> ID tokens are JSON Web Tokens (JWTs) that conform to the OpenID Connect (OIDC) specification. They are composed of a set of key-value pairs called claims.

> Unlike access tokens, which are opaque objects that cannot be inspected by the application, ID tokens are meant to be inspected and used by the application. Information from the token, such as Who signed the token or the identity for whom the ID token was issued, is available for use by the application.

重點：
- id token 本身是self-containned 的JWT而構成；access token 本身不一定會是self-containned的JWT而構成
- id token 由於是JWT，所以本身會夾雜內容；access token由於不一定會是JWT，所以本身不一定夾雜額外內容
- id token 本身夾雜的內容會特定身份有關；access token本身夾雜的內容則是無或者就是誰授權予誰的資訊
## 複習
#🧠 id token 的發放和驗證流程為何？ ->->-> `會是以OAuth 2.0中的authorization code grant type、implicit grant type、resource owner password credentials grant type、client credentials grant type為主`
<!--SR:!2023-03-25,3,250-->

#🧠 id token 的發放和驗證流程為OAuth 2.0中的authorization code grant type、implicit grant type、resource owner password credentials grant type、client credentials grant type為主，為何以他們為主？->->-> `由於id token本身是由OpenId Connect標準提出，該標準又是以OAuth為基礎`
<!--SR:!2023-03-25,3,250-->

#🧠  OpenID Connect下的 id token 和 OAuth 2.0下的access_token 之間有何種差異? 有三者->->-> `- id token 本身是self-containned 的JWT而構成；access token 本身不一定會是self-containned的JWT而構成  - id token 由於是JWT，所以本身會夾雜內容；access token由於不一定會是JWT，所以本身不一定夾雜額外內容 - id token 本身夾雜的內容會特定身份有關；access token本身夾雜的內容則是無或者就是誰授權予誰的資訊`
<!--SR:!2023-03-26,3,250-->

#🧠  OpenID Connect下的 id token 和 OAuth 2.0下的access_token 之間有何種構成差異->->-> `- id token 本身是self-containned 的JWT而構成；access token 本身不一定會是self-containned的JWT而構成`
<!--SR:!2023-03-25,3,250-->

#🧠  OpenID Connect下的 id token 和 OAuth 2.0下的access_token 之間有何種夾雜的內容差異->->-> ` id token 由於是JWT，所以本身會夾雜內容；access token由於不一定會是JWT，所以本身不一定夾雜額外內容`
<!--SR:!2023-04-04,10,250-->


#🧠 OpenID Connect下的 id token 和 OAuth 2.0下的access_token 這兩種token本身會夾雜什麼內容？->->-> `id token 本身夾雜的內容會特定身份有關；access token本身夾雜的內容則是無或者就是誰授權予誰的資訊`
<!--SR:!2023-03-25,3,250-->




---
Status: #🌱 
Tags:
[[OpenID-Connect]]
Links:
[[id token 本身是用來證明特定使用者是受過認證的資訊，使用者或者Relying Party 向OpenID Provider提供特定身份的證明資訊，接著由OpenID Provider對其進行驗證，若驗證成功就會發放對應token]]
[[OpenID 是一個開放式協定和標準，定義特定應用服務A如何與分散式身份認證系統進行認證；OpenID Connect主要以OAuth 2.0協定作為基礎來做驗證和權限分發，權限分發會是以token為表示來分發]]
[[implicit grant type 在OAuth 上是以與Authorization code grant type版本來說相對簡化的模式，該模式主要不通過第三方應用程式或Client來進行授權碼，並直接在瀏覽器上向認證服務器上申請token]]
[[OAuth 中 的 Authentication Code Grant Type 是以authorization code和申請其code來分別作為認證授權伺服器能夠認可使用者授權的的結果物和流程]]
[[Resource Owner Password Credentials Grant 會是由使用者以特定系統的帳密來當作授權許來給客戶端索要特定系統下之授權伺服器的token]]
[[client credentials grant type 是指客戶端以自己的名義授權自己來向認證伺服器進行認證和索要token，並非由使用者名義來向]]
References:
[[@TokenTypesAuthentication]]