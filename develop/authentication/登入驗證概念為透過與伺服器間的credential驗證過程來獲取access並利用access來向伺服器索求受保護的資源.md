## 描述


### authentication 命名緣由
> the process of proving that something is real, true, or what people say it is
> 驗證，認證

重點：
- 證明特定事物是正確、真的的過程

### credential  命名緣由
> a piece of information that is sent from one computer to another to check that a user is who they claim to be or to allow someone to see information

重點：
- 用來證明合法使用者的資訊





###  伺服器和客戶端之間為何需要authentication


> authentication is needed if content should be protected (not accessible by everyone)

由於以下狀況是常見的，為了實現，需要authentication概念來實現
1.  內容肯定會有只限於特定人士才能存取和所有都能存取的



### 內容根據存取的區分


網頁內容基本上根據存取權限區分成以下，在這裡內容會是指的是前端部分的畫面、API能提供的資料、服務：
1. 一種分為不用授權存取就能獲取的內容；
2. 另一個需要授權存取才能獲取的內容。比如特定使用者的個人資料編輯。




### authentication 概念

> how does authentication then work in general. In general, authentication is a two-step process：
> 1. Get access/permission
> 2. Send request to protected resource


重點：
- authentication 實現概念上是具有以下兩個步驟
	- Get access/permission。
	- Send request to protected resource with access/permission。
- Get access/permission：
	- 從特定認證方式輸入自己的credential來驗證，若驗證成功就獲取permission或者access；若驗證失敗就不允許獲取
	- 案例：認證方式通常會是使用帳號密碼來作為credential 證明自己是合法使用者的資料，若是的話，會事先將合法的帳號密碼儲存在後端伺服器或者資料庫來方便驗證使用者所輸入的帳密是否一致，一致就給予代表access或者permission的資料；不一致就報錯
- Send request to protected resource with access/permission：
	- 憑藉著從第一階段獲取到的access或者permission來向伺服器所求被保護的資料，伺服器收到會驗證access或者permission的合法性，若合法就允許存取；若不合法就不允許存取
  
  

### 能夠代表 access/permission的事物

若客戶端提供crediental 來驗證並獲取回應，並以回應來作為存取受保護資源的權力依據，主要回應分為以下幾種：
- 使用固定字串的回應，比如yes/no，yes代表驗證成功，no代表未驗證或者驗證失敗，並在請求封包添加yes來發送，伺服器看到yes就直接放行存取。 但很容易被人偽造身份
- server-side session中的session id
- authentication token中的token


####  authentication為何出現以下這兩個方法- server-side session中的session id - authentication token中的token


主要是為了檢測客戶端的資料被人惡意竄改而假冒他人





## 複習

#🧠 authentication 命名緣由為何？ ->->-> `證明特定事物是正確、真的的過程`
<!--SR:!2023-10-19,181,250-->

#🧠 credential 命名緣由為何？ ->->-> `用來證明合法使用者的資訊`
<!--SR:!2024-03-02,202,230-->

#🧠  伺服器和客戶端之間為何需要authentication？ ->->-> `內容肯定會有只限於特定人士才能存取和所有都能存取的`
<!--SR:!2023-10-20,180,250-->

#🧠 伺服器和客戶端之間的內容肯定會有只限於特定人士才能存取和所有都能存取的，那麼要如何實現限制呢？ ->->-> `authentication概念來實現`
<!--SR:!2024-02-08,192,230-->


#🧠 伺服器和客戶端之間的內容肯定會有只限於特定人士才能存取和所有都能存取的，那麼哪些應用服務頁面或者服務是限定特定人士才能存取，舉例？->->-> `比如特定使用者的個人資料編輯`
<!--SR:!2024-02-09,187,230-->

#🧠 伺服器和客戶端之間的內容肯定會有只限於特定人士才能存取和所有都能存取的，那麼哪些是限定特定人士才能存取，內容會是什麼？ (包含前後端)->->-> `前端部分的畫面、API能提供的資料、服務`
<!--SR:!2024-04-24,234,230-->

#🧠 伺服器和客戶端之間的內容肯定會有只限於特定人士才能存取和所有都能存取的，那麼哪些是限定特定人士才能存取，內容會是什麼？- ->->-> `前端部分的畫面、API能提供的資料、服務`
<!--SR:!2023-12-19,139,190-->

#🧠 authentication 在電腦科學上的通用概念為何？->->-> `	- Get access/permission。 - Send request to protected resource with access/permission。`
<!--SR:!2024-04-20,284,250-->

#🧠 authentication 通用概念為- Get access/permission。 - Send request to protected resource with access/permission，請問前者具體為何？ ->->-> `從特定認證方式輸入自己的credential來驗證，若驗證成功就獲取permission或者access；若驗證失敗就不允許獲取`
<!--SR:!2023-11-20,198,250-->

#🧠 authentication 通用概念為- Get access/permission。 - Send request to protected resource with access/permission，請問後者具體為何？:->->-> `憑藉著從Get access/permissionㄐ獲取到的access或者permission來向伺服器所求被保護的資料，伺服器收到會驗證access或者permission的合法性，若合法就允許存取；若不合法就不允許存取`
<!--SR:!2023-11-09,121,230-->

#🧠 authentication 通用概念為- Get access/permission。 - Send request to protected resource with access/permission，請舉例來說明前者 ->->-> `認證方式通常會是使用帳號密碼來作為credential 證明自己是合法使用者的資料，若是的話，會事先將合法的帳號密碼儲存在後端伺服器或者資料庫來方便驗證使用者所輸入的帳密是否一致，一致就給予代表access或者permission的資料；不一致就報錯`
<!--SR:!2024-06-06,311,250-->

#🧠 authentication 所採用的access/permission為何不能用固定字串和credential來表示？->->-> `很容易被人偽造身份`
<!--SR:!2024-08-19,363,250-->



#🧠 authentication 通用概念為- Get access/permission。 - Send request to protected resource with access/permission，能夠代表access/permission的事物具體可以會是什麼？ ->->-> `使用固定字串的回應、server-side session的session id、authentication token中的token`
<!--SR:!2023-11-16,128,210-->

#🧠 authentication 通用概念為- Get access/permission。 - Send request to protected resource with access/permission，access/permission是什麼意思？ ->->-> `作為存取受保護資源的權力依據`
<!--SR:!2023-10-16,97,190-->

`````````````````````````````
```#🧠 authentication的access/permission產生：為何出現以下這兩個方法- server-side session中的session id - authentication token中的token ->->-> `主要是為了檢測客戶端的資料被人惡意竄改而假冒他人`
<!--SR:!2023-01-26,18,250-->

#🧠  authentication的access/permission產生：使用固定字串的回應、 server-side session中的session id、authentication token中的token，哪一個能解決若代表permission資料被其他惡意主機奪走？為何能解決？->->-> `都沒有，這些最主要面向於前端所儲存的資訊是否被人惡意竄改成其他人。`
<!--SR:!2023-06-28,111,250-->



---
Status: #🌱 
Tags:
[[Authentication]]
Links:
References: