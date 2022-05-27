
## 描述

### Express-Session

#### 它是什麼？用途是什麼
一種實現在express框架上的第三方套件，非官方套件，主要幫助開發者產生/管理對應的cookie和session


#### 安裝/設定方式
express-session 套件安裝方式：
```
npm install express-session
```

套件載入至主程式(伺服器)的方式：由於該套件是以middleware為主，該middleware會攔截請求封包並設定對應的cookie、session等資訊，設定為
```
// 替req增加屬性，如req.session
req.session = .....
req.cookie = .....
```

給後續middleware得知
```
// load express-session
// 其套件的回傳內容是本身是一個middleware function
const session = require('express-session')
app.use('/', seession( options ))

// other routes (other middleware functions)
app.method(path, callback)
app.method(path, callback)
.
.
```

所以若要讓其他的middleware能夠使用其功能所提供的session 功能，必須先將套件以app.use來使用其midddleware function並放置在其他middleware之前，就能攔截所有對應請求來做處理，或者在正式做處理之前就能先處理，如上例子。

#### session(options)的options是？


#### 如何實現產生/管理對應的cookie和session？
 具體來說，當載入該模組時，客戶端和伺服器端只要處於request/response cycle的話，就會建立session來紀錄兩者的連線過程，同時間會賦予session id 給該session並讓客戶端建立cookie去儲存session id，而到時cookie只要拿著這session id發送請求至伺服器，伺服器收到便拿該id獲取對應先前的連線過程是什麼。



---
Status: #🌱 
Tags:
[[Express]] 
Links:
References:
