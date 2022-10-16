
## 描述


#### REST 架構和非REST架構

1. 全名為Hypermedia As The Engine Of Application State，主要是用來區分REST 架構和非REST 架構的條件

> Hypermedia as the Engine of Application State (HATEOAS) is a constraint of the REST application architecture that distinguishes it from other network application architectures.

  
### HATEOAS 是什麼

1. HATEOAS如同其名，**以超媒體(Hypermedia)來表示整個網頁應用程式來表示目前的狀態以及可用的狀態是什麼**
2. 只要客戶端向應用伺服器中的某個資源X發出變更請求時，伺服器就會回傳一組超媒體以及對應資料，其超媒體(一組連結)會是根據使用者對於其資源相關聯的資源是否有權限而生成對應資源的API連結(超連結)或者對應資源的連結，兩者皆含有目前狀態所在的URI位址
3. 超媒體可以圖片、文字等任何可以呈現資訊的形式

> With HATEOAS, a client interacts with a network application whose application servers provide information dynamically through hypermedia. A REST client needs little to no prior knowledge about how to interact with an application or server beyond a generic understanding of hypermedia.



簡單來說，當使用者透過初始API URI就能獲取接下來能夠做的操作以及資源的對應連結，接著使用者想要對其中一個資源操作下達對應的請求，就能讓伺服器再次回傳其資訊以及接下來還能夠做啥操作和資源的對應連結。

這可以帶來：

- 在前後分離的架構，前端可以不必事先知道伺服器的處理邏輯以及對應的API是什麼而寫死API URI，因為每個請求回應都會包含著接下來能夠執行的操作以及資源是什麼，而且當伺服器更動API時，前端也不需要跟著改動，只需要等待伺服器回傳對應較新的API URI

- 伺服器能在客戶端不中斷的情況下根據與客戶端的API互動而進行對應能操作的資源之URI

  
#### 案例
伺服器和客戶端都支援著HATEOAS，那麼只要客戶端向伺服器發出查詢12345這帳戶的資料

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
		},
	
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




## 複習


---
Status: #🌱 
Tags:
Links:
[[hypertext 是電腦或電子裝置能夠呈現的文字，hypermedia 是電子或電子裝置能夠呈現的任一可以表達資訊的事物，hyperlink 是以將特定頁面的網址綁定在hypertext或者hypermedia作為轉移時的連結]]
[[medium 為傳遞或表達特定事物的任一方法或形式，比如表達資訊的圖片、報紙、影片，其中media為單數，medium為複數]]
References:
[[@QianTanRESTAPI]]
[[@flydeanJiaGouZhiRESTHeHATEOASZhiHu]]