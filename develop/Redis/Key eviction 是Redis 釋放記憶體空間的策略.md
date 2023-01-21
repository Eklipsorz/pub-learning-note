
## 描述

引用[[@redisKeyEviction]]所描述：
> Overview of Redis key eviction policies (LRU, LFU, etc.)

> When Redis is used as a cache, it is often convenient to let it automatically evict old data as you add new data. This behavior is well known in the developer community, since it is the default behavior for the popular_memcached_ system.

> This page covers the more general topic of the Redis `maxmemory` directive used to limit the memory usage to a fixed amount. This page it also covers in depth the LRU eviction algorithm used by Redis, that is actually an approximation of the exact LRU.

引用[[@wljRedisZiLiaoYiJingGuoQiLiaoWeiShiMoHuanZhanYongJiYiTi]]所描述：
> ## redis中的記憶體淘汰機制

> 如果redis的記憶體佔用過多的時候，此時會進行記憶體淘汰，有如下一些策略：
> 1）**noeviction**：對於寫請求不再提供服務，直接返回錯誤
> 2）**allkeys-lru**：從鍵空間中，移除最近最少使用的key（這個是最常用的）
> 3）**allkeys-random**：從所有key中隨機淘汰資料
> 4）**volatile-lru**：從設定了過期時間的鍵空間中，移除最近最少使用的key（這個一般不太合適）
> 5）**volatile-random**：從設定了過期時間的鍵空間中，隨機移除某個key
> 6）**volatile-ttl**：從設定了過期時間的鍵空間中，有更早過期時間的key優先移除

重點：
- 是redis 在記憶體使用過多的情況所執行之釋放記憶體空間的策略，主要釋放key-value pairs
- 其策略主要會依據著過期key、LRU、LFU來決定哪些KEY要被移除




## 複習
#🧠 Redis key eviction 是什麼？  ->->-> `是redis 在記憶體使用過多的情況所執行之釋放記憶體空間的策略`
<!--SR:!2023-01-24,3,250-->

#🧠 Redis key eviction 是redis 在記憶體使用過多的情況所執行之釋放記憶體空間的策略，主要釋放什麼？  ->->-> `key-value pairs`
<!--SR:!2023-01-24,3,250-->

#🧠 Redis key eviction決定哪些KEY要被移除的策略是 (過期key)->->-> `其策略主要會依據著過期key、LRU、LFU來決定哪些KEY要被移除`




---
Status: #🌱 
Tags:
[[Memory]] - [[Redis]]
Links:
[[redis 刪除過期鍵值有兩種方式：鍵值有被存取才去檢查過期和刪除、每隔一段時間挑選幾個鍵來檢查過期和刪除]]
[[redis key上的過期策略為active deletion + passive deletion]]
[[緩存用來決定哪些資料區塊先被釋放的演算法：LRU、LFU、FIFO]]
References:
[[@redisKeyEviction]]
[[@wljRedisZiLiaoYiJingGuoQiLiaoWeiShiMoHuanZhanYongJiYiTi]]