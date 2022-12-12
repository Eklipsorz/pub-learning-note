## 描述




### 流程
1. 使用者按下確定付款，並讓客戶端透過Payment Element擷取使用者所輸入的付款資料和Key來向Stripe 伺服器索要token，具體是客戶端呼叫以下方法
```
// cardElement： 用以擷取使用者輸入卡號的元件
stripe.createToken(cardElement)
```
2. Stripe 伺服器收到後就檢驗付款資料和Key
	- 若檢驗失敗的話，Stripe伺服器就回傳失敗訊息

3. 若檢驗成功的話，Stripe 伺服器會建立對應token並紀錄下來，最後由它回傳token至客戶端
4. 客戶端收到token之後，就會向伺服器發送POST /purchase請求並夾帶著token以及結帳總金額
5. 伺服器接收到該請求，就使用自己的key、客戶端傳過來的token以及結帳總金額向Stripe伺服器發送結帳請求，具體會是呼叫以下方法
```
stripe.charges.create({
	token:....,
	amount:....
})
```
6. Stripe 伺服器接收到結帳請求時，會檢測token、key是否正確
	- 若檢驗失敗的話，Stripe 伺服器會回傳失敗訊息至伺服器，接著伺服器接收到失敗訊息也跟著轉遞給客戶端
7. 若檢驗成功的話，Stripe伺服器會回傳結帳成功訊息至伺服器，接著伺服器就會更新庫存，然後傳遞成功訊息至客戶端
8. 客戶端收到成功訊息

![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1656922313/blog/paymentFlow/stripe/token_and_charge_flow_esf3go.png)
### 特點
1. 結帳決定權容易落在伺服器來決定
2. 由於結帳部分是由伺服器來決定，所以安全性會比intents來得高

### token 

> Tokenization is the process Stripe uses to collect sensitive card or bank account details, or personally identifiable information (PII), directly from your customers in a secure manner. A token representing this information is returned to your server to use.

重點：
- Tokenization 是 Stripe 官方用來將付款資料(信用卡資料細節或者銀行帳號細節等)轉換成一段字串，接著Stripe 會事先儲存該字串，以便未來來識別該字串是代表著對應付款資料
- 該字串會代表著對應付款資料


## 複習
#🧠 Tokenization 是什麼樣的技術？ (從敏感至不敏感？如何識別)->->-> `具體將敏感資料轉換成另一種較不敏感的字串，接著為了以後識別該字串，會在伺服器端紀錄token是對應哪個付款資料，當客戶端傳遞請求時夾帶該字串，就能藉由事先紀錄來識別`
<!--SR:!2023-04-22,180,250-->

#🧠 Stripe token+charges 結帳方法的特點？->->-> `1. 結帳決定權容易落在伺服器來決定 2. 由於結帳部分是由伺服器來決定，所以安全性會比intents來得高`
<!--SR:!2023-08-19,250,250-->

#🧠 Stripe token+charges整體流程 是什麼？以這圖來說明![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1656922313/blog/paymentFlow/stripe/token_and_charge_flow_esf3go.png)->->-> `1. 使用者按下確定付款，並讓客戶端透過Payment Element擷取使用者所輸入的付款資料和Key來向Stripe 伺服器索要token，2. Stripe 伺服器收到後就檢驗付款資料和Key - 若檢驗失敗的話，Stripe伺服器就回傳失敗訊息 3. 若檢驗成功的話，Stripe 伺服器會建立對應token並紀錄下來，最後由它回傳token至客戶端 4. 客戶端收到token之後，就會向伺服器發送POST /purchase請求並夾帶著token以及結帳總金額 5. 伺服器接收到該請求，就使用自己的key、客戶端傳過來的token以及結帳總金額向Stripe伺服器發送結帳請求 6. Stripe 伺服器接收到結帳請求時，會檢測token、key是否正確 - 若檢驗失敗的話，Stripe 伺服器會回傳失敗訊息至伺服器，接著伺服器接收到失敗訊息也跟著轉遞給客戶端 7. 若檢驗成功的話，Stripe伺服器會回傳結帳成功訊息至伺服器，接著伺服器就會更新庫存，然後傳遞成功訊息至客戶端 8. 客戶端收到成功訊息`
<!--SR:!2022-12-25,106,250-->

---
Status: #🌱 
Tags:
[[Stripe]]
Links:
[[Stripe Payment Element 是Stripe 提供於UI開發的元件來從而擷取使用者透過該元件的輸入結果並產出伺服器容易處理的結果，其元件具體會是由部分DOM節點和事件綁定來構成]]
References:
[[@stripeStripeJSReference]]