## 描述

### authentication token / access token
1. token 是由客戶端用來向伺服器索求受保護資源的驗證資料，並讓伺服器對其進行驗證，若驗證成功，伺服器就允許客戶端使用資源；若驗證失敗，伺服器就不允許客戶端使用資源
2. 該驗證資料會夾雜在客戶端的請求中，其夾雜的位置會是請求封包的以下位置：
	- header 部分：增加Authentication header，對應內容為bearer token，token前面會有bearer標誌
	- body 部分：以物件屬性來儲存token
	- query string部分：以token作為key，value為對應token實際內容

### 從哪個元件發送基於token的請求

發送請求的元件：
1. 由元件本身來發送
2. 由元件的parent元件本身來發送：在parent element定義callback並轉遞給元件當props，該callback會接收請求資料來處理，並於元件本身呼叫callback來代表parent element來處理

### authentication token vs. access token
1. authentication token 泛指夾雜著身分證明資訊的且要求伺服器驗證其身份證明的token
2. access token 單純是指代表特定資源之存取權限的資訊，誰擁有它誰就能存取特定資源


## 複習

#🧠 authentication token / access token 會夾雜在客戶端的請求中，請問具體位置為何？ ->->-> `header 部分、 body 部分、query string部分`

#🧠 authentication token vs. access token 差別？ ->->-> `1. authentication token 泛指夾雜著身分證明資訊的且要求伺服器驗證其身份證明的token2. access token 單純是指代表特定資源之存取權限的資訊，誰擁有它誰就能存取特定資源`

#🧠 authentication token / access token 會夾雜在客戶端的請求中，若具體位置為header部分的話，具體會是什麼？？ ->->-> `增加Authentication header，對應內容為bearer token，token前面會有bearer標誌`

#🧠 authentication token / access token 會夾雜在客戶端的請求中，若具體位置為body部分的話，具體會是什麼？？ ->->-> `以物件屬性來儲存token`

#🧠 authentication token / access token 會夾雜在客戶端的請求中，若具體位置為body部分的話，具體會是什麼？？ ->->-> `以物件屬性來儲存token`


---
Status: #🌱 
Tags:
[[Authentication]] - [[Authorization]]
Links:
References: