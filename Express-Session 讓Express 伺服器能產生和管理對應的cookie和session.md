
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
1. Options 是藉由物件來設定Express-Session所提供的middleware

2. 該物件常用的屬性為：
- store: 定義session儲存在哪？選項有內建的MemoryStore、資料庫、redis
- secret：一組字串，用來簽署每個儲存session id的cookie以及用該字串來解開每個被簽署過後的cookie是否由該伺服器所建立的cookie

- name：字串，設定由模組建立的cookie 所擁有的名字。

- saveUninitialized：布林值，原本當客戶端與伺服器開始進行連線時，就會開始建立session物件來紀錄兩者在連線時的狀態，且剛建立的session物件的屬性未在伺服器中被任意值來寫入，此session就會被當作未初始化的session，而若saveUninitialized被設定為true時，就便會將未初始化的session儲存在伺服器的session store，而saveUninitialized被設定為false時，就便不會將未初始化的session儲存在伺服器session store。 true是會強制儲存未初始化的session至伺服器中的session store以及替客戶端建立儲存對應session id的cookie，false是不會強制儲存。

> When an empty session object is created and no properties are set, it is the uninitialized state. So, setting saveUninitialized to false will not save the session if it is not modified.

- resave：布林值，若設為true，每一次客戶端和伺服器之間只要出現連線互動，所對應的session都會強制繼續存在session store，在請求過程中，無論對應session內容是否有被伺服器修改，也都會繼續存至session store，若為false，則不會只因為出現連線互動而強制保留對應的session至session store

3. 需要注意的點：

- 伺服器要求客戶端儲存session id至cookie時，此cookie會被稱之為session id cookie

#### 如何實現產生/管理對應的cookie和session？
 具體來說，當載入該模組時，客戶端和伺服器端只要處於request/response cycle的話，就會建立session來紀錄兩者的連線過程，同時間會賦予session id 給該session並讓客戶端建立cookie去儲存session id，而到時cookie只要拿著這session id發送請求至伺服器，伺服器收到便拿該id獲取對應先前的連線過程是什麼。



---
Status: #🌱 
Tags:
[[Express]] 
Links:

References:
