
  

## REST 等級模型

1. 目的在於：以REST約束來評估一個Web服務設計的好壞並做個分級

2. 等級模型起草於Leonard Richardson在2008年 QCon Talk中，並於2010年由Martin Fowler進一步詮釋模型，並使該模型更加完整

3. 等級大致上分為：

- Level 0：將整個Web服務規劃成一個URI，並只用一個HTTP動詞來進行客戶端和伺服器之間的互動方式，通常HTTP動詞會是POST

- Level 1：將整個Web服務依據資源來分成多個URI，但只用一個HTTP動詞來進行客戶端和伺服器之間的互動方式

- Level 2：將整個Web服務依據資源來分成多個URI，並分成多個HTTP動詞來進行客戶端和伺服器之間的互動方式

- Level 3：基於Level2的概念下使用HATEOAS概念。

![](https://devopedia.org/images/article/252/1821.1579540894.jpg)

參考資料：

[你的REST不是REST？](https://www.ithome.com.tw/voice/128528)

[Richardson Maturity Model](https://devopedia.org/richardson-maturity-model)

## HATEOAS

1. 全名為Hypermedia As The Engine Of Application State，主要是用來區分REST 架構和非REST 架構的條件

> Hypermedia as the Engine of Application State (HATEOAS) is a constraint of the REST application architecture that distinguishes it from other network application architectures.

  

2. HATEOAS如同其名，**以超媒體(Hypermedia)來表示整個網頁應用程式來表示目前的狀態以及可用的狀態是什麼**，只要客戶端一向應用伺服器向某個資源X發出變更請求時，伺服器就會回傳一組超媒體以及對應資料，其超媒體(一組連結)會是根據使用者對於其資源相關聯的資源是否有權限而生成對應資源的API連結(超連結)或者對應資源的連結，兩者皆含有目前狀態所在的URI位址

> With HATEOAS, a client interacts with a network application whose application servers provide information dynamically through hypermedia. A REST client needs little to no prior knowledge about how to interact with an application or server beyond a generic understanding of hypermedia.

簡單來說，當使用者透過初始API URI就能獲取接下來能夠做的操作以及資源的對應連結，接著使用者想要對其中一個資源操作下達對應的請求，就能讓伺服器再次回傳其資訊以及接下來還能夠做啥操作和資源的對應連結。

這可以帶來：

- 在前後分離的架構，前端可以不必事先知道伺服器的處理邏輯以及對應的API是什麼而寫死API URI，因為每個請求回應都會包含著接下來能夠執行的操作以及資源是什麼，而且當伺服器更動API時，前端也不需要跟著改動，只需要等待伺服器回傳對應較新的API URI

- 伺服器能在客戶端不中斷的情況下根據與客戶端的API互動而進行對應能操作的資源之URI

  

3. 案例：伺服器和客戶端都支援著HATEOAS，那麼只要客戶端向伺服器發出查詢12345這帳戶的資料

  

```

GET /accounts/12345 HTTP/1.1

Host: bank.example.com

```

就會呈現該帳號的資料以及一組連結、包含目前所在的狀態資訊-self資訊，連結會是伺服器根據客戶端對於其帳號相關聯的資源是否有權限而動態生成對應的連結，self資訊是用來告知彼此目前狀態或者目前處理的請求是什麼，在這是允許12345帳號是擁有存款(deposits)、提款(withdrawals)、轉帳(transfers)、關閉請求(close-requests)的請求，所以會生成四個連結，而self則是指的是/accounts/12345

  

```

HTTP/1.1 200 OK

  

{

"account": {

"account_number": 12345,

"balance": {

"currency": "usd",

"value": 100.00

},

"self": {

"href": "/accounts/12345 HTTP/1.1"

}

"links": {

"deposits": "/accounts/12345/deposits",

"withdrawals": "/accounts/12345/withdrawals",

"transfers": "/accounts/12345/transfers",

"close-requests": "/accounts/12345/close-requests"

}

}

}

```

  

假使12345帳戶沒錢的話的話，伺服器給定的連結會只剩下存款和關閉請求

```

"links": {

"deposits": "/accounts/12345/deposits",

"close-requests": "/accounts/12345/close-requests"

}

```

  

4. 參考資料

[架构之:REST和HATEOAS](https://zhuanlan.zhihu.com/p/393221998)

[淺談 REST API 的設計和規劃](https://marco79423.net/articles/淺談-rest-api-的設計和規劃)
