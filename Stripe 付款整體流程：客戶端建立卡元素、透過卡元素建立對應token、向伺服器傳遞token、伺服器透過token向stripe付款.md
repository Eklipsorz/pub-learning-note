## 描述




### 流程
1. 使用者按下確定付款，並讓客戶端透過Payment Element擷取使用者所輸入的付款資料和Key來向Stripe 伺服器索要token，具體是客戶端呼叫以下方法
```
// cardElement： 用以擷取使用者輸入卡號的元件
stripe.createToken(cardElement)
```
2. Stripe 伺服器收到後就檢驗付款資料和Key
	- 若檢驗失敗的話，Stripe伺服器就回傳失敗訊息
	-

![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1656883162/blog/paymentFlow/stripe/token_and_charge_flow_gmbat7.png)


## 複習
#🧠 Question :: ->->-> ``

---
Status: 
Tags:
[[Stripe]]
Links:
[[Stripe Payment Element 是Stripe 提供於UI開發的元件來從而擷取使用者透過該元件的輸入結果並產出伺服器容易處理的結果，其元件具體會是由部分DOM節點和事件綁定來構成]]
References: