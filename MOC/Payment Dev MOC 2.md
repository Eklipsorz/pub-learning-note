
## 付款概念
- 信用卡資料和確認付款是否可分開？
[[金流服務 - 輸入信用卡資料和確認付款這兩項動作是可以分開]]

## Stripe




### 付款方式
- intents
[[Stripe Payment Intents 是後端伺服器給予付款權利至客戶端，讓它自行決定何時付款]]
- charges
[[Stripe Token+Charges整體流程：客戶端建立卡元素、透過卡元素建立對應token、向伺服器傳遞token、伺服器透過token向stripe付款]]

- intents 和 charges 在地區上的支援
[[Stripe Tokens + Charge API 適用於美加地區，Payment Intents API適用於全球]]

### 客戶端擷取付款資料
- Payment Element
[[Stripe Payment Element 是Stripe 提供於UI開發的元件來從而擷取使用者透過該元件的輸入結果並產出伺服器容易處理的結果，其元件具體會是由部分DOM節點和事件綁定來構成]]
