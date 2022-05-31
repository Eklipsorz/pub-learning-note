
## 描述
 [[@notesRedisKeyExpiration2022]]
> # **Redis 刪除過期的鍵值，有兩種方式:**

> _1. Passive(被動被動刪除) : 當該鍵值被存取到時，若該鍵值已過期，則會先刪除該鍵值，而後回覆空值給前端應用。_
> 
> _2. Active(主動刪除) : 每隔 100 milliseconds 隨機挑選 20 個鍵值，然後刪除過期鍵值，若這20個鍵值中，有超過25%是過期的鍵值，則會重複這個動作，直到過期比率低於25%。 (每秒做10次，每次挑20個鍵值)_


## 複習
#🧠 Question :: ->->-> ``

---
Status: 
Tags:
Links:
References:
[[@notesRedisKeyExpiration2022]]