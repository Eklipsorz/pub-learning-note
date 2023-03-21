
## 描述


### 客戶端是否憑著使用者同意授權來索要token


由於會讓客戶端憑著使用者同意授權來索要token，所以
- authorization code grant type：會讓客戶端憑著使用者授權的資料來索要
	- 授權的資料：authorization code ，代表著使用者授權同意
	- grant_type：authorization_code
-  implicit grant type：由於不會讓客戶端憑著使用者授權，只是單方面在瀏覽器進行授權和索要token
- resource owner password credentials grant type：會讓客戶端憑著代表使用者授權的資料來索要
	- 授權的資料： resource owner password credential，代表著使用者授權同意
	- grant_type：password
- client credentials grant type：本身並不會依據使用者同意授權來索要，而是以client 授權 自己的結果來索求token
	- 授權的資料：client credentials ，代表著客戶端授權同意自己
	- grant_type：client_credentials

### 流程下所會用到的http動詞和資料形式

- 所有指示特定對象導向至特定頁面：
	- http 動詞：GET
	- 封裝請求資料/結果資料形式：以URI、封包為主
- authorization code grant type 以授權同意結果來向認證伺服器索求token：
	- http 動詞：POST
	- 封裝請求資料/結果資料形式：以封包為主
- implitic grant type 皆以GET為http 動詞，並以URI、封包為主，包含以授權同意結果來向認證伺服器索求token亦是如此。
- resource owner password credentials grant type 以授權同意結果來向認證伺服器索求token：
	- http 動詞：POST
	- 封裝請求資料/結果資料形式：以封包為主
- client credentials grant type 授權同意結果來向認證伺服器索求token
	- http 動詞：POST
	- 封裝請求資料/結果資料形式：以封包為主



## 複習

#🧠 Question :: ->->-> ``







---
Status: #🌱 
Tags:
[[OAuth]]
Links:
[[implicit grant type 在OAuth 上是以與Authorization code grant type版本來說相對簡化的模式，該模式主要不通過第三方應用程式或Client來進行授權碼，並直接在瀏覽器上向認證服務器上申請token]]
[[OAuth 中 的 Authentication Code Grant Type 是以authorization code和申請其code來分別作為認證授權伺服器能夠認可使用者授權的的結果物和流程]]
[[OAuth 會是標準、協定，其內容為如何在不需要將 "擁有資源使用權限的使用者帳密" 給予 特定服務A的情況下，發放資源使用權限給特定服務A來代表使用者去做特定事情]]
References: