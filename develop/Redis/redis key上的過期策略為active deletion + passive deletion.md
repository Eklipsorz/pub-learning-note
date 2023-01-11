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
- redis active deletion 是出自於官方的經驗法則，這表示每一秒對於已過期的key-value pair進行寫入的key數量最大會是25%

### 是不是還存在著過期key仍未釋放的情況
使用著passive deletion和active deletion之後，是不是還存在著過期key仍未釋放的情況？ 答案是可能的，若是這樣，也表明著KEY過期機制上出現著：
	- passive deletion 漏洞：從未存取過的過期key
	- active deletion 漏洞：
		- (所有種類)key增加速率大於key被釋放速率，會出現部分過期key無法被隨機挑選到，接而被刪除釋放。
		- 釋放速率太慢，以至於還會有過期的key
	
那麼這問題的解法可以根據：
[[@wljRedisZiLiaoYiJingGuoQiLiaoWeiShiMoHuanZhanYongJiYiTi]]：
> ### 我插入redis的資料應該過期了，為什麼還佔用記憶體？
> **可是有了定期刪除和惰性刪除就可以保證過期的key真的被刪掉嗎？**

> 當然不能，問題2就是一個明顯的例子

> 問題2的解決：設定記憶體淘汰機制

重點：
- 除了passive deletion因依據使用者來控制所以對於伺服器而言，是一個不可控因素以外，就只能透過active deletion漏洞來解決，從該漏洞可以得知其問題源自於過期key的數量增加速率大於釋放速率，那麼就表示過期key數量一直在增加
- 根據第一點來看敘述：記憶體遲早有一天會被塞爆，那麼就從記憶體釋放來淘汰掉一些無法從passive deletion 和 active deletion機制刪掉的key


## 複習
#🧠 redis 如何處理key的過期？採取什麼樣策略->->-> `redis 系統一旦執行時就會同時執行passive deletion 和 active deletion，並不會挑選其中一樣來實現`
<!--SR:!2023-03-05,165,250-->

#🧠 redis passive deletion 是什麼樣的技術(重複)？ ->->-> `系統不主動檢查哪些key已經過期以及進行過期刪掉，只會在客戶端對著key存取時，才會檢查key是否過期和過期的話就刪掉的回應`
<!--SR:!2023-11-10,314,250-->

#🧠 redis active deletion 是什麼樣的技術(重複)? ->->-> `系統主動檢查哪些key已經過期以及進行過期刪掉，每一秒會做十次執行以下具體行為：隨機挑選20個key來檢查是否過期、將對應過期key的key-value pair進行刪除；將對應沒過期key的key-value pair進行保留、如果過期的key佔整體key的比率超過25%，就回到第一個步驟，直到過期key的比率低於25%`
<!--SR:!2023-01-19,10,229-->

#🧠 redis active deletion 是系統主動檢查哪些key已經過期以及進行過期刪掉，每一秒會做十次執行以下具體行為...，請問具體每一秒會做十次是如何實現？->->-> `也就是設定每100ms就做一次`
<!--SR:!2023-01-17,6,247-->

#🧠 redis active deletion 是系統主動檢查哪些key已經過期以及進行過期刪掉，每一秒會做十次執行以下具體行為...，請問具體每一秒會做十次是如何實現？換言之會是指？ ->->-> `系統每100ms做一次以下行為：：隨機挑選20個key來檢查是否過期、將對應過期key的key-value pair進行刪除；將對應沒過期key的key-value pair進行保留、如果過期的key佔整體key的比率超過25%，就回到第一個步驟，直到過期key的比率低於25%`
<!--SR:!2023-01-16,5,247-->


#🧠  redis active deletion 的策略是出自於？->->-> `官方的經驗法則`
<!--SR:!2023-04-09,190,250-->

#🧠 使用著passive deletion和active deletion之後，是不是還存在著過期key仍未釋放的情況？->->-> `答案是可能的`
<!--SR:!2023-02-14,59,230-->

#🧠 使用著passive deletion和active deletion之後可能存在過期key仍未釋放的情況 ，那麼原因會是什麼？->->-> `若是這樣，也表明著KEY過期機制上出現著：1. passive deletion 漏洞：從未存取過的過期key 2. active deletion 漏洞：- (所有種類)key增加速率大於key被釋放速率，會出現部分過期key無法被隨機挑選到，接而被刪除釋放。 - 釋放速率太慢，以至於還會有過期的key`
<!--SR:!2023-05-01,185,250-->


#🧠 使用著passive deletion和active deletion之後可能存在過期key仍未釋放的情況：解法可能可以朝著passive deletion 和 active deletion的缺失走嗎 ->->-> `passive deletion為因依據使用者來控制所以對於伺服器而言，是一個不可控因素，就只能透過active deletion漏洞來解決`
<!--SR:!2023-03-23,177,250-->

#🧠 使用著passive deletion和active deletion之後可能存在過期key仍未釋放的情況：解法朝著active deletion漏洞解決，那麼方向會是如何(提示：增加速率大於釋放速率)>->-> `從該漏洞可以得知其問題源自於過期key的數量增加速率大於釋放速率或者釋放速率太慢，那麼就表示過期key數量一直都會在`


#🧠 使用著passive deletion和active deletion之後可能存在過期key仍未釋放的情況：解法朝著active deletion的方向，會構成什麼樣的解法(提示：記憶體遲早有一天會被塞爆) ->->-> `記憶體遲早有一天會被塞爆，那麼就從記憶體釋放來淘汰掉一些無法從passive deletion 和 active deletion機制刪掉的key`
<!--SR:!2023-02-23,160,250-->


---
Status: #🌱 
Tags:
[[Redis]] - [[Database]]
Links:
[[redis 刪除過期鍵值有兩種方式：鍵值有被存取才去檢查過期和刪除、每隔一段時間挑選幾個鍵來檢查過期和刪除]]
[[Key eviction 是Redis 釋放記憶體空間的策略]]
References:
[[@redisEXPIRERedis]]
[[@wljRedisZiLiaoYiJingGuoQiLiaoWeiShiMoHuanZhanYongJiYiTi]]