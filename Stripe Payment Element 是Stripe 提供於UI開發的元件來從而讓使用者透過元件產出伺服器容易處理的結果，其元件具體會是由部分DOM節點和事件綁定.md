



## 描述
[[@StripePaymentElement]] 所描述：
> The Payment Element is an embeddable UI component that lets you accept up to 18+ payment methods with a single integration. Whether you’re just collecting card payments or dozens of payment methods, the Payment Element is the easiest way to build an embedded and customized payments experience. If you have a mobile app as well, use our equivalent integrations for iOS, Android, and React Native.

[[@stripeStripeJSReference]] 所描述：
> The [Payment Element](https://stripe.com/docs/payments/payment-element) is an embeddable component for securely collecting payment details. The Payment Element supports dozens of payment methods with a single integration.

重點：
- Stripe Payment Element 是Stripe 提供於UI開發的元件來從而讓使用者透過元件產出伺服器容易處理的結果，其元件具體會是由部分DOM節點和事件綁定來構成
- Payment Element 是Stripe 官方提供的UI元件，其元件會由部分DOM節點和事件綁定來構成，具體元件種類會根據付款種類而區分，比如信用卡就用信用卡UI元件
- 需要的API token：stripe public key
- Payment Element 用途：
	- 從使用者對於元件的互動中收集付款資料
	- 將付款資料轉換為對於Strip伺服器方便處理的資料，必要的話，會先透過客戶端這邊的stripe public key 來向stripe 伺服器產出識別資料，然後再由其元件先將轉換資料給開發者後端伺服器處理，處理完再由識別資料，從後端伺服器來識別出該資料是源自於哪裡


---
Status: #🌱 
Tags:
[[Stripe]]
Links:
References:
[[@StripePaymentElement]]
[[@stripeStripeJSReference]]