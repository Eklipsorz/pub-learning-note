## 描述

引用[[@redisEXPIRERedis]]所描述的：
> Redis keys are expired in two ways: a passive way, and an active way.

> A key is passively expired simply when some client tries to access it, and the key is found to be timed out.

> Of course this is not enough as there are expired keys that will never be accessed again. These keys should be expired anyway, so periodically Redis tests a few keys at random among keys with an expire set. All the keys that are already expired are deleted from the keyspace.

> Specifically this is what Redis does 10 times per second:
> 1.  Test 20 random keys from the set of keys with an associated expire.
> 2.  Delete all the keys found expired.
> 3.  If more than 25% of keys were expired, start again from step 1.

> This is a trivial probabilistic algorithm, basically the assumption is that our sample is representative of the whole key space, and we continue to expire until the percentage of keys that are likely to be expired is under 25%

> This means that at any given moment the maximum amount of keys already expired that are using memory is at max equal to max amount of write operations per second divided by 4.

引用[[@wljRedisZiLiaoYiJingGuoQiLiaoWeiShiMoHuanZhanYongJiYiTi]]所描述：
> ## redis的過期策略
> redis的過期策略：定期刪除+惰性刪除
> -   定期刪除：redis預設是每隔100ms就隨機抽取一些設定了過期時間的key，檢查其是否過期，如果過期就刪除。
> -   惰性刪除：在你獲取某個key的時候，redis會檢查一下 ，這個key如果設定了過期時間那麼是否過期了？如果過期了此時就會刪除，不會給你返回任何東西

重點：
- redis 過期刪掉key-value pair的方式具體來說有兩種，並且皆以key來代表整個key-value pair
	- passive deletion / passive way
	- active deletion / active way
- redis 系統一旦執行時就會同時執行passive deletion 和 active deletion，並不會挑選其中一樣來實現
- redis passive deletion：系統不主動檢查哪些key已經過期以及進行過期刪掉，只會在客戶端對著key存取時，才會檢查key是否過期和過期的話就刪掉的回應
- redis active deletion：系統主動檢查哪些key已經過期以及進行過期刪掉，每一秒會做十次執行以下具體行為：
	- 隨機挑選20個key來檢查是否過期
	- 將對應過期key的key-value pair進行刪除；將對應沒過期key的key-value pair進行保留
	- 如果過期的key佔整體key的比率超過25%，就回到第一個步驟，直到過期key的比率低於25%
- redis active deletion 是出自於官方的經驗法則，這表示每一秒對於已過期的key-value pair進行寫入的 最大會是25%

## 複習
#🧠 Question :: ->->-> ``

---
Status: 
Tags:
Links:
References:
[[@redisEXPIRERedis]]
[[@wljRedisZiLiaoYiJingGuoQiLiaoWeiShiMoHuanZhanYongJiYiTi]]