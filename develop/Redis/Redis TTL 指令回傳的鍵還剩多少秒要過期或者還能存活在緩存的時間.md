


## 描述

> Returns the remaining time to live of a key that has a timeout. This introspection capability allows a Redis client to check how many seconds a given key will continue to be part of the dataset.

語法形式為：
> TTL key




> Starting with Redis 2.8 the return value in case of error changed:

> -   The command returns `-2` if the key does not exist.
> -   The command returns `-1` if the key exists but has no associated expire.
重點：
- TTL 指令回傳的鍵還剩多少秒要過期或者還能存活在緩存的時間
- 形式為：key為指定key值
```
TTL <key>
```
- 可若回傳-1的話，就表示key存在，但就沒綁定過期時間，另外，當對redis新增一些key，預設是不會設定過期時間
- 可若回傳-2的話，就表示key不存在

### Note
1. TTL 是指Time to live，意指為存活時間，在Redis上是指該key-value pairs還能在緩存存活的秒數


## 複習
#🧠 Redis TTL上是指哪個英文全名？意思為？ ->->-> `Time to live，意指為存活時間，在Redis上是指該key-value pairs還能在緩存存活的秒數`
<!--SR:!2022-12-10,78,210-->

#🧠 Redis TTL key 是什麼指令 ->->-> `獲取KEY還能在緩存存活的秒數，會以過期時間來計算`
<!--SR:!2023-05-08,201,248-->

#🧠 Redis TTL key 回傳 -1 就表示什麼？ ->->-> `就表示key存在，但就沒綁定過期時間`
<!--SR:!2022-10-27,79,248-->

#🧠 Redis TTL key 回傳-2 就表示什麼？ ->->-> `就表示key不存在`
<!--SR:!2023-04-06,176,248-->

#🧠 當對redis新增一些key時，redis會幫助我們設定預設的過期時間給這些key嗎？->->-> `redis並不會設定預設的過期時間給key`
<!--SR:!2022-11-01,82,248-->

---
Status: #🌱 
Tags:
[[Redis]]
Links:
References: