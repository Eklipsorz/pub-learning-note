## 描述

[[@LiJieOAuthRuanYiFengDeWangLuoRiZhi]]

> 如果用户访问的时候，客户端的"访问令牌"已经过期，则需要使用"更新令牌"申请一个新的访问令牌。

> 客户端发出更新令牌的HTTP请求，包含以下参数：

> -   grant_type：表示使用的授权模式，此处的值固定为"refresh_token"，必选项。
> -   refresh_token：表示早前收到的更新令牌，必选项。
> -   scope：表示申请的授权范围，不可以超出上一次申请的范围，如果省略该参数，则表示与上一次一致。

> 下面是一个例子。

```http
POST /token HTTP/1.1

Host: server.example.com
Authorization: Basic czZCaGRSa3F0MzpnWDFmQmF0M2JW
Content-Type: application/x-www-form-urlencoded

grant_type=refresh_token&refresh_token=tGzv3JOkF0XG5Qx2TlKWIA
```


重點：
- 若客戶端所擁有的token已經過期或者失效的話，可透過refresh token來申請新的token
-  使用refresh token來申請token請求的封裝形式：封包
- 主要流程為：
	- 客戶端憑藉refresh token直接向認證伺服器來索要token
	- 認證伺服器驗證refresh token無誤後，就產生新的token和refresh token至客戶端
	- 客戶端利用新的token重新對resource server發送索要資源的請求

### 參數：客戶端憑藉refresh token直接向認證伺服器來索要token

重點：
- 主要參數為：
	- grant_type： 表示授權種類為何，若用refresh token來申請就填寫為refresh_token
	- refresh_token：用來申請新的token的token
	- scope：申請新token的權限，通常來說不可超出上次申請的權限範疇


## 複習

#🧠 token based authentication/OAuth：若客戶端所擁有的token已經過期或者失效的話，客戶端可以做些什麼來獲取token ->->-> `1. 利用refresh token來申請新的token 2. 重新獲得授權同意並拿同意來索求token`
<!--SR:!2023-09-20,24,190-->

#🧠 token based authentication/OAuth：使用refresh token來申請token請求的封裝形式為何？->->-> `封包`
<!--SR:!2023-09-15,19,210-->

#🧠 token based authentication/OAuth：使用refresh token來申請token請求之主要流程為何？ ->->-> `	- 客戶端憑藉refresh token直接向認證伺服器來索要token - 認證伺服器驗證refresh token無誤後，就產生新的token和refresh token至客戶端 - 客戶端利用新的token重新對resource server發送索要資源的請求`
<!--SR:!2024-03-25,211,250-->

#🧠 使用refresh token來申請token請求之主要流程："客戶端憑藉refresh token直接向認證伺服器來索要token"，這步驟所需要的請求封包會需要什麼參數？ ->->-> `	- grant_type： 表示授權種類為何，若用refresh token來申請就填寫為refresh_token- refresh_token：用來申請新的token的token - scope：申請新token的權限，通常來說不可超出上次申請的權限範疇`
<!--SR:!2023-09-29,33,190-->

#🧠 使用refresh token來申請token請求之主要流程："客戶端憑藉refresh token直接向認證伺服器來索要token"，通常會用什麼http動詞來索要？->->-> `POST`
<!--SR:!2023-09-02,99,250-->

#🧠 使用refresh token來申請token請求之主要流程："客戶端憑藉refresh token直接向認證伺服器來索要token"，通常會用什麼http動詞以及端點會是什麼？請舉例來說？->->-> `POST /token`
<!--SR:!2023-10-15,47,230-->





---
Status: #🌱 
Tags:
[[Authentication]] - [[Authorization]]
Links:
[[refresh token 是種token來讓Client或Replying Party 在不需要額外使用者帳號進行credential驗證的情況下直接向Authorization Server索要新的Access Token或ID token]]
References:
[[@LiJieOAuthRuanYiFengDeWangLuoRiZhi]]