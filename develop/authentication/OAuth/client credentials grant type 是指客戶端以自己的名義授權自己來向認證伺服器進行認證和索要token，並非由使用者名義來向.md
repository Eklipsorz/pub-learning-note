## 描述

[[@ClientCredentialsOAuth]]
> The Client Credentials grant type is used by clients to obtain an access token outside of the context of a user.


[[@LiJieOAuthRuanYiFengDeWangLuoRiZhi]]

> 客户端模式（Client Credentials Grant）指客户端以自己的名义，而不是以用户的名义，向"服务提供商"进行认证。严格地说，客户端模式并不属于OAuth框架所要解决的问题。在这种模式中，用户直接向客户端注册，客户端以自己的名义要求"服务提供商"提供服务，其实不存在授权问题。


![客户端模式](https://www.ruanyifeng.com/blogimg/asset/2014/bg2014051207.png)


> 它的步骤如下：
> （A）客户端向认证服务器进行身份认证，并要求一个访问令牌。
> 
> （B）认证服务器确认无误后，向客户端提供访问令牌。

重點：
- client credentials grant type 是指客戶端以自己的名義授權自己來向認證伺服器進行認證和索要token，並非由使用者名義來向。
- 主要流程為：
	- 客戶端憑藉自己平台的身份資訊作為 **自己平台** 授權 **自己** 並以此向認證伺服器索要token
	- 認證伺服器確認身份資訊無誤之後，就會回傳token至客戶端
- 細節：
	- 該種類並不屬於OAuth 所處理的面向，由於本身不存在使用者授權流程，只是單純是客戶端憑藉自己平台的身份資訊作為 **自己平台** 授權 **自己** 


### 步驟A所需要的參數

> A步骤中，客户端发出的HTTP请求，包含以下参数：

> -   grant_type：表示授权类型，此处的值固定为"client_credentials"，必选项。
> -   scope：表示权限范围，可选项。

```http

     POST /token HTTP/1.1
     Host: server.example.com
     Authorization: Basic czZCaGRSa3F0MzpnWDFmQmF0M2JW
     Content-Type: application/x-www-form-urlencoded

     grant_type=client_credentials
```
> 认证服务器必须以某种方式，验证客户端身份。

[[@ClientCredentialsOAuth]]
> #### Client Authentication (required)

> The client needs to authenticate themselves for this request. Typically the service will allow either additional request parameters `client_id` and `client_secret`, or accept the client ID and secret in the HTTP Basic auth header.

重點：
- 步驟A：客戶端憑藉自己平台的身份資訊作為 **自己平台** 授權 **自己** 並以此向認證伺服器索要token
- 請求形式為：封包
- 主要參數為：
	- grant_type：授權種類，在這裡會是client_credentials
	- scope：表示申請權限
	- client_id：客戶端在認證伺服器上所註冊的client_id，通常會放在封包的header 或者 body
	- client_secret：客戶端在認證伺服器上註冊的client_id所擁有的secret，通常會放在封包的header 或者 body
- 細節：
	- 認證伺服器要做client_id和client_secret的身份驗證，就會存放在封包內的client_id和client_secret來驗證

### 步驟B所需要的參數

> B步骤中，认证服务器向客户端发送访问令牌，下面是一个例子。

```http

     HTTP/1.1 200 OK
     Content-Type: application/json;charset=UTF-8
     Cache-Control: no-store
     Pragma: no-cache

     {
       "access_token":"2YotnFZFEjr1zCsicMWpAA",
       "token_type":"example",
       "expires_in":3600,
       "example_parameter":"example_value"
     }
```

重點：
- 認證伺服器確認身份資訊無誤之後，就會回傳token至客戶端
- 回應形式為：封包
- 主要回應內容：
	- access_token：代表特定身份權限的token
	- token_type：token的種類
	- expires_in：token的有限時間

## 複習

#🧠 client credential grant type 在OAuth 下會是什麼？ ->->-> `client credentials grant type 是指客戶端以自己的名義授權自己來向認證伺服器進行認證和索要token，並非由使用者名義來向`
<!--SR:!2023-06-08,49,250-->

#🧠 client credential grant type 在OAuth 下，client會以誰授權誰的結果來索要token？ ->->-> `client本身 授權 自己 的結果來索要token`
<!--SR:!2023-05-08,30,248-->

#🧠 client credential grant type 在OAuth 下的流程會是什麼？ ->->-> `	- 客戶端憑藉自己平台的身份資訊作為 **自己平台** 授權 **自己** 並以此向認證伺服器索要token - 認證伺服器確認身份資訊無誤之後，就會回傳token至客戶端`
<!--SR:!2023-05-14,35,248-->

#🧠 client credential grant type 在OAuth 下的流程會是什麼？畫圖表示 ->->-> ![客户端模式](https://www.ruanyifeng.com/blogimg/asset/2014/bg2014051207.png)
<!--SR:!2023-05-25,41,248-->

#🧠 client credential grant type 在OAuth 下嚴格來說，會是使用者授權嗎？為什麼 ->->-> `不屬於，只是單純是客戶端憑藉自己平台的身份資訊作為 **自己平台** 授權 **自己** `
<!--SR:!2023-05-28,43,248-->

#🧠 client credential grant type 在OAuth下："客戶端憑藉自己平台的身份資訊作為 **自己平台** 授權 **自己** 並以此向認證伺服器索要token"，其請求會是什麼形式 ->->-> `封包`
<!--SR:!2023-05-26,41,230-->

#🧠 client credential grant type 在OAuth下："客戶端憑藉自己平台的身份資訊作為 **自己平台** 授權 **自己** 並以此向認證伺服器索要token"，其請求會是什麼參數和資料？ ->->-> `	- grant_type：授權種類，在這裡會是client_credentials - scope：表示申請權限 - client_id：客戶端在認證伺服器上所註冊的client_id，通常會放在封包的header 或者 body - client_secret：客戶端在認證伺服器上註冊的client_id所擁有的secret，通常會放在封包的header 或者 body`
<!--SR:!2023-05-10,32,250-->


#🧠 client credential grant type 在OAuth下："客戶端憑藉自己平台的身份資訊作為 **自己平台** 授權 **自己** 並以此向認證伺服器索要token"，其請求的grant_type會是什麼？ ->->-> `	- grant_type：授權種類，在這裡會是client_credentials`
<!--SR:!2023-05-10,33,250-->

#🧠 client credential grant type 在OAuth下："客戶端憑藉自己平台的身份資訊作為 **自己平台** 授權 **自己** 並以此向認證伺服器索要token"，其中發送的請求會在哪裡存放著身份資訊來做驗證 ->->-> `封包的header或者body部分`
<!--SR:!2023-06-16,41,208-->


#🧠 client credential grant type 在OAuth下："認證伺服器確認身份資訊無誤之後，就會回傳token至客戶端"，其回應封包所要回傳的內容形式為何 ->->-> `封包`
<!--SR:!2023-05-10,27,228-->


#🧠 client credential grant type 在OAuth下："認證伺服器確認身份資訊無誤之後，就會回傳token至客戶端"，其回應封包所要回傳的內容為何 ->->-> `- access_token：代表特定身份權限的token - token_type：token的種類 - expires_in：token的有限時間`
<!--SR:!2023-07-07,60,228-->

#🧠  client credential grant type 在OAuth下，通常會是以什麼http動詞來讓客戶端索求token？請舉例->->-> `POST /token`
<!--SR:!2023-05-09,32,250-->




---
Status: #🌱 
Tags:
[[OAuth]]
Links:
References:
[[@ClientCredentialsOAuth]]
[[@LiJieOAuthRuanYiFengDeWangLuoRiZhi]]