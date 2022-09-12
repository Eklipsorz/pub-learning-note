
## 描述
 [[@notesRedisKeyExpiration2022]]
> # **Redis 刪除過期的鍵值，有兩種方式:**

> _1. Passive(被動被動刪除) : 當該鍵值被存取到時，若該鍵值已過期，則會先刪除該鍵值，而後回覆空值給前端應用。_
> 
> _2. Active(主動刪除) : 每隔 100 milliseconds 隨機挑選 20 個鍵值，然後刪除過期鍵值，若這20個鍵值中，有超過25%是過期的鍵值，則會重複這個動作，直到過期比率低於25%。 (每秒做10次，每次挑20個鍵值)_

> One lazy way deletes a key when it is requested by a command, but it is found to be already expired._

>One active way expires a few keys every 100 milliseconds._

根據[[@redisEXPIRE]] 所描述
> A key is passively expired simply when some client tries to access it, and the key is found to be timed out.

> Of course this is not enough as there are expired keys that will never be accessed again. These keys should be expired anyway, so periodically Redis tests a few keys at random among keys with an expire set. All the keys that are already expired are deleted from the keyspace.

> Specifically this is what Redis does 10 times per second:

> 1.  Test 20 random keys from the set of keys with an associated expire.
> 2.  Delete all the keys found expired.
> 3.  If more than 25% of keys were expired, start again from step 1.


重點：
- Redis 如何刪除過期的鍵值或者刪掉key-value pair，主要有兩種形式：
	- Passive deletion
	- Active deletion
- Passive deletion 是指系統不主動去查哪些key已經過期，而是當因為請求讀取到key才會檢查是否過期，若過期就直接刪除
- Active deletion 是指系統本身主動每100ms從資料庫內挑出20組key來檢查是否過期並刪除




## 複習
#🧠 Redis 如何刪除過期的鍵值或者刪掉過期的key-value pair (有三種方式) ->->-> `passive deletion、active deletion、key eviction`
<!--SR:!2022-11-01,74,250-->


#🧠 Redis 上的passive deletion 是如何解決過期的key->->-> `是指系統不主動去查哪些key已經過期，而是當因為請求讀取到key才會檢查是否過期，若過期就直接刪除`
<!--SR:!2023-02-25,166,250-->

#🧠 Redis 上的Active deletion 是如何解決過期的key ->->-> `指系統本身主動每100ms從資料庫內挑出20組key來檢查是否過期並刪除`
<!--SR:!2023-01-16,138,250-->

---
Status: #🌱 
Tags:
[[Redis]]
Links:
[[redis key上的過期策略為active deletion + passive deletion]]
References:
[[@redisEXPIRE]]
[[@notesRedisKeyExpiration2022]]
