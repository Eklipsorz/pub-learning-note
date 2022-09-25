
## 描述
[[@StripePaymentElement]] 所描述：
> The Payment Element is an embeddable UI component that lets you accept up to 18+ payment methods with a single integration. Whether you’re just collecting card payments or dozens of payment methods, the Payment Element is the easiest way to build an embedded and customized payments experience. If you have a mobile app as well, use our equivalent integrations for iOS, Android, and React Native.

[[@stripeStripeJSReference]] 所描述：
> The [Payment Element](https://stripe.com/docs/payments/payment-element) is an embeddable component for securely collecting payment details. The Payment Element supports dozens of payment methods with a single integration.

重點：
- Stripe Payment Element 是Stripe 提供於UI開發的元件來從而擷取使用者透過該元件的輸入結果並產出伺服器容易處理的結果，其元件具體會是由部分DOM節點和事件綁定來構成
- Payment Element 是Stripe 官方提供的UI元件，本身會以SDK或者API形式來提供給開發者，其元件會由部分DOM節點和事件綁定來構成，具體元件種類會根據付款種類而區分，比如信用卡就用信用卡UI元件
- 需要的API token：stripe public key
- Payment Element 用途：
	- 擷取使用者所輸入的付款資料
	- 將付款資料傳遞至對應的stripe server來驗證是否合法

## 複習

#🧠 Stripe Payment Element是什麼元件？ ->->-> `Stripe Payment Element 是Stripe 提供於UI開發的元件來從而擷取使用者透過該元件的輸入結果並產出伺服器容易處理的結果，其元件具體會是由部分DOM節點和事件綁定來構成`
<!--SR:!2022-10-19,69,250-->

#🧠  Stripe Payment Element 是由什麼構成的？種類會根據什麼來區分(提示付款？) ->->-> `其元件會由部分DOM節點和事件綁定來構成，具體元件種類會根據付款種類而區分，比如信用卡就用信用卡UI元件`
<!--SR:!2022-10-24,29,230-->

#🧠 要使用Stripe 所提供的Payment Element 元件，需要什麼樣的密鑰->->-> `stripe public key`
<!--SR:!2022-10-16,65,250-->

#🧠 Stripe 所提供的Payment Element 元件之用途是什麼？ ->->-> `- 擷取使用者所輸入的付款資料 - 將付款資料傳遞至對應的stripe server來驗證是否合法`
<!--SR:!2022-12-08,74,250-->



---
Status: #🌱 
Tags:
[[Stripe]]
Links:
References:
[[@StripePaymentElement]]
[[@stripeStripeJSReference]]