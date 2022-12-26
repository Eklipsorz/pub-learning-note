## 描述


### 

為何需要authentication

authentication is needed if content should be protected (not accessible by everyone)


### 
content can be different things.

  

一種分為不用授權存取就能獲取的內容；另一個需要授權存取才能獲取的內容。比如特定使用者的個人資料編輯。在這裡內容會是指的是前端部分的畫面、API能提供的資料、服務

###


how does authentication then work in general.

In general, authentication is a two-step process：

1. Get access/permission：從特定認證方式輸入自己的credential來驗證，若驗證成功就獲取permission或者access；若驗證失敗就不允許獲取。認證方式通常會是使用帳號密碼來作為credential 證明自己是合法使用者的資料，若是的話，會事先將合法的帳號密碼儲存在後端伺服器或者資料庫來方便驗證使用者所輸入的帳密是否一致，一致就給予代表access或者permission的資料；不一致就報錯

2. Send request to protected resource：憑藉著從第一階段獲取到的access或者permission來索要被保護的資料，存取前會要求驗證代表permission或者access的資料 來驗證、驗證成功才允許存取；驗證失敗就不允許存取  
  
  
the process of proving that something is real, true, or what people say it is

驗證，認證

  

credential  
  
a piece of information that is sent from one computer to another to check that a user is who they claim to be or to allow someone to see information


###

1. Get access/permission

2. Send request to protected resource

  

若客戶端提供crediental 來驗證並獲取回應，並以回應來作為存取受保護資源的權力依據：

- 若回應本身過於太簡單，比如yes/no，會容易被其他外人偽造成合法者去存取受保護資源，比如在請求封包添加yes來發送，伺服器看到yes就直接放行存取

- server-side session

- authentication token


## 複習



---
Status: #🌱 
Tags:
[[Authentication]]
Links:
References: