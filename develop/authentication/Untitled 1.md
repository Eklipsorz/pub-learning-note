## 描述



### server-side session

> server-side session： the server generates and store some unique identifier
> store unique identifier on server, send some identifier to client


重點：
- server-side session：每到驗證成功就在server產生session並存放對應使用者資料、接著賦予session id給予客戶端，客戶端在請求封包裡夾雜session id，當伺服器要驗證id就會透過id去找尋對應session，進而獲取進一步的資料和驗證。
-  帶來的好處就是：
	- 相較於較為的access，不容易偽造其access

  

壞處則是會需要伺服器額外處理空間成本和時間成本在session的儲存、管理、獲取、驗證上

  

適用場景為：

  

> it works great if your backend, your server and your front-end server are tightly coupled

> but
stateless 這規則不一定適用於所有API Server ，只是stateless給出的利會大於弊。




## 複習


---
Status: #🌱 
Tags:
[[Authentication]]
Links:
References: