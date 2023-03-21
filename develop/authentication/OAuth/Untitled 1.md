
## 描述


由於會讓客戶端憑著使用者授權來索要token，所以
- authorization code grant type：會讓客戶端憑著使用者授權的資料來索要
	- 使用者授權的資料：authorization code 
	- grant_type：authorization_code
-  implicit grant type：由於不會讓客戶端憑著使用者授權，只是單方面在瀏覽器進行授權和索要token
- resource owner password credentials grant type：會讓客戶端憑著代表使用者授權的資料來索要
	- 使用者授權的資料： resource owner password credential
	- grant_type：password


## 複習

---
Status: #🌱 
Tags:
[[OAuth]]
Links:
[[implicit grant type 在OAuth 上是以與Authorization code grant type版本來說相對簡化的模式，該模式主要不通過第三方應用程式或Client來進行授權碼，並直接在瀏覽器上向認證服務器上申請token]]
[[OAuth 中 的 Authentication Code Grant Type 是以authorization code和申請其code來分別作為認證授權伺服器能夠認可使用者授權的的結果物和流程]]
[[OAuth 會是標準、協定，其內容為如何在不需要將 "擁有資源使用權限的使用者帳密" 給予 特定服務A的情況下，發放資源使用權限給特定服務A來代表使用者去做特定事情]]
References: