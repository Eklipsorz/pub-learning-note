

## 描述

引用[[@redisKEYS]]所述：
```
redis:6379> MSET firstname Jack lastname Stuntman age 35
"OK"
redis:6379> KEYS *name*
1) "firstname"
2) "lastname"
redis:6379> KEYS a??
1) "age"
redis:6379> KEYS *
1) "age"
2) "firstname"
3) "lastname"

redis:6379>
```
## 複習
#🧠 Question :: ->->-> ``

---
Status: #📥 
Tags:
[[Redis]] 
Links:
References:
[[@redisKEYS]]