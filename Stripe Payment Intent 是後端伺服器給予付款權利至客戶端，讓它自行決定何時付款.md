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
1. 客戶端憑著Key來使用Payment Element來擷取使用者所輸入的付款資料，然後當使用者按下確認付款時，就會向Stripe伺服器發送付款資料和Key來驗證付款資料和key是否正確：
	- 若不正確的話，Stripe伺服器就會透過Payment Element來告知使用者和客戶端資料是不正確的
2. 若都正確的話，客戶端會透過GET /secret 向後端伺服器索要對應的stripe client_secret
```
const paymentIntent = await stripe.paymentIntents.create({
  amount: 1099,
  currency: 'usd',
});
const clientSecret = paymentIntent.client_secret
```
3. 後端伺服器收到GET /secret請求，便呼叫以下函式來向Stripe伺服器索要client_secret，同時Stripe伺服器會產生對應secret並紀錄
```
stripe.paymentIntents.create(....)
```
4. Stripe伺服器做完產生和紀錄後，就把client_secret回傳到伺服器，伺服器在回傳給客戶端
5. 接著客戶端呼叫以下方法，客戶端就等同向Stripe 伺服器發送確定付款的請求，並要求驗證附加的client_secret和key
```
stripe.confirmPayment(client_secret,...)
```
6.  Stripe 伺服器收到後就驗證key、client_secret是否正確：
		- 若不正確的話，就告知客戶端是錯誤的
7. 若正確的話，伺服器就會告知成功付款

![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1656884961/blog/paymentFlow/stripe/payment_intents_flow_e4anpn.png)


另外請注意
細節3：基於[[金流服務 - 輸入信用卡資料和確認付款這兩項動作是可以分開]]，所以當客戶端獲取付款權利的client_secret時，不一定代表著就已經填入信用卡。

所以流程可能會是：
- 客戶端先獲取client_secret，隨後在填入信用卡資料，最後再呼叫confirmPayment
- 使用者先填入信用卡資料，接著在取得client_secret，最後再呼叫confirmPayment


### 特點
1. 付款決定權全都在客戶端
2. 由於能夠決定付款的secret放在前端，所以安全性較低

## 複習
#🧠 Question :: ->->-> ``

---
Status: 
Tags:
Links:
References:
