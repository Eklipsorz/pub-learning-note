## 描述
[[@LiJieOAuthRuanYiFengDeWangLuoRiZhi]]



> ## 简化模式

> 简化模式（implicit grant type）不通过第三方应用程序的服务器，直接在浏览器中向认证服务器申请令牌，跳过了"授权码"这个步骤，因此得名。所有步骤在浏览器中完成，令牌对访问者是可见的，且客户端不需要认证。


![](https://www.ruanyifeng.com/blogimg/asset/2014/bg2014051205.png)

> 它的步骤如下：

> （A）客户端将用户导向认证服务器。
> 
> （B）用户决定是否给于客户端授权。
> 
> （C）假设用户给予授权，认证服务器将用户导向客户端指定的"重定向URI"，并在URI的Hash部分包含了访问令牌。
> 
> （D）浏览器向资源服务器发出请求，其中不包括上一步收到的Hash值。
> 
> （E）资源服务器返回一个网页，其中包含的代码可以获取Hash值中的令牌。
> 
> （F）浏览器执行上一步获得的脚本，提取出令牌。
> 
> （G）浏览器将令牌发给客户端。


简化模式（implicit grant type）不通过第三方应用程序的服务器，直接在浏览器中向认证服务器申请令牌，跳过了"授权码"这个步骤，因此得名。所有步骤在浏览器中完成，令牌对访问者是可见的，且客户端不需要认证。

重點：
- implicit grant type 在OAuth 上是以與Authorization code grant type版本來說相對簡化的模式，該模式，主要不通過第三方應用程式/Client來進行授權碼，並直接在瀏覽器上向認證服務器上申請token。
- token 索要過程是對訪問者是可見的，客戶端不需要從中參與認證
- 主要流程為：
	- A. 使用者訪問客戶端，客戶端將使用者導向認證伺服器來進行身份認證、授權詢問
	- B. 使用者通過身份認證並確定授權
	- C. 假設使用者允許授權並發送至認證伺服器，認證伺服器就將使用者導向客戶端是先指定的重導向URI，並在URI添加Fragment (裡面夾雜Hash格式構成的access token)
		- User Agent 會將Fragment 部分儲存在本身的儲存系統，並不會因重導向URI而發送向對應端點該部分內容。
		- 重導向URI通常會是指Client 或者 Resource Server
	- D.  使用者透過瀏覽器向指定的重導向URI發送請求，但不包含先前的Fragment
	- E.  對應URI/Client/Resource Server 會回傳一份夾雜Script的網頁至User Agent
	- F.  執行上一步獲得的Script，來從C步驟獲得的Fragment解開Token以及其相關資訊
	- G. 將上一步解開的結果物-Token 發給Client端
- 細節：
	- implicit grant type 這模式還分出兩個版本：
		- 第一個版本就是目前這個
		- 第二個版本為
		[[develop/authentication/OAuth/Untitled 1]]


### 步驟A所需要的參數

> A步骤中，客户端发出的HTTP请求，包含以下参数：

> -   response_type：表示授权类型，此处的值固定为"token"，必选项。
> -   client_id：表示客户端的ID，必选项。
> -   redirect_uri：表示重定向的URI，可选项。
> -   scope：表示权限范围，可选项。
> -   state：表示客户端的当前状态，可以指定任意值，认证服务器会原封不动地返回这个值。

> 下面是一个例子。
```http
GET /authorize?response_type=token&client_id=s6BhdRkqt3&state=xyz
    &redirect_uri=https%3A%2F%2Fclient%2Eexample%2Ecom%2Fcb HTTP/1.1
Host: server.example.com
```

重點：
- 步驟A：使用者訪問客戶端，客戶端將使用者導向認證伺服器來進行身份認證、授權詢問
- 請求形式為：URI(含URI參數)、封包
- 主要參數：
	- response_type： 表示授權類型為何，若是implicit grant type，就為token
	- client_id：表示客戶端應用程式在認證伺服器上所註冊的client_id
	- redirect_uri：定義哪邊提供Script或者哪邊接收token
	- scope：定義申請的權限範疇
- 細節：
	- response_type、client_id 是必填的
	- redirect_uri 可在認證伺服器上事先定義好
	- scope 可於認證伺服器上事先定義好 或者 在認證伺服器對使用者進行授權詢問而得到

### 步驟C所需要的參數

> C步骤中，认证服务器回应客户端的URI，包含以下参数：

> -   access_token：表示访问令牌，必选项。
> -   token_type：表示令牌类型，该值大小写不敏感，必选项。
> -   expires_in：表示过期时间，单位为秒。如果省略该参数，必须其他方式设置过期时间。
> -   scope：表示权限范围，如果与客户端申请的范围一致，此项可省略。
> -   state：如果客户端的请求中包含这个参数，认证服务器的回应也必须一模一样包含这个参数。

> 下面是一个例子。

```http
HTTP/1.1 302 Found
Location: http://example.com/cb#access_token=2YotnFZFEjr1zCsicMWpAA &state=xyz&token_type=example&expires_in=3600
```

> 在上面的例子中，认证服务器用HTTP头信息的Location栏，指定浏览器重定向的网址。注意，在这个网址的Hash部分包含了令牌。

重點：
- 步驟C：假設使用者允許授權並發送至認證伺服器，認證伺服器就將使用者導向客戶端是先指定的重導向URI，並在URI添加Fragment (裡面夾雜Hash格式構成的access token)
- 請求形式為：URI(含)

## 複習
#🧠 Question :: ->->-> ``

---
Status: #🌱 
Tags:
[[OAuth]]
Links:
[[OAuth 會是標準、協定，其內容為如何在不需要將 "擁有資源使用權限的使用者帳密" 給予 特定服務A的情況下，發放資源使用權限給特定服務A來代表使用者去做特定事情]]
[[OAuth 中 的 Authentication Code Grant Type 是以authorization code和申請其code來分別作為認證授權伺服器能夠認可使用者授權的的結果物和流程]]
References:
[[@LiJieOAuthRuanYiFengDeWangLuoRiZhi]]