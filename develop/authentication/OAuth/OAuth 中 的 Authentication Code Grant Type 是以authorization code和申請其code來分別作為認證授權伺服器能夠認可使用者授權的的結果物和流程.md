

## 描述


[[@LiJieOAuthRuanYiFengDeWangLuoRiZhi]]
> 授权码模式（authorization code）是功能最完整、流程最严密的授权模式。它的特点就是通过客户端的后台服务器，与"服务提供商"的认证服务器进行互动。

![授权码模式](https://www.ruanyifeng.com/blogimg/asset/2014/bg2014051204.png)

> 它的步骤如下：

> （A）用户访问客户端，后者将前者导向认证服务器。
> （B）用户选择是否给予客户端授权。
> （C）假设用户给予授权，认证服务器将用户导向客户端事先指定的"重定向URI"（redirection URI），同时附上一个授权码。
> （D）客户端收到授权码，附上早先的"重定向URI"，向认证服务器申请令牌。这一步是在客户端的后台的服务器上完成的，对用户不可见。
> （E）认证服务器核对了授权码和重定向URI，确认无误后，向客户端发送访问令牌（access token）和更新令牌（refresh token）。

重點：
- 在這裡會以authorization code和申請其code來分別作為認證授權伺服器能夠認可使用者授權的的結果物和流程
- 當使用者授與存取網路服務提供商的權利給應用服務A來存取時，其流程為：
	- A. 使用者訪問身為客戶端的應用服務A，應用服務A將使用者導向網路服務提供商之認證授權伺服器來認證使用者、詢問授權範疇、是否授權
		- 主要目的：透過導向方式來間接要求使用者發送相同同樣請求來向認證授權伺服器表示授權申請
		- 其導向請求會以URL (含URL參數)、封包 來進行，主要內容為授權種類、權限、申請授權作為認證用的重導向URL，並且轉由使用者發送同樣的請求至認證授權伺服器
	- B. 使用者在認證頁面同意授權給應用服務A
	- C. 假設使用者同意授權，認證授權伺服器會將使用者導向客戶端事先指定的URI並附上授權碼
		- 主要目的：透過導向方式來間接要求使用者發送授權成功的結果資料傳遞給應用服務A
		- 其導向請求會是以URL (含URL參數)、封包 來進行，主要內容為授權碼，並且轉由使用者發送同樣的請求至客戶端的應用服務A
	- D. 身為客戶端的應用服務A會從URI接收到授權碼，並向認證授權伺服器以該token、redirect_uri、client_id發送索要token請求
		- 主要目的：讓應用服務A向認證授權伺服器發送索要token的請求
		- 其請求會是以URL和其URL參數、封包來進行，主要會附加授權碼、當初申請授權碼的重導向URL、當初申請授權碼的client_id
	- E. 認證授權用的伺服器會從中驗證授權碼和當初申請授權碼的重導向URL是否正確無誤，若無誤，就會向客戶端的應用服務A發送access token和refresh token。

![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1679145847/blog/OAuth/OAuth-with-code_bn5ih9.png)


###  步驟A所需的參數

[[@LiJieOAuthRuanYiFengDeWangLuoRiZhi]]
> A步骤中，客户端申请认证的URI，包含以下参数：

> -   response_type：表示授权类型，必选项，此处的值固定为"code"
> -   client_id：表示客户端的ID，必选项
> -   redirect_uri：表示重定向URI，可选项
> -   scope：表示申请的权限范围，可选项
> -   state：表示客户端的当前状态，可以指定任意值，认证服务器会原封不动地返回这个值。

> 下面是一个例子。
```
GET /authorize?response_type=code&client_id=s6BhdRkqt3&state=xyz
         &redirect_uri=https%3A%2F%2Fclient%2Eexample%2Ecom%2Fcb HTTP/1.1

Host: server.example.com
```


重點：
- 步驟A： 使用者訪問身為客戶端的應用服務A，應用服務A將使用者導向網路服務提供商之認證授權伺服器
- 首先當使用者訪問應用服務A，應用服務A就會以下面導向請求來要求使用者發送其請求至認證授權伺服器
	- 請求形式為：URI(URI參數)、封包
	- 參數會有：
		- response_type：申請什麼樣的授權類型
		- client_id：指定客戶端的應用程式A在網路服務提供商所註冊的client_id
		- redirect_uri：申請之後應用程式接收code的重導向頁面
		- scope：申請授權資料所能擁有的權限為何
		- state：表示客戶端的應用程式A所擁有的狀態
	- 細節：
		- 只有response_type、client_id會是必填
		- redirect_uri為可選，可以在網路服務提供商那邊事先申請
		- scope為可選，主要會以提供使用者決定權限的表單為主
		- state為可選
```
// URL
GET /authorize?response_type=type1&client_id=id1&redirect_uri=uri1
HOST: server.example.com
```

###  步驟C所需的參數
> C步骤中，服务器回应客户端的URI，包含以下参数：

> -   code：表示授权码，必选项。该码的有效期应该很短，通常设为10分钟，客户端只能使用该码一次，否则会被授权服务器拒绝。该码与客户端ID和重定向URI，是一一对应关系。
> -   state：如果客户端的请求中包含这个参数，认证服务器的回应也必须一模一样包含这个参数。

> 下面是一个例子。
```
HTTP/1.1 302 Found
Location: https://client.example.com/cb?code=SplxlOBeZQQYbYS6WxSbIA&state=xyz
```

重點：
- 步驟C：假設使用者同意授權，認證授權伺服器會將使用者導向客戶端事先指定的URI並附上授權碼
	- 請求形式為：URI(含URI參數)、封包
	- 參數會有：
		- code：表示認證授權伺服器授與的授權碼，主要是要讓應用服務A申請token
		- state：客戶端目前所處的狀態，會延續上一個步驟A所傳遞過來的
	```
	HTTP/1.1 302 Found
	Location: https://client.example.com/cb?code=SplxlOBeZQQYbYS6WxSbIA&state=xyz
	```
	- 參數細節：
		- 導向的端點正是為客戶端用來接收code的重導向URI
		- 授權碼code 和 代表權限的 token 是不一樣，前者是用來申請token。
		- 授權碼的限制為：有效時間通常很短，如10分鐘、用碼申請token的次數是有限的，如1次，若違反限制，就會在申請token過程中被拒絕

### 步驟D所需的參數
> D步骤中，客户端向认证服务器申请令牌的HTTP请求，包含以下参数：

> -   grant_type：表示使用的授权模式，必选项，此处的值固定为"authorization_code"。
> -   code：表示上一步获得的授权码，必选项。
> -   redirect_uri：表示重定向URI，必选项，且必须与A步骤中的该参数值保持一致。
> -   client_id：表示客户端ID，必选项。

> 下面是一个例子。

```
POST /token HTTP/1.1
Host: server.example.com
Authorization: Basic czZCaGRSa3F0MzpnWDFmQmF0M2JW
Content-Type: application/x-www-form-urlencoded

grant_type=authorization_code&code=SplxlOBeZQQYbYS6WxSbIA&redirect_uri=https%3A%2F%2Fclient%2Eexample%2Ecom%2Fcb 
```

重點：
- 步驟D：身為客戶端的應用服務A會從URI接收到授權碼，並向認證授權伺服器以該token、redirect_uri、client_id發送索要token請求
	- 請求形式為：封包
	- 參數會有：
		- grant_type：定義要使用何種方式來授權，這裡會是authorization_code
		- code：用來申請token用的授權碼
		- redirect_uri：是指當初應用程式A接收code用的重導向URI，主要會與步驟A、步驟C的重導向URI保持一致
		- client_id：應用程式A在認證授權伺服器中所註冊的client_id
	```
	POST /token HTTP/1.1
	Host: server.example.com
	Authorization: Basic czZCaGRSa3F0MzpnWDFmQmF0M2JW
	Content-Type: application/x-www-form-urlencoded
	
	grant_type=authorization_code&code=SplxlOBeZQQYbYS6WxSbIA&redirect_uri=https%3A%2F%2Fclient%2Eexample%2Ecom%2Fcb 
	```


### 步驟E所需的參數
> E步骤中，认证服务器发送的HTTP回复，包含以下参数：

> -   access_token：表示访问令牌，必选项。
> -   token_type：表示令牌类型，该值大小写不敏感，必选项，可以是bearer类型或mac类型。
> -   expires_in：表示过期时间，单位为秒。如果省略该参数，必须其他方式设置过期时间。
> -   refresh_token：表示更新令牌，用来获取下一次的访问令牌，可选项。
> -   scope：表示权限范围，如果与客户端申请的范围一致，此项可省略。

下面是一个例子。

```
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

> 从上面代码可以看到，相关参数使用JSON格式发送（Content-Type: application/json）。此外，HTTP头信息中明确指定不得缓存。

重點：
- 步驟E：認證授權用的伺服器會從中驗證授權碼和當初申請授權碼的重導向URL是否正確無誤，若無誤，就會向客戶端的應用服務A發送access token和refresh token。
- 主要會回傳一份回應封包，裡面會有：
	- access_token：表示其使用者授予權限的token
	- token_type：表示token種類，可以是bearer類型
	- expires_in：表示過期時間，單位為秒
	- refresh_token：表示用來申請access-token的token
	- scope：表示access_token被授與的權限為何
```
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


#🧠 authorization code grant type 在OAuth  流程中的 "使用者訪問身為客戶端的應用服務A，應用服務A將使用者導向網路服務提供商之認證授權伺服器來認證使用者、詢問授權範疇、是否授權" ，請問主要參數的response_type為申請授權類型，若是authorization code grant type 版本，得填寫什麼？->->-> `code`
<!--SR:!2024-03-18,214,250-->

#🧠 authorization code grant type 在OAuth 上是以什麼形式來讓認證授權伺服器認可為使用者合法授權的結果？ ->->-> `以authorization code的形式`
<!--SR:!2024-03-22,209,248-->


#🧠 authorization code grant type 在OAuth 上的授權流程為何？在這裡會有(網路服務提供商)Authorization Server、(應用服務A)Client、(使用者)Resource Owner、User Agent 以及 當使用者授與存取網路服務提供商的權利給應用服務A來存取時->->-> `使用者訪問身為客戶端的應用服務A，應用服務A將使用者導向網路服務提供商之認證授權伺服器來認證使用者、詢問授權範疇、是否授權 -> 使用者在認證頁面同意授權給應用服務A -> 假設使用者同意授權，認證授權伺服器會將使用者導向客戶端事先指定的URI並附上授權碼 -> 身為客戶端的應用服務A會從URI接收到授權碼，並向認證授權伺服器以該token、redirect_uri、client_id發送索要tokem請求 -> 認證授權用的伺服器會從中驗證授權碼和當初申請授權碼的重導向URL是否正確無誤，若無誤，就會向客戶端的應用服務A發送access token和refresh token。`
<!--SR:!2024-04-01,228,250-->

#🧠 authorization code grant type 在OAuth 上的授權流程為何？在這裡會有(網路服務提供商)Authorization Server、(應用服務A)Client、(使用者)Resource Owner、User Agent 以及 當使用者授與存取網路服務提供商的權利給應用服務A來存取時 ，請畫圖來表示->->-> ![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1679145847/blog/OAuth/OAuth-with-code_bn5ih9.png)
<!--SR:!2024-03-17,213,250-->



#🧠 authorization code grant type 在OAuth 上的授權流程中："使用者訪問身為客戶端的應用服務A，應用服務A將使用者導向網路服務提供商之認證授權伺服器來認證使用者、詢問授權範疇、是否授權"，導向和主要目的的關係是如何？ ->->-> `透過導向方式來間接要求使用者發送相同同樣請求來向認證授權伺服器表示授權申請`
<!--SR:!2024-02-19,196,250-->

#🧠 authorization code grant type 在OAuth 上的授權流程中："假設使用者同意授權，認證授權伺服器會將使用者導向客戶端事先指定的URI並附上授權碼"，導向和主要目的的關係是如何？ ->->-> `透過導向方式來間接要求使用者發送授權成功的結果資料傳遞給應用服務A`
<!--SR:!2024-04-03,230,250-->

#🧠 authorization code grant type 在OAuth 上的授權流程中："身為客戶端的應用服務A會從URI接收到授權碼，並向認證授權伺服器以該code、redirect_uri、client_id發送索要token請求"，主要目的的關係是如何？->->-> `讓應用服務A向認證授權伺服器發送索要token的請求`
<!--SR:!2024-04-22,240,250-->

#🧠 authorization code grant type 在OAuth 上的授權流程中："使用者訪問身為客戶端的應用服務A，應用服務A將使用者導向網路服務提供商之認證授權伺服器來認證使用者、詢問授權範疇、是否授權"，應用服務A發送過來的導向請求形式會是什麼？內容又會是什麼？對於使用者來說是什麼意思 ->->-> `其導向請求會是以URL (含URL參數)、封包 來進行，主要內容為授權申請的資料，透過導向方式來間接要求使用者發送相同同樣請求來向認證授權伺服器表示授權申請`
<!--SR:!2024-03-27,218,250-->

#🧠 authorization code grant type 在OAuth 上的授權流程中："假設使用者同意授權，認證授權伺服器會將使用者導向客戶端事先指定的URI並附上授權碼"，認證授權伺服器發送過來的導向請求形式會是什麼？內容又會是什麼？對於使用者來說是什麼意思? ->->-> ` 其導向請求會是以URL (含URL參數)、封包 來進行，主要內容為授權碼，並且轉由使用者發送同樣的請求至客戶端的應用服務A`
<!--SR:!2023-11-17,148,250-->

#🧠 authorization code grant type 在OAuth 上的授權流程中："假設使用者同意授權，認證授權伺服器會將使用者導向客戶端事先指定的URI並附上授權碼"，使用者向客戶端發送封包，請問HTTP動詞是為何？ ->->-> `GET`
<!--SR:!2024-04-08,235,249-->


#🧠 authorization code grant type 在OAuth 上的授權流程中："身為客戶端的應用服務A會從URI接收到授權碼，並向認證授權伺服器以該code、redirect_uri、client_id發送索要token請求"，應用服務A發送過來的導向請求形式會是什麼？內容又會是什麼？->->-> `其請求會是以封包來進行，主要會在封包內部附加授權碼、當初申請授權碼的重導向URL、當初申請授權碼的client_id`
<!--SR:!2024-03-13,209,249-->


#🧠 authorization code grant type 在OAuth 上的授權流程中："使用者訪問身為客戶端的應用服務A，應用服務A將使用者導向網路服務提供商之認證授權伺服器來認證使用者、詢問授權範疇、是否授權"，這步驟所發送的請求是從何而來？發送至哪 ->->-> `從應用服務A發送過來的請求，以指定的請求封包內容來要求使用者向認證授權伺服器發送。會發送至認證授權伺服器`
<!--SR:!2024-04-19,240,250-->

#🧠 authorization code grant type 在OAuth 上的授權流程中："使用者訪問身為客戶端的應用服務A，應用服務A將使用者導向網路服務提供商之認證授權伺服器來認證使用者、詢問授權範疇、是否授權"，這步驟所需要的參數為何？ ->->-> `response_type：申請什麼樣的授權類型 - client_id：指定客戶端的應用程式A在網路服務提供商所註冊的client_id - redirect_uri：申請之後應用程式接收code的重導向頁面 - scope：申請授權資料所能擁有的權限為何 - state：表示客戶端的應用程式A所擁有的狀態`
<!--SR:!2024-01-19,155,230-->

#🧠 authorization code grant type 在OAuth 上的授權流程中："使用者訪問身為客戶端的應用服務A，應用服務A將使用者導向網路服務提供商之認證授權伺服器來認證使用者、詢問授權範疇、是否授權"，這步驟所需要的參數-response_type、client_id、redirect_uri、scope、state是為何？ ->->-> `response_type：申請什麼樣的授權類型 - client_id：指定客戶端的應用程式A在網路服務提供商所註冊的client_id - redirect_uri：申請之後應用程式接收code的重導向頁面 - scope：申請授權資料所能擁有的權限為何 - state：表示客戶端的應用程式A所擁有的狀態`
<!--SR:!2023-11-14,137,230-->


#🧠 authorization code grant type 在OAuth 上的授權流程中："使用者訪問身為客戶端的應用服務A，應用服務A將使用者導向網路服務提供商之認證授權伺服器來認證使用者、詢問授權範疇、是否授權"，這步驟所需要的必填參數會是什麼？ ->->-> `response_type、client_id`
<!--SR:!2024-03-20,216,250-->

#🧠 authorization code grant type 在OAuth 上的授權流程中："使用者訪問身為客戶端的應用服務A，應用服務A將使用者導向網路服務提供商之認證授權伺服器來認證使用者、詢問授權範疇、是否授權"，這步驟所需要的參數-redirect_uri為何是可選填參數？ ->->-> `redirect_uri為可選，可以在網路服務提供商那邊事先申請`
<!--SR:!2023-10-06,41,230-->

#🧠 authorization code grant type 在OAuth 上的授權流程中："使用者訪問身為客戶端的應用服務A，應用服務A將使用者導向網路服務提供商之認證授權伺服器來認證使用者、詢問授權範疇、是否授權"，這步驟所需要的參數-scope為何是可選填參數？ ->->-> `可以在網路服務提供商那邊事先申請`
<!--SR:!2023-09-21,17,245-->



#🧠 authorization code grant type 在OAuth 上的授權流程中："使用者訪問身為客戶端的應用服務A，應用服務A將使用者導向網路服務提供商之認證授權伺服器來認證使用者、詢問授權範疇、是否授權"，從應用服務A發送過來的導向請求會是什麼？舉例來說，假如認證授權伺服器為server.example.com，端點為authorize ->->-> `GET server.example.com/authorize?response_type=type1&client_id=id1&redirect_uri=uri1`
<!--SR:!2024-01-17,163,230-->

#🧠  authorization code grant type 在OAuth 上的授權流程中："假設使用者同意授權，認證授權伺服器會將使用者導向客戶端事先指定的URI並附上授權碼"，該步驟所需要的參數會是什麼？->->-> `		- code：表示認證授權伺服器授與的授權碼，主要是要讓應用服務A申請token - state：客戶端目前所處的狀態，會延續上一個步驟A所傳遞過來的`
<!--SR:!2023-09-18,43,230-->

#🧠  authorization code grant type 在OAuth 上的授權流程中："假設使用者同意授權，認證授權伺服器會將使用者導向客戶端事先指定的URI並附上授權碼"，其授權碼就是代表使用者權限的token嗎？->->-> `並不是`
<!--SR:!2024-02-20,198,250-->



#🧠  authorization code grant type 在OAuth 上的授權流程中：token 和 authorization code 之間的差別是什麼？->->-> `前者是代表特定身份所擁有的使用權限，後者則是用來申請token的代碼，其本身代表著使用者對於授權的許可證明`
<!--SR:!2024-01-19,165,230-->


#🧠 authorization code grant type 在OAuth 上的授權流程中：authorization code 本身限制是什麼？ ->->-> `有效時間通常很短，如10分鐘、用碼申請token的次數是有限的，如1次`
<!--SR:!2024-01-21,148,230-->


#🧠 authorization code grant type 在OAuth 上的授權流程中：authorization code 使用限制是有效時間通常很短，如10分鐘、用碼申請token的次數是有限的，如1次，若違反限制的話，會如何？ ->->-> `若違反限制，就會在申請token過程中被拒絕`
<!--SR:!2024-03-14,220,250-->


#🧠 authorization code grant type 在OAuth 上的授權流程中："假設使用者同意授權，認證授權伺服器會將使用者導向客戶端事先指定的URI並附上授權碼"，其導向請求源自哪裡？ 會發送至哪？->->-> `源自於認證授權伺服器發過來的導向請求，會發送至client指定接收code的地點`
<!--SR:!2024-04-21,246,250-->


#🧠 authorization code grant type 在OAuth 上的授權流程中："身為客戶端的應用服務A會從URI接收到授權碼，並向認證授權伺服器以該code來向認證伺服器索要token請求"，請求中的參數會是如何？ ->->-> `		- grant_type：定義要使用何種方式來授權，這裡會是authorization_code - code：用來申請token用的授權碼 - redirect_uri：是指當初應用程式A接收code用的重導向URI，主要會與步驟A、步驟C的重導向URI保持一致 - client_id：應用程式A在認證授權伺服器中所註冊的client_id`
<!--SR:!2023-10-12,25,190-->


#🧠 authorization code grant type 在OAuth 上的授權流程中："身為客戶端的應用服務A會從URI接收到授權碼，並向認證授權伺服器以該token、redirect_uri、client_id發送索要token請求"，請求中的參數- grant_type 、code、redirect_uri、client_id是什麼？ ->->-> `		- grant_type：定義要使用何種方式來授權，這裡會是authorization_code - code：用來申請token用的授權碼 - redirect_uri：是指當初應用程式A接收code用的重導向URI，主要會與步驟A、步驟C的重導向URI保持一致 - client_id：應用程式A在認證授權伺服器中所註冊的client_id`
<!--SR:!2023-11-12,143,250-->

#🧠 authorization code grant type 在OAuth 上的授權流程中："身為客戶端的應用服務A會從URI接收到授權碼，並向認證授權伺服器以該redirect_uri、client_id發送索要token請求"，請求中的參數為何需要redirect_uri、client、code ->->-> `需要驗證該應用服務是否為當初向使用者發送授權申請`
<!--SR:!2024-03-23,223,250-->

#🧠  authorization code grant type 在OAuth 上的授權流程中："認證授權用的伺服器會從中驗證授權碼和當初申請授權碼的重導向URL是否正確無誤，若無誤，就會向客戶端的應用服務A發送access token和refresh token"，認證授權伺服器發送過來的回應封包會有哪些內容？ ->->-> `	- access_token：表示其使用者授予權限的token - token_type：表示token種類，可以是bearer類型 - expires_in：表示過期時間，單位為秒 - refresh_token：表示用來申請access-token的token - scope：表示access_token被授與的權限為何`
<!--SR:!2024-04-20,241,250-->

#🧠  authorization code grant type 在OAuth 上的授權流程中："身為客戶端的應用服務A會從URI接收到授權碼，並向認證授權伺服器以該token、redirect_uri、client_id發送索要token請求"，其中的grant_type 會是定義為？ ->->-> ` authorization_code`
<!--SR:!2024-02-13,190,249-->


#🧠  authorization code grant type 在OAuth 上的授權流程中："身為客戶端的應用服務A會從URI接收到授權碼，並向認證授權伺服器以code、redirect_uri、client_id發送索要token請求"，其中應用程式A會以什麼http動詞來向伺服器發送token索求 ->->-> `POST`
<!--SR:!2024-04-10,228,249-->



---
Status: #🌱 
Tags:
[[OAuth]]
Links:
References:
[[@OAuthGrantTypes]]
[[@LiJieOAuthRuanYiFengDeWangLuoRiZhi]]




