## 描述

### authentication token 
1. token 是由客戶端用來向伺服器索求受保護資源的識別字
2. 該識別字會在客戶端的請求中出現，其夾雜的位置會是請求封包的以下位置：
	- header 部分：增加Authentication header，對應內容為bearer token，token前面會有bearer標誌
	- body 部分：以token作為屬性，以token實際內容為屬性實際內容
	- query string部分：以token作為key，value為對應token實際內容

### 從哪個元件發送基於token的請求

發送請求的元件：
1. 由元件本身來發送
2. 由元件的parent元件本身來發送：在parent element定義callback並轉遞給元件當props，該callback會接收請求資料來處理，並於元件本身呼叫callback來代表parent element來處理







## 複習

---
Status: #🌱 
Tags:
[[Authentication]]
Links:
References: