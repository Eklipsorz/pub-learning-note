
## 描述

### Express-Session

#### 它是什麼？用途是什麼
1. 一種實作在express框架上的套件，主要幫助開發者產生/管理對應的cookie和session
2. express-session 具體功能為：
- 以middleware來攔截每個請求來管理/產生session，並且要求客戶端儲存對應的session id當作其cookie的內容
- 等到客戶端持著夾帶合法session id的cookie來向伺服器發送請求，伺服器上該套件就會攔截並輸出對應的session內容至req.session來給後續middleware使用


#### 安裝/設定方式
express-session 套件安裝方式：
```
npm install express-session
```

套件載入至主程式(伺服器)的方式：由於該套件是以middleware為主，
```
// load express-session
// 其套件的回傳內容是本身是一個middleware function
const session = require('express-session')
app.use('/', seession( options ))

```

該middleware會攔截請求封包是否夾帶著session id的cookie並根據session id來輸出對應的session的資訊，設定為
```
// 替req增加屬性，如req.session
req.session = .....
```

透過給後續middleware得知
```
// load express-session
// 其套件的回傳內容是本身是一個middleware function
const session = require('express-session')
app.use('/', seession( options ))

// 給其他middleware得知
app.method(path, callback)
app.method(path, callback)
.
.
```

所以若要讓其他的middleware能夠使用其功能所提供的session 功能，必須先將套件以app.use來使用其midddleware function並放置在其他middleware之前，就能攔截所有對應請求來做處理，或者在正式做處理之前就能先處理，如上例子。

#### 當對req.session進行寫入時
[[在沒有任何session的情況下，只要當req.session下任一屬性被寫入，express-session就會為它建立對應的cookie和session]]

#### 客戶端如何傳遞帶有session id的cookie
[[客戶端每當發送請求時，會根據請求的Domain會是什麼而根據cookie上 Domain欄位來添加對應的cookie內容至請求封包]]


#### session(options)的options是？
1. Options 是藉由物件來設定Express-Session所提供的middleware

2. 該物件常用的屬性為：
- store: 定義session儲存在哪？選項有內建的MemoryStore、資料庫、redis
- secret：一組字串，用來簽署每個儲存session id的cookie以及用該字串來解開每個被簽署過後的cookie是否由該伺服器所建立的cookie

- name：字串，設定由模組建立的cookie 所擁有的名字。

- saveUninitialized：布林值，原本當客戶端與伺服器開始進行連線時，就會開始建立session物件來紀錄兩者在連線時的狀態，且剛建立的session物件的屬性未在伺服器中被任意值來寫入，此session就會被當作未初始化的session，而若saveUninitialized被設定為true時，就便會將未初始化的session儲存在伺服器的session store，而saveUninitialized被設定為false時，就便不會將未初始化的session儲存在伺服器session store。 true是會強制儲存未初始化的session至伺服器中的session store以及替客戶端建立儲存對應session id的cookie，false是不會強制儲存。

> When an empty session object is created and no properties are set, it is the uninitialized state. So, setting saveUninitialized to false will not save the session if it is not modified.

- resave：布林值，若設定為true，每一次客戶端和伺服器之間只要出現連線互動，所對應的session都會重新寫進至session store，即使從store取出來的session 沒有被伺服器修改，也會重新寫進store並更新過期時間；若為false，就直接關閉這項功能。
	[[session的resave功能是盡可能讓潛在可用的session繼續留在session store]]
> Forces the session to be saved back to the session store, even if the session was never modified during the request. Depending on your store this may be necessary, but it can also create race conditions where a client makes two parallel requests to your server and changes made to the session in one request may get overwritten when the other request ends, even if it made no changes (this behavior also depends on what store you're using).



## 複習
#🧠 Express-Session 是Express 框架的模組，用途是什麼？->->-> `主要幫助開發者產生/管理對應的cookie和session，具體是以middleware來攔截每個請求來管理/產生session，並且要求客戶端儲存對應的session id當作其cookie的內容、等到客戶端持著夾帶合法session id的cookie來向伺服器發送請求，伺服器上該套件就會攔截並輸出對應的session內容至req.session來給後續middleware使用`
<!--SR:!2023-12-25,94,188-->

#🧠  session(options)的options是 ->->-> `是藉由物件來設定Express-Session所提供的middleware`
<!--SR:!2023-09-23,290,248-->
#🧠 session(options)的options 所描述的store是 ->->-> `定義session儲存在哪？選項有內建的MemoryStore、資料庫、redis`
<!--SR:!2025-04-15,623,248-->

#🧠 session(options)的options 所描述的saveUninitialized是 ->->-> `原本當客戶端與伺服器開始進行連線時，就會開始建立session物件來紀錄兩者在連線時的狀態，且剛建立的session物件的屬性未在伺服器中被任意值來寫入，此session就會被當作未初始化的session，而若saveUninitialized被設定為true時，就便會將未初始化的session儲存在伺服器的session store，而saveUninitialized被設定為false時，就便不會將未初始化的session儲存在伺服器session store`
<!--SR:!2023-12-09,129,228-->

#🧠 session(options)的options 所描述的resave是 ->->-> `每一次客戶端和伺服器之間只要出現連線互動，所對應的session都會重新寫進至session store，即使從store取出來的session 沒有被伺服器修改，也會重新寫進store並更新過期時間；若為false，就直接關閉這項功能`
<!--SR:!2024-02-25,338,210-->

---
Status: #🌱 
Tags:
[[Express]] 
Links:
[[在沒有任何session的情況下，只要當req.session下任一屬性被寫入，express-session就會為它建立對應的cookie和session]]
[[Express-session 會替要傳給客戶端當cookie內容的session做簽署以防竄改]]
[[body-parser 是express內建套件且 用來解析請求封包下的message body並將解析結果放至req.body]]
References:
[[@express-sessionExpressjsSessionSimple]]
