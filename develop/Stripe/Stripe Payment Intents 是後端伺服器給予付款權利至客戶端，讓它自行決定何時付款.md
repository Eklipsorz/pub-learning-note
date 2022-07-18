## 描述
stripe intents 細節1： [[@AcceptPayment]]
> **Server-side** 
> On your server, make an endpoint that creates a PaymentIntent with an amount and currency. Always decide how much to charge on the server side, a trusted environment, as opposed to the client. This prevents malicious customers from being able to choose their own prices.

stripe intents 細節2：[[@AcceptPayment]]
> When the customer taps **Pay**, confirm the PaymentIntent to complete the payment.
> 
> Rather than sending the entire PaymentIntent object to the client, use its client secret. This is different from your API keys that authenticate Stripe API requests. The client secret should be handled carefully because it can complete the charge. Don’t log it, embed it in URLs, or expose it to anyone but the customer.

重點：
- 細節1：由於總是從伺服器端來決定結帳金額，所以避免了客戶端被惡意竄改金額的風險
- 細節2：從伺服器獲得的client_secret可以代替那名使用者
- 細節3：基於[[金流服務 - 輸入信用卡資料和確認付款這兩項動作是可以分開]]，所以當客戶端獲取付款權利的client_secret時，不一定代表著就已經填入信用卡。

### 流程

#### 付款資料的填寫和建立
1. 客戶端會透過Payment Element 來擷取使用者所輸入的付款資料，接著再從客戶端呼叫，其Data為付款資料，透過此呼叫，來讓客戶端向stripe發送建立付款方式物件的請求
```
stripe.createPaymentMethod(Data)
```
2. stripe伺服器收到請求就驗證付款資料和key
	- 若不正確，Stripe伺服器就會透過Payment Element來告知使用者和客戶端資料是不正確的
3. 若正確的話，stripe伺服器會建立對應PaymentMethod物件並紀錄，同時回傳對應物件至客戶端，由客戶端自行透過這物件來表示自己要用哪個資訊來當付款的基礎
![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1656946266/blog/paymentFlow/stripe/pre-build-billing-data_wxzoqm.png)

#### 客戶端索要client_secret

1. 客戶端會透過GET /secret 向後端伺服器索要對應的stripe client_secret
```
const paymentIntent = await stripe.paymentIntents.create({
  amount: 1099,
  currency: 'usd',
});
const clientSecret = paymentIntent.client_secret
```
2. 後端伺服器收到GET /secret請求，便呼叫以下函式來向Stripe伺服器索要client_secret，同時Stripe伺服器會產生對應secret並紀錄
```
stripe.paymentIntents.create(....)
```
3. Stripe伺服器做完產生和紀錄後，就把client_secret回傳到伺服器，伺服器在回傳給客戶端
4. 接著客戶端呼叫以下方法，其中會附加client_secret、預先建立的付款資料方法物件(定義如何付款和付款資訊)，這呼叫就等同客戶端向Stripe 伺服器發送確定付款的請求，並要求驗證附加的client_secret、預先建立的付款資料方法物件、key
```
stripe.confirmPayment(client_secret,paymentMethod)
```
5.  Stripe 伺服器收到後就驗證key、client_secret是否正確：
		- 若不正確的話，就告知客戶端是錯誤的
6 若正確的話，伺服器就會告知成功付款

![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1656946813/blog/paymentFlow/stripe/payment_intents_flow_j2nigv.png)

另外請注意
細節3：基於[[金流服務 - 輸入信用卡資料和確認付款這兩項動作是可以分開]]，所以當客戶端獲取付款權利的client_secret時，不一定代表著就已經填入信用卡。

所以流程會是：
- 使用者先填入信用卡資料，接著在取得client_secret，最後在呼叫confirmPayment來確認付款 
- 先取得client_secret，接著再填入信用卡資料，最後在呼叫confirmPayment
- 只要能讓最後的confirmPayment能拿到付款資訊和secret，前兩者順序皆可調換



### 特點
1. 結帳決定權容易全都在客戶端
2. 由於能夠決定付款的secret放在前端，所以安全性較低

## 複習
#🧠 Stripe Payment Intents 是什麼樣服務->->-> `後端伺服器給予付款權利至客戶端，讓它自行決定何時付款 `
<!--SR:!2022-08-06,22,250-->

#🧠  Stripe Payment Intents 以下為付款資料的填寫和建立的流程，請說明流程 ![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1656946266/blog/paymentFlow/stripe/pre-build-billing-data_wxzoqm.png)->->-> `1. 客戶端會透過Payment Element 來擷取使用者所輸入的付款資料，接著再從客戶端呼叫，其Data為付款資料，透過此呼叫，來讓客戶端向stripe發送建立付款方式物件的請求2. stripe伺服器收到請求就驗證付款資料和key - 若不正確，Stripe伺服器就會透過Payment Element來告知使用者和客戶端資料是不正確的 3. 若正確的話，stripe伺服器會建立對應PaymentMethod物件並紀錄，同時回傳對應物件至客戶端，由客戶端自行透過這物件來表示自己要用哪個資訊來當付款的基礎`
<!--SR:!2022-07-18,10,250-->


#🧠 Stripe Payment Intents 以下為客戶端索要client_secret並確認付款的流程，請說明流程 ![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1656946813/blog/paymentFlow/stripe/payment_intents_flow_j2nigv.png)->->-> `1. 客戶端會透過GET /secret 向後端伺服器索要對應的stripe client_secret 2. 後端伺服器收到GET /secret請求，便呼叫以下函式來向Stripe伺服器索要client_secret，同時Stripe伺服器會產生對應secret並紀錄 3. Stripe伺服器做完產生和紀錄後，就把client_secret回傳到伺服器，伺服器在回傳給客戶端 4. 接著客戶端呼叫以下方法，其中會附加client_secret、預先建立的付款資料方法物件(定義如何付款和付款資訊)，這呼叫就等同客戶端向Stripe 伺服器發送確定付款的請求，並要求驗證附加的client_secret、預先建立的付款資料方法物件、key 5.  Stripe 伺服器收到後就驗證key、client_secret是否正確： - 若不正確的話，就告知客戶端是錯誤的 6 若正確的話，伺服器就會告知成功付款`
<!--SR:!2022-07-18,10,250-->


#🧠  Stripe Payment Intents 流程會是？(以輸入信用卡、client_secret、確定付款為例)->->-> `- 使用者先填入信用卡資料，接著在取得client_secret，最後在呼叫confirmPayment來確認付款 -先取得client_secret，接著再填入信用卡資料，最後在呼叫confirmPayment，只要能讓最後的confirmPayment能拿到付款資訊和secret，前兩者順序皆可調換`
<!--SR:!2022-08-15,28,250-->


#🧠 Stripe Payment Intents  特點是什麼？ ->->-> `1. 結帳決定權容易全都在客戶端 2. 由於能夠決定付款的secret放在前端，所以安全性較低`
<!--SR:!2022-08-05,21,250-->

---
Status: #🌱 
Tags:
[[Payment]]
Links:
[[Stripe Payment Element 是Stripe 提供於UI開發的元件來從而擷取使用者透過該元件的輸入結果並產出伺服器容易處理的結果，其元件具體會是由部分DOM節點和事件綁定來構成]]
[[金流服務 - 輸入信用卡資料和確認付款這兩項動作是可以分開]]
References:
[[@AcceptPayment]]