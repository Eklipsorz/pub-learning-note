

## 描述
KEYS 是Redis 指令，形式會是：
```
KEYS <pattern>
```


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
<!--SR:!2022-06-17,9,250-->

---
Status: #📥 
Tags:
[[Redis]] 
Links:
[[Redis KEYS 指令的缺點主要有沒分頁、資料越多成本越高的O(n)、前兩者導致的阻塞問題]]
References:
[[@redisKEYS]]