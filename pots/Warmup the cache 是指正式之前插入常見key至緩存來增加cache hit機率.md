## 描述
根據[[@fasterrizeCacheWarmingWhy]]所描述：
> Warming up the cache involves **artificially filling the cache so that real visitors always have cache access**

重點：
- Warm本身是指使用頻率介於 hot和cold之間，而warmup則是表明從cold狀態提升使用頻率，而在這裡是指藉由添加資料至緩存來增加緩存被使用的頻率
- Warmup the cache 是指事先插入常出現的資料至緩存來增加cache hit機率，從而增加效率
## 複習
#🧠 Warmup the cache是什麼樣的技術->->-> `事先插入常出現的資料至緩存來增加cache hit機率，從而增加效率`
<!--SR:!2022-06-14,9,250-->

---
Status: #🌱 
Tags:
[[Redis]]
Links:
[[hot、cold、warm 是強調著資料的使用率，hot是頻繁存取的資料、cold是偶爾存取的資料、warm則是之間]]
References:
[[@fasterrizeCacheWarmingWhy]]