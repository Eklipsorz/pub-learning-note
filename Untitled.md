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


### 流程

![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1656883162/blog/paymentFlow/stripe/payment_intents_flow_q8vet6.png)

## 複習
#🧠 Question :: ->->-> ``

---
Status: 
Tags:
Links:
References:
