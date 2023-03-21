## 描述


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
	- 使用者直接向客戶端提供特定系統的帳號和密碼
		- 主要目的為：將帳密作為使用者的授權許可之證明
	- 客戶端憑藉著帳密來向認證伺服器索要token
	- 認證伺服器確認無誤後，就會將token回傳給客戶端

### 步驟B所需要的參數
> B步骤中，客户端发出的HTTP请求，包含以下参数：

> -   grant_type：表示授权类型，此处的值固定为"password"，必选项。
> -   username：表示用户名，必选项。
> -   password：表示用户的密码，必选项。
> -   scope：表示权限范围，可选项。

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


## 複習


---
Status: #🌱 
Tags:
[[OAuth]]
Links:
[[OAuth 會是標準、協定，其內容為如何在不需要將 "擁有資源使用權限的使用者帳密" 給予 特定服務A的情況下，發放資源使用權限給特定服務A來代表使用者去做特定事情]]
References:
