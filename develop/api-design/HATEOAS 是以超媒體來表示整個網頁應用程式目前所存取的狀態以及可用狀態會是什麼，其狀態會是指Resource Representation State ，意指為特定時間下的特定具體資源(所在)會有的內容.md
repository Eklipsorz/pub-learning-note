
## 描述


#### REST 架構和非REST架構

1. 全名為Hypermedia As The Engine Of Application State，主要是用來區分REST 架構和非REST 架構的條件

> Hypermedia as the Engine of Application State (HATEOAS) is a constraint of the REST application architecture that distinguishes it from other network application architectures.


[[@linxinliangNiDeRESTBuShiREST]]
>  現今應用程式開發者認知中的REST，其實多是屬於Richardson成熟模型中的Level 2，使用多個URI、多個HTTP方法，並善用HTTP回應狀態碼來代表操作結果。而其中的URI用來代表資源，像是/messages、/messages/1等就是資源代表；HTTP方法則是動詞，也就是打算進行的動作，例如GET /messages取得全部訊息，GET /messages/1取得指定訊息，POST /messages新增訊息、DELETE /messages/1刪除指定訊息等。


> **HATEOAS與HAL**
> 按照Roy Fielding的觀點，沒有HATEOAS約束，就不是REST，然而，Leonard Richardson也說過，一開始就要討論HATEOAS的概念是困難的，因此他才從HTML與URI開始，開展了他對成熟模型的區分。

  
### HATEOAS 是什麼

1. HATEOAS如同其名，**以超媒體(Hypermedia)來表示整個網頁應用程式的目前所存取的狀態以及可用的狀態是什麼**：
	- 狀態會是指Resource Representation State ，意指為特定時間下的特定具體資源(所在)會有的內容
	- 目前的狀態會是指目前存取到的特定具體資源(所在)會有的內容，形式會是 **識別字：端點位置**
	- 可用的狀態會是根據目前狀態、使用者權限來決定哪些特定具體資源(所在)的內容可以被存取，形式會是 **識別字：端點位置**
	
2. 只要客戶端向應用伺服器中的某個資源X發出變更請求時，伺服器就會回傳一組超媒體以及對應資料，其超媒體(一組連結)會是根據使用者對於其資源相關聯的資源是否有權限而生成對應資源的API連結(超連結)或者對應資源的連結以及目前所在的狀態-目前所存取的具體資源(所在)
3. 超媒體是指可以在電子裝置/電腦呈現的圖片、文字等任何可以呈現資訊的形式

> With HATEOAS, a client interacts with a network application whose application servers provide information dynamically through hypermedia. A REST client needs little to no prior knowledge about how to interact with an application or server beyond a generic understanding of hypermedia.





簡單來說，當使用者透過初始API URI就能獲取接下來能夠做的操作以及資源的對應連結，接著使用者想要對其中一個資源操作下達對應的請求，就能讓伺服器再次回傳其資訊以及接下來還能夠做啥操作和資源的對應連結。


### 帶來的好處
在前後分離的架構，這可以帶來：

- 前端可以不必事先知道伺服器的特定資源所對應的端點是什麼而寫死API 端點，因為每個請求回應都會包含著接下來能夠執行的操作以及資源是什麼
- 當伺服器更動API時，前端也不需要跟著改動，只需要等待伺服器回傳對應較新的API 端點


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

#🧠 HATEOAS 全名是什麼？ ->->-> `Hypermedia As The Engine of Application State`
<!--SR:!2025-02-16,527,250-->

#🧠 HATEOAS 功能是什麼？->->-> `**以超媒體(Hypermedia)來表示整個網頁應用程式的目前所存取的狀態以及可用的狀態是什麼**`
<!--SR:!2024-09-06,419,250-->

#🧠 HATEOAS 功能是**以超媒體(Hypermedia)來表示整個網頁應用程式的目前所存取的狀態以及可用的狀態是什麼** ，其中狀態在REST會是指什麼？->->-> `狀態會是指Resource Representation State ，意指為特定時間下的特定具體資源(所在)會有的內容`
<!--SR:!2023-12-21,104,230-->

#🧠 HATEOAS 功能是**以超媒體(Hypermedia)來表示整個網頁應用程式的目前所存取的狀態以及可用的狀態是什麼** ，其中目前所存取的狀態會是什麼？ ->->-> `目前的狀態會是指目前存取到的特定具體資源(所在)會有的內容；`
<!--SR:!2024-11-29,472,250-->

#🧠 HATEOAS 功能是**以超媒體(Hypermedia)來表示整個網頁應用程式的目前所存取的狀態以及可用的狀態是什麼** ，其中可用的狀態是什麼？ ->->-> `可用的狀態會是根據目前狀態、使用者權限來決定哪些特定具體資源(所在)的內容可以被存取`
<!--SR:!2024-10-18,443,250-->


#🧠 HATEOAS 功能是**以超媒體(Hypermedia)來表示整個網頁應用程式的目前所存取的狀態以及可用的狀態是什麼**，請以客戶端和伺服器來說明 ->->-> `只要客戶端向應用伺服器中的某個資源X發出變更請求時，伺服器就會回傳一組超媒體以及對應資料，其超媒體(一組連結)會是根據使用者對於其資源相關聯的資源是否有權限而生成對應資源的API連結(超連結)或者對應資源的連結以及目前所在的狀態-目前所存取的具體資源(所在)`
<!--SR:!2025-02-17,528,250-->

#🧠 HATEOAS中的hypermedia是指什麼？ ->->-> `超媒體是指可以在電子裝置/電腦呈現的圖片、文字等任何可以呈現資訊的形式`
<!--SR:!2024-03-22,316,250-->

#🧠 HATEOAS帶來的好處是什麼？ ->->-> `- 前端可以不必事先知道伺服器的特定資源所對應的端點是什麼而寫死API 端點，因為每個請求回應都會包含著接下來能夠執行的操作以及資源是什麼 - 當伺服器更動API時，前端也不需要跟著改動，只需要等待伺服器回傳對應較新的API 端點 `
<!--SR:!2023-12-16,99,230-->


#🧠 伺服器和客戶端都支援著HATEOAS，那麼只要客戶端向伺服器發出查詢12345這銀行帳戶的資料，且客戶端的銀行帳戶是有錢的，上圖為客戶端向伺服器發送的請求端點和方法，下圖為結果，請試著說明 ![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1665905332/blog/REST/HATEOAS-example1_ad6vh3.png)![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1665905332/blog/REST/HATEOAS-example1-with-money_yp1z7n.png)->->-> `伺服器和客戶端都支援著HATEOAS，那麼只要客戶端向伺服器發出查詢12345這帳戶的資料，就會呈現該帳號的資料以及一組連結、包含目前所在的狀態資訊-self資訊，連結會是伺服器根據客戶端對於其帳號相關聯的資源是否有權限而動態生成對應的連結，self資訊是用來告知彼此目前狀態或者目前處理的請求是什麼，在這是允許12345帳號是擁有存款(deposits)、提款(withdrawals)、轉帳(transfers)、關閉請求(close-requests)的請求，所以會生成四個連結，而self則是指的是/accounts/12345`
<!--SR:!2024-12-01,474,250-->


#🧠 伺服器和客戶端都支援著HATEOAS，那麼只要客戶端向伺服器發出查詢12345這銀行帳戶的資料，且客戶端的銀行帳戶是沒錢的，上圖為客戶端向伺服器發送的請求端點和方法，下圖為結果，請試著說明 ![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1665905332/blog/REST/HATEOAS-example1_ad6vh3.png)![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1665905332/blog/REST/HATEOAS-example1-without-money_sfjdmc.png)->->-> `假使12345帳戶沒錢的話的話，伺服器給定的連結會只剩下存款和關閉請求`
<!--SR:!2023-12-17,100,230-->

#🧠 伺服器和客戶端都支援著HATEOAS，那麼伺服器回應的目前狀態形式會是如何？ ->->-> `識別字：端點位置`
<!--SR:!2024-11-30,473,250-->


#🧠 伺服器和客戶端都支援著HATEOAS，那麼伺服器回應的可用狀態形式會是如何？ ->->-> `識別字：端點位置`
<!--SR:!2024-08-31,416,250-->



---
Status: #🌱 
Tags:
[[Representational State Transfer]]
Links:
[[hypertext 是電腦或電子裝置能夠呈現的文字，hypermedia 是電子或電子裝置能夠呈現的任一可以表達資訊的事物，hyperlink 是以將特定頁面的網址綁定在hypertext或者hypermedia作為轉移時的連結]]
[[medium 為傳遞或表達特定事物的任一方法或形式，比如表達資訊的圖片、報紙、影片，其中media為單數，medium為複數]]
[[REST是一種 以資源為中心，用HTTP方法操作資源，並且最終目標為打造出滿足於HATEOAS之產品的網路軟體開發風格]]
References:
[[@QianTanRESTAPI]]
[[@linxinliangNiDeRESTBuShiREST]]
[[@flydeanJiaGouZhiRESTHeHATEOASZhiHu]]