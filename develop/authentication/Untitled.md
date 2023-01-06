## 描述

###

token 在請求封包中會在以下任一位置：

1. header 部分：增加Authentication header，對應內容為bearer [[token]]，token前面會有bearer標誌

2. body 部分：以token作為屬性，以token實際內容為屬性實際內容

3. query string部分：以token作為key，value為對應token實際內容


###

發送請求的元件：

1. 表格本身來發送：在表格元件內定義請求並發送

2. 由表格的parent element來發送：在parent element定義callback，來接收請求資料來處理，並於表格本身呼叫callback來代表parent element來處理


###


returnSecureToken 為 true

> whether or not to return an ID and refresh token

> but it could be true if we want to get a new token in response

  

=> 替每個端點增加是否回傳新id token和refresh token的功能。




## 複習

---
Status: #🌱 
Tags:
[[Authentication]]
Links:
References: