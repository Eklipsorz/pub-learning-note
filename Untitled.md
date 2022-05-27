## Express-Session

1. 一種第三方套件，非官方套件，主要幫助開發者產生/管理對應的cookie和session

2. 可以幫開發者從伺服器中擷取cookie資訊、並從中替客戶端建立儲存對應id的cookie和對應的session在伺服器內部的套件。

3. 具體來說，當載入該模組時，客戶端和伺服器端只要處於request/response cycle的話，就會建立session來紀錄兩者的連線過程，同時間會賦予session id 給該session並讓客戶端建立cookie去儲存session id，而到時cookie只要拿著這session id發送請求至伺服器，伺服器收到便拿該id獲取對應先前的連線過程是什麼。

4. 安裝方式：

```
npm install express-session
```

5. 載入以及設定方式：其套件的回傳內容是本身是一個middleware function，所以若要讓其他的middleware能夠使用其功能所提供的session 功能，必須先將套件以app.use來使用其midddleware function並放置在其他middleware之前，如下例子：首先先載入express-session回傳的middleware function至session變數，然後用options物件去設定該middleware function，然後後面的app.method或者其他middleware function就能因為use的特性而使用express-session功能。

```

// load express-session

const session = require('express-session')

app.use('/', seession( options ))


// other routes (other middleware functions)

app.method(path, callback)

app.method(path, callback)

.

.

```

  

5. 延續上個例子，當某個請求是可以對應某一個route時，在伺服器以那個route之前來處理請求，會先經過app.use所載入的session middleware來對req生成對應的屬性來代表著session和cookie的內容

  

```

app.use('/', seession( options ))

  

// other routes (other middleware functions)

app.method(path, callback)

app.method(path, callback)

.

.

```