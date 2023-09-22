## 描述

[[@LiJieOAuthRuanYiFengDeWangLuoRiZhi]]
> 密码模式（Resource Owner Password Credentials Grant）中，用户向客户端提供自己的用户名和密码。客户端使用这些信息，向"服务商提供商"索要授权。

> 在这种模式中，用户必须把自己的密码给客户端，但是客户端不得储存密码。这通常用在用户对客户端高度信任的情况下，比如客户端是操作系统的一部分，或者由一个著名公司出品。而认证服务器只有在其他授权模式无法执行的情况下，才能考虑使用这种模式。

![密码模式](https://www.ruanyifeng.com/blogimg/asset/2014/bg2014051206.png)

> 它的步骤如下：
> 
> （A）用户向客户端提供用户名和密码。
> 
> （B）客户端将用户名和密码发给认证服务器，向后者请求令牌。
> 
> （C）认证服务器确认无误后，向客户端提供访问令牌。

重點：
- Resource Owner Password Credentials Grant 會是由使用者以特定系統的帳密來當作授權許來給客戶端索要特定系統下之授權伺服器的token
- 適用場景：
	- 由於是使用者提供高度敏感的帳密，所以客戶端必須是值得信任，比如客戶端為作業系統的一部分或者由一個著名公司出品的客戶端
	- 其他授權模式無法實現才會選擇本方案
- 主要流程為
	- A. 使用者直接向客戶端提供特定系統的帳號和密碼
		- 主要目的為：將帳密作為使用者的授權許可之證明
	- B. 客戶端憑藉著使用者的帳密來向認證伺服器索要token
	- C. 認證伺服器確認無誤使用者的帳密後，就會將token回傳給客戶端
- 細節：
	- 通常來說，必須規定在過程中客戶端不得儲存使用者任何帳密

### 步驟B所需要的參數
> B步骤中，客户端发出的HTTP请求，包含以下参数：

> -   grant_type：表示授权类型，此处的值固定为"password"，必选项。
> -   username：表示用户名，必选项。
> -   password：表示用户的密码，必选项。
> -   scope：表示权限范围，可选项。

```http
POST /token HTTP/1.1

Host: server.example.com
Authorization: Basic czZCaGRSa3F0MzpnWDFmQmF0M2JW
Content-Type: application/x-www-form-urlencoded 

grant_type=password&username=johndoe&password=A3ddj3w
```

重點：
- 步驟B：客戶端憑藉著使用者的帳密來向認證伺服器索要token
- 請求方式：封包
- 主要參數：
	- grant_type：授權種類，在這裡會是填寫password
	- username：表示特定系統下的帳號
	- password：表示特定系統下的帳號所擁有的密碼
	- scope：表示索要的token要什麼樣的scope

### 步驟C所需要的參數
> C步骤中，认证服务器向客户端发送访问令牌，下面是一个例子。

```http 
HTTP/1.1 200 OK
Content-Type: application/json;charset=UTF-8
Cache-Control: no-store
Pragma: no-cache

{
	"access_token":"2YotnFZFEjr1zCsicMWpAA",
    "token_type":"example",
    "expires_in":3600,
    "refresh_token":"tGzv3JOkF0XG5Qx2TlKWIA",
	"example_parameter":"example_value"
}
```

重點：
- 步驟C：認證伺服器確認無誤使用者的帳密後，就會將token回傳給客戶端
- 請求方式：URI(含URI參數)、封包
- 主要回應內容：
	- token_type：token 種類
	- access_token：代表特定身份下所擁有的權限結果物 access token 
	- refresh_token：用以申請新的access token和refresh token的token
	- expires_in：access token的有效時間

## 複習

#🧠 Resource Owner Password Credentials Grant 在 OAuth 下會是什麼？->->-> `Resource Owner Password Credentials Grant 會是由使用者以特定系統的帳密來當作授權許來給客戶端索要特定系統下之授權伺服器的token`
<!--SR:!2023-11-02,46,247-->


#🧠 Resource Owner Password Credentials Grant 在 OAuth 下會是以什麼形式來當作使用者同意授權的資料？ ->->-> `使用者的帳密`
<!--SR:!2024-03-12,218,250-->

#🧠 Resource Owner Password Credentials Grant 在OAuth 下的適用場景為何？ ->->-> `	- 由於是使用者提供高度敏感的帳密，所以客戶端必須是值得信任，比如客戶端為作業系統的一部分或者由一個著名公司出品的客戶端 - 其他授權模式無法實現才會選擇本方案`
<!--SR:!2024-04-02,229,250-->

#🧠 Resource Owner Password Credentials Grant 在 OAuth 下 所擁有的流程為何？->->-> `A. 使用者直接向客戶端提供特定系統的帳號和密碼、 B. 客戶端憑藉著使用者的帳密來向認證伺服器索要token、C. 認證伺服器確認無誤使用者的帳密後，就會將token回傳給客戶端`
<!--SR:!2023-10-14,22,210-->

#🧠 Resource Owner Password Credentials Grant 在 OAuth 下 所擁有的流程為何？畫圖來說明 ->->-> ![密码模式](https://www.ruanyifeng.com/blogimg/asset/2014/bg2014051206.png)
<!--SR:!2024-04-11,236,250-->

#🧠 在Resource Owner Password Credentials Grant 在 OAuth 下 所擁有的流程中，其中`A. 使用者直接向客戶端提供特定系統的帳號和密碼` 的帳號和密碼是做什麼目的？ ->->-> `主要目的為：將帳密作為使用者的授權許可之證明`
<!--SR:!2024-02-15,193,250-->

#🧠 在Resource Owner Password Credentials Grant 在 OAuth 下："客戶端憑藉著使用者的帳密來向認證伺服器索要token"，客戶端發送的請求會是什麼形式？->->-> `封包`
<!--SR:!2024-06-03,265,249-->

#🧠 在Resource Owner Password Credentials Grant 在 OAuth 下："客戶端憑藉著使用者的帳密來向認證伺服器索要token"，客戶端向認證伺服器索求token的http動詞會是什麼？ ->->-> `通常會是POST`
<!--SR:!2024-03-27,225,249-->


#🧠 在Resource Owner Password Credentials Grant 在 OAuth 下："客戶端憑藉著使用者的帳密來向認證伺服器索要token"，客戶端的請求封包之主要內容為何->->-> `- grant_type：授權種類，在這裡會是填寫password - username：表示特定系統下的帳號 - password：表示特定系統下的帳號所擁有的密碼 - scope：表示索要的token要什麼樣的scope`
<!--SR:!2024-04-14,239,250-->

#🧠 在Resource Owner Password Credentials Grant 在 OAuth 下："認證伺服器確認無誤使用者的帳密後，就會將token回傳給客戶端"，其中的回應會是什麼形式 ->->-> `封包`
<!--SR:!2024-02-14,191,249-->



#🧠 在Resource Owner Password Credentials Grant 在 OAuth 下："認證伺服器確認無誤使用者的帳密後，就會將token回傳給客戶端"，其中的回應內容會是什麼 ->->-> `- token_type：token 種類 - access_token：代表特定身份下所擁有的權限結果物 access token  - refresh_token：用以申請新的access token和refresh token的token - expires_in：access token的有效時間`
<!--SR:!2023-10-28,72,210-->



#🧠 在Resource Owner Password Credentials Grant 在 OAuth 下，客戶端對於使用者提供的帳密會如何處理？(儲存) ->->-> `1. 會拿來索要token  並且通常來說，必須規定在過程中客戶端不得儲存使用者任何帳密`
<!--SR:!2024-03-11,218,249-->

#🧠 在Resource Owner Password Credentials Grant 在 OAuth 下，客戶端對於使用者提供的帳密會如何處理？->->-> `1. 會拿來索要token  並且通常來說，必須規定在過程中客戶端不得儲存使用者任何帳密`
<!--SR:!2024-04-10,235,249-->

#🧠 在Resource Owner Password Credentials Grant 在 OAuth 下，客戶端對於使用者提供的帳密會儲存起來嗎？ 為什麼？->->-> `並不會儲存，確保帳密安全`
<!--SR:!2024-03-31,227,249-->



---
Status: #🌱 
Tags:
[[OAuth]]
Links:
[[OAuth 會是標準、協定，其內容為如何在不需要將 "擁有資源使用權限的使用者帳密" 給予 特定服務A的情況下，發放資源使用權限給特定服務A來代表使用者去做特定事情]]
References:
[[@LiJieOAuthRuanYiFengDeWangLuoRiZhi]]