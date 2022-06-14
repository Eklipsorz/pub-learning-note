


## 描述

> Returns the remaining time to live of a key that has a timeout. This introspection capability allows a Redis client to check how many seconds a given key will continue to be part of the dataset.

語法形式為：
> TTL key

重點：
- TTL 指令回傳的鍵還剩多少秒要過期或者還能存活在緩存的時間
- 形式為：key為指定key值
```
TTL <key>
```

### Note
1. TTL 是指Time to live，意指為存活時間，在Redis上是指該key-value pairs還能在緩存存活的秒數


## 複習
#🧠 Redis TTL上是指哪個英文全名？意思為？ ->->-> `Time to live，意指為存活時間，在Redis上是指該key-value pairs還能在緩存存活的秒數`
<!--SR:!2022-06-19,5,230-->

#🧠 Redis TTL key 是什麼指令 ->->-> `獲取KEY還能在緩存存活的秒數，會以過期時間來計算`
<!--SR:!2022-06-18,5,248-->


---
Status: #🌱 
Tags:
[[Redis]]
Links:
References: