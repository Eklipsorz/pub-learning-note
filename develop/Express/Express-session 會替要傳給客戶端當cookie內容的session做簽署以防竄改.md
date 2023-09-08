## 描述

當客戶端的cookie物件內容來使用session id 來告知伺服器哪一個伺服器的session 物件內容是要拿來處理這次的session時，若session id被篡改成其他客戶端與伺服器之間的session物件，那伺服器該如何防範？

在這裡的解法會是，當每次客戶端發出請求致使伺服器建立session時，

![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1650553317/blog/network/session/create-session-sign_mjqbsd.png)

 
原本伺服器會藉由Set-Cookie標頭封包來告知客戶端對應的sessionID是什麼(圖中會是1)，但在這裡會選擇將sessionID和伺服器所儲存的密鑰(secret)一起透過雜湊演算法來產生名為簽名(signature)的雜湊值，

![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1650553443/blog/network/session/sign-generate_grxsdm.png)

  
並將傳遞給客戶端的封包改成以下形式的字串，在這裡會是1.signature1，其中signature1是透過sessionID(=1)和密鑰而構成的，而當客戶端收到之後，就便建立cookie物件來存放sessionID和簽署所構成的字串。

```
Set-Cookie: sessionId=<session id>.<signature>
```

而當下次客戶端再次向同個伺服器發出請求時，便會把對應的cookie內容(此時會是1.signature1)附加至請求封包，

![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1650553317/blog/network/session/send-with-cookie-sign_n2hv2s.png)

  

而伺服器收到之後就會分別對sessionID和signature1進行處理，首先會先對收到的sessionID和伺服器的密鑰進行雜湊演算法獲取另一個簽名(signature')，並且將結果簽名值與接收過來的signature比較是否相同，若相同就代表著接收到的封包內容是未被竄改，未被竄改才會允許伺服器去找尋對應的session，否則就駁回

![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1650553936/blog/network/session/sign-compare_hfxe4p.png)

  

在這裡除非接收封包內的sessionID和signature都被改成相對應的組合(PS. sessionID透過同個算法和密鑰能夠得到同樣的signature)以外，否則只要任一改變就會被認定被惡意竄改而拒絕。此外，事實上這方法也藉由讓客戶端儲存要比較的結果簽名值來減少伺服器對空間需求。

## 複習

#🧠 express.session 為什麼需要密鑰？ ->->-> `防止客戶端的cookie被竄改或者使用非法的session`
<!--SR:!2023-09-29,21,250-->

#🧠 express.session 為什麼需要密鑰？其中的防止客戶端的cookie被竄改或者使用非法的session會是指甚麼? ->->-> `前者是客戶端的cookie內容被人修改，後者則是客戶端想用其他狀態`
<!--SR:!2023-09-11,3,250-->

#🧠 express-session 具體拿密鑰是如何防偽 ->->-> `首先當session一被建立，伺服器就會拿到對應的session id並且拿密鑰和session id進行hash算法來得到簽署值，接著拿session id和簽署值合併成一個新字串給客戶端當cookie的內容，當客戶端再次向同樣伺服器發送請求並夾帶著上次cookie內容時，伺服器就會拿cookie內容中的session Id和伺服器握有的密鑰進行再一次hash比對cookie內容中的簽署值是否一樣，若一樣的話，就表示客戶端cookie未被人惡意竄改，若不一樣就表示竄改`
<!--SR:!2023-09-28,20,250-->


---
Status: #🌱 
Tags:
[[Express]] - [[Session]]
Links: 
[[Express-Session 讓Express 伺服器能產生和管理對應的cookie和session]]
[[在沒有任何session的情況下，只要當req.session下任一屬性被寫入，express-session就會為它建立對應的cookie和session]]
References: