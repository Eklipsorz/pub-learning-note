
## 描述
> [Checkout](https://stripe.com/payments/checkout) is a low-code payment integration that creates a customizable payment page so you can quickly collect payments on desktop and mobile devices. Checkout supports one-time payments and subscriptions for your global customer base with coverage across over twenty local payment methods

> A Checkout Session represents your customer's session as they pay for one-time purchases or subscriptions through Checkout or Payment Links. We recommend creating a new Session each time your customer attempts to pay.
> 
> Once payment is successful, the Checkout Session will contain a reference to the Customer, and either the successful PaymentIntent or an active Subscription. You can create a Checkout Session on your server and pass its ID to the client to begin Checkout.


重點：
- stripe API有提供官方結帳網頁和結帳功能的API，其API會是如下，主要會建立對應結帳的session以及(附加結帳功能的)結帳網頁
```
stripe.checkout.sessions.create(....)
```
- 每一次呼叫都會建立新的對應session、新的結帳網頁
### stripe.checkout.sessions.create 參數

 基本上create本身指定的參數是一個option物件，其物件屬性會有：
 	- line_items：列出購買者正購買的物品清單(包含價錢、名稱、幣種、數量)
	> A list of items the customer is purchasing.
	- mode：指定付款方式
	> The mode of the Checkout Session.
	- success_url：指定一個購買成功的網頁，如果購買者成功完成購買，會被導向到那
	> The URL to which Stripe should send customers when payment or setup is complete.
	- cancel_url：指定一個取消購買的網頁，如果購買者決定要取消購買時，會被導向到那
	> The URL the customer will be directed to if they decide to cancel payment and return to your website.
```js
const session = await stripe.checkout.sessions.create({
		line_items: [
			{
				price_data: {
					currency: 'usd',
					product_data: {
						name: 'T-shirt',
					},
					unit_amount: 2000,
				},
				quantity: 1,
			},
		],
		mode: 'payment',
		success_url: 'https://example.com/success',
		cancel_url: 'https://example.com/cancel',
});
```


### line_items 列出購買者正購買的物品清單
```
line_items: [
		{
			price_data: {
				currency: 'usd',
				product_data: {
					name: 'T-shirt',
				},
				unit_amount: 2000,
			},
			quantity: 1,
		},
],

```
重點：
- line_items 是一組陣列，陣列是存放物件，每個物件代表每一種購買者所想要買的產品資訊(包含價格、幣值、名稱、數量)
- 每一個想購買的產品資訊可以用price_data來定義該產品的價格設定
	- currency 幣種
	- product_data 以物件的屬性來呈現產品簡介
	- unit_account：以非負數值的百分比來表示對應產品的單項價錢，換言之，一個產品A多少錢，且是以百分比來表示
	> A non-negative integer in cents representing how much to charge
	- quantity 數量：購買者購買的量
### mode 指定付款方式
> `payment` Accept one-time payments for cards, iDEAL, and more.
> `setup` Save payment details to charge your customers later.
> `subscription` Use Stripe Billing to set up fixed-price subscriptions.

重點：
- payment ，指定接收一次性信用卡付款
- setep，可以允許購買者晚點付款並儲存目前付款資訊，以待下次使用
- subscription，使用訂閱制



### checkout session 和 網頁 時限
[[@AcceptPayment]]所描述
> Checkout Sessions expire 24 hours after creation.


1. 每一個checkout session在建立後的24個小時後會被釋放
2. 每當購買成功時，對應的checkout session和相關網頁也會被釋放


note:
1. 購買取消並不會釋放，還可以透過同樣的購買網址來購買


## 複習
#🧠 Question :: ->->-> ``
<!--SR:!2022-07-05,3,250-->

---
Status: #🌱 
Tags:
[[Stripe]]
Links:
References:
[[@AcceptPayment]]