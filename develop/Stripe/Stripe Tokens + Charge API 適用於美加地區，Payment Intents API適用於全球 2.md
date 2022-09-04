
## 描述
[[@stripeStripeJSReference]] 所描述：
> The Charges API is the fastest way to accept U.S. and Canadian payments for your startup or prototype. Stripe.js provides the following methods to create Tokens and Sources, which are part of the Charges API.
> 
> To accept payments globally, use the Payment Intents API instead.

重點：
- Tokens + Charge 是Stripe對於美加地區所提供的最快付款方式，但僅限於美加地區使用
- Payment Intents API 適用於全球地區付款使用


### Charge 物件
> Charges
> To charge a credit or a debit card, you create a Charge object. You can retrieve and refund individual charges as well as list all charges. Charges are identified by a unique, random ID.

重點：
- 若要付款，必須建立對應儲存付款資訊的Charge 物件，才能夠成功付款

---
Status: #🌱 
Tags:
[[Payment]] - [[Stripe]]
Links:
References:
[[@stripeStripeJSReference]]