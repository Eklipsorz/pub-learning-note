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
- implicit grant type 在OAuth 上是以與Authorization code grant type版本來說相對簡化的模式，該模式主要不通過第三方應用程式/Client來進行授權碼，並直接在瀏覽器上向認證服務器上申請token。
- token 索要過程是對訪問者是可見的，客戶端不需要從中參與認證
- 主要流程為：
	- A. 使用者訪問客戶端，客戶端將使用者導向認證伺服器來進行身份認證、授權詢問
	- B. 使用者通過身份認證並確定授權
	- C. 假設使用者允許授權並發送至認證伺服器，認證伺服器就將使用者導向客戶端是先指定的重導向URI，並在URI添加Fragment (裡面夾雜Hash格式構成的access token)
		- User Agent 會將Fragment 部分儲存在本身的儲存系統，並不會因重導向URI而發送向對應端點該部分內容，等到之後獲取提取用的Script，接著提取並轉交給Client
		- 重導向URI通常會是指Client 或者 Resource Server
	- D.  使用者透過瀏覽器向指定的重導向URI發送請求，但不包含先前的Fragment
	- E.  對應URI/Client/Resource Server 會回傳一份夾雜Script的網頁至User Agent
	- F.  執行上一步獲得的Script，來從C步驟獲得的Fragment解開Token以及其相關資訊
	- G. 將上一步解開的結果物-Token 發給Client端
- 細節：
	- implicit grant type 這模式還分出兩個版本：
		- 第一個版本：redirect_uri 是用來提供獲取Token的script
		- 第二個版本為： redirect_uri 是用來接收token的地點
		[[implicit grant type的 第二個版本為，主要利用 redirect_uri 來將token傳遞至client]]


![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1679229338/blog/OAuth/OAuth-implicit-version1_a4o6wt.png)


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
- 請求形式為：URI(含URI參數)、封包
- 主要參數為：
	- access_token：表示token
	- token_type：表示token種類
	- expires_in：表示過期時間
	- scope：表示token所擁有的使用權限
```
HTTP/1.1 302 Found
Location: http://example.com/cb#access_token=2YotnFZFEjr1zCsicMWpAA &state=xyz&token_type=example&expires_in=3600
```

## 複習
#🧠 implicit grant type 在OAuth 上會是指什麼？ ->->-> `implicit grant type 在OAuth 上是以與Authorization code grant type版本來說相對簡化的模式，該模式主要不通過第三方應用程式/Client來進行授權碼，並直接在瀏覽器上向認證服務器上申請token。`
<!--SR:!2024-02-21,199,250-->

#🧠  implicit grant type 在OAuth 中為何被稱之為implicit ？ ->->-> `implicit grant type 在OAuth 上是以與Authorization code grant type版本來說相對簡化的模式`
<!--SR:!2024-04-05,234,250-->

#🧠 implicit grant type 在OAuth 上的流程為何？以redirect_uri 是用來提供獲取Token的script作為主要解說版本 ->->-> `	- A. 使用者訪問客戶端，客戶端將使用者導向認證伺服器來進行身份認證、授權詢問 - B. 使用者通過身份認證並確定授權 - C. 假設使用者允許授權並發送至認證伺服器，認證伺服器就將使用者導向客戶端是先指定的重導向URI，並在URI添加Fragment (裡面夾雜Hash格式構成的access token) 	- D.  使用者透過瀏覽器向指定的重導向URI發送請求，但不包含先前的Fragment - E.  對應URI/Client/Resource Server 會回傳一份夾雜Script的網頁至User Agent - F.  執行上一步獲得的Script，來從C步驟獲得的Fragment解開Token以及其相關資訊 - G. 將上一步解開的結果物-Token 發給Client端`
<!--SR:!2023-09-08,33,230-->

#🧠 implicit grant type 在OAuth 上的流程為何？以redirect_uri 是用來提供獲取Token的script作為主要解說版本，在這裡請畫圖來表示 ->->-> ![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1679229338/blog/OAuth/OAuth-implicit-version1_a4o6wt.png)
<!--SR:!2023-09-16,13,190-->

#🧠   implicit grant type 在OAuth 流程中的 "假設使用者允許授權並發送至認證伺服器，認證伺服器就將使用者導向客戶端是先指定的重導向URI，並在URI添加Fragment (裡面夾雜Hash格式構成的access token)"，其中的Fragment 會如何被處理？？ ->->-> `User Agent 會將Fragment 部分儲存在本身的儲存系統，並不會因重導向URI而發送向對應端點該部分內容，等到之後獲取提取用的Script，接著提取並轉交給Client`
<!--SR:!2023-10-22,117,230-->

#🧠  以redirect_uri 是用來提供獲取Token的script作為主要解說版本：implicit grant type 在OAuth 流程中的 "假設使用者允許授權並發送至認證伺服器，認證伺服器就將使用者導向客戶端是先指定的重導向URI，並在URI添加Fragment (裡面夾雜Hash格式構成的access token)"，其中的重導向URI會是做什麼以及指向哪裡？？？ ->->-> `在這裡會是指定哪個端點會提供提取工具的script，至於指向哪，重導向URI通常會是指Client 或者 Resource Server`
<!--SR:!2023-11-26,111,230-->

#🧠  以redirect_uri 是用來提供獲取Token的script作為主要解說版本：implicit grant type 在OAuth 流程中的 "假設使用者允許授權並發送至認證伺服器，認證伺服器就將使用者導向客戶端是先指定的重導向URI"，在這個階段會回傳token，請問它會如何回傳 ->->-> `以URI Fragment形式來回傳token`
<!--SR:!2024-04-04,233,250-->

#🧠 以redirect_uri 是用來提供獲取Token的script作為主要解說版本：implicit grant type 在OAuth 流程中的 "假設使用者允許授權並發送至認證伺服器，認證伺服器就將使用者導向客戶端是先指定的重導向URI"，在這個階段會回傳token，請問它會如何回傳，請舉一個URI作為例子 ->->-> `http://example.com/cb#access_token=2YotnFZFEjr1zCsicMWpAA &state=xyz&token_type=example&expires_in=3600`
<!--SR:!2024-03-24,214,250-->

#🧠 implicit grant type 在OAuth 中存在兩個主要版本，主要會是什麼？ ->->-> `- 第一個版本：redirect_uri 是用來提供獲取Token的script - 第二個版本為： redirect_uri 是用來接收token的地點`
<!--SR:!2024-03-19,213,250-->

#🧠 以redirect_uri 是用來提供獲取Token的script作為主要解說版本：implicit grant type 在OAuth 流程中的 "使用者訪問客戶端，客戶端將使用者導向認證伺服器來進行身份認證、授權詢問" ，請問請求封包源自於哪裡？發送至哪？形式為何？ ->->-> `形式為URI(URI參數)、封包，源自於客戶端所發送的請求封包，發送至認證伺服器`
<!--SR:!2024-02-03,172,230-->

#🧠 以redirect_uri 是用來提供獲取Token的script作為主要解說版本：implicit grant type 在OAuth 流程中的 "使用者訪問客戶端，客戶端將使用者導向認證伺服器來進行身份認證、授權詢問" ，請問使用者向認證伺服器發送授權請求的http動詞會是什麼？ ->->-> `GET`
<!--SR:!2024-04-23,248,250-->

#🧠  以redirect_uri 是用來提供獲取Token的script作為主要解說版本：implicit grant type 在OAuth 流程中的 "使用者訪問客戶端，客戶端將使用者導向認證伺服器來進行身份認證、授權詢問" ，請問主要參數為何？做什麼用 ->->-> `	- response_type： 表示授權類型為何 - client_id：表示客戶端應用程式在認證伺服器上所註冊的client_id - redirect_uri：定義哪邊提供Script或者哪邊接收token - scope：定義申請的權限範疇`
<!--SR:!2023-09-28,42,230-->

#🧠 以redirect_uri 是用來提供獲取Token的script作為主要解說版本：implicit grant type 在OAuth 流程中的 "使用者訪問客戶端，客戶端將使用者導向認證伺服器來進行身份認證、授權詢問" ，請問主要參數的response_type為申請授權類型，若是implicit版本，得填寫什麼？->->-> `token`
<!--SR:!2023-09-21,45,230-->

#🧠 以redirect_uri 是用來提供獲取Token的script作為主要解說版本：implicit grant type 在OAuth 流程中的 "使用者訪問客戶端，客戶端將使用者導向認證伺服器來進行身份認證、授權詢問" ，請問主要參數-response_type、client_id、redirect_uri、scope為何？ ->->-> `- response_type： 表示授權類型為何 - client_id：表示客戶端應用程式在認證伺服器上所註冊的client_id - redirect_uri：定義哪邊提供Script或者哪邊接收token - scope：定義申請的權限範疇`
<!--SR:!2023-09-04,28,210-->

#🧠 以redirect_uri 是用來提供獲取Token的script作為主要解說版本：implicit grant type 在OAuth 流程中的 "假設使用者允許授權並發送至認證伺服器，認證伺服器就將使用者導向客戶端是先指定的重導向URI，並在URI添加Fragment (裡面夾雜Hash格式構成的access token)"，請求封包源自於哪裡？發送至哪？  ->->-> `源自於認證伺服器，發送至重導向URI`
<!--SR:!2024-03-13,219,250-->

#🧠 以redirect_uri 是用來提供獲取Token的script作為主要解說版本：implicit grant type 在OAuth 流程中的 "假設使用者允許授權並發送至認證伺服器，認證伺服器就將使用者導向客戶端是先指定的重導向URI，並在URI添加Fragment (裡面夾雜Hash格式構成的access token)，請問會是以什麼http動詞來讓使用者向客戶端發送 ->->-> `GET`
<!--SR:!2024-04-12,237,250-->

#🧠 以redirect_uri 是用來提供獲取Token的script作為主要解說版本：implicit grant type 在OAuth 流程中的 "假設使用者允許授權並發送至認證伺服器，認證伺服器就將使用者導向客戶端是先指定的重導向URI，並在URI添加Fragment (裡面夾雜Hash格式構成的access token)"，主要內容為何？ ->->-> `- access_token：表示token - token_type：表示token種類 - expires_in：表示過期時間 - scope：表示token所擁有的使用權限`
<!--SR:!2024-02-10,160,230-->

#🧠 以redirect_uri 是用來提供獲取Token的script作為主要解說版本：implicit grant type 在OAuth 流程中的 "假設使用者允許授權並發送至認證伺服器，認證伺服器就將使用者導向客戶端是先指定的重導向URI，並在URI添加Fragment (裡面夾雜Hash格式構成的access token)"，主要參數-access_token、token_type、expires_in、scope是為何？ ->->-> `- access_token：表示token - token_type：表示token種類 - expires_in：表示過期時間 - scope：表示token所擁有的使用權限`
<!--SR:!2024-04-07,234,250-->


#🧠  implicit grant type 在OAuth下會需要設定grant_type？為什麼？ ->->-> `並不會，由於grant_type會是得讓使用者的授權同意授與客戶端來讓它發送索要token的請求，但該type並沒有，只是全都在使用者的瀏覽器進行授權同意和索要token`
<!--SR:!2023-11-11,142,250-->




---
Status: #🌱 
Tags:
[[OAuth]]
Links:
[[OAuth 會是標準、協定，其內容為如何在不需要將 "擁有資源使用權限的使用者帳密" 給予 特定服務A的情況下，發放資源使用權限給特定服務A來代表使用者去做特定事情]]
[[OAuth 中 的 Authentication Code Grant Type 是以authorization code和申請其code來分別作為認證授權伺服器能夠認可使用者授權的的結果物和流程]]
References:
[[@LiJieOAuthRuanYiFengDeWangLuoRiZhi]]