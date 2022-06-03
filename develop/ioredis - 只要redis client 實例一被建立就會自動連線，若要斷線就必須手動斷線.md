
## 描述

### 當redis client實例一被建立時


> ## Connect to Redis

> When a new `Redis` instance is created, a connection to Redis will be created at the same time. You can specify which Redis to connect to by:
```
new Redis(); // Connect to 127.0.0.1:6379
new Redis(6380); // 127.0.0.1:6380
new Redis(6379, "192.168.1.1"); // 192.168.1.1:6379
new Redis("/tmp/redis.sock");
new Redis({
  port: 6379, // Redis port
  host: "127.0.0.1", // Redis host
  username: "default", // needs Redis >= 6
  password: "my-top-secret",
  db: 0, // Defaults to 0
});
```

```
// Connect to 127.0.0.1:6380, db 4, using password "authpassword":
new Redis("redis://:authpassword@127.0.0.1:6380/4");
```

```
// Username can also be passed via URI.
new Redis("redis://username:authpassword@127.0.0.1:6380/4");
```


重點：
- 只要redis client實例使用下述方法來建立，就會自動與redis server連線
```
const client = new Redis(....)
```
- Redis 建構式可以放連線資訊，來幫助連線

### 那ioredis 如何斷線

> By default, ioredis will try to reconnect when the connection to Redis is lost except when the connection is closed manually
> 
>   by `redis.disconnect()` or `redis.quit()`.

ioredis 每一次當開發者對redis存取會自動與資料庫連線，但不會自己斷線，除非自己手動執行

```
redis.disconnect() 
or 
redis.quit()
```

## 複習

#🧠 ioredis 如何與redis資料庫系統連線->->-> `只要建構出redis client實例就會自動與redis server連線`
<!--SR:!2022-06-06,3,250-->

#🧠 ioredis 如何與redis資料庫系統斷線->->-> `預設上只會自己連線，不會自己斷線，得手動調用ioredis的redis.discconect或者redis.quit才能順利斷線`

---
Status: #🌱 
Tags:
[[Redis]] - [[Redis Client]]
Links:
[[由於node-redis本身穩定性不高且沒金主支持而轉而較穩定的client - ioredis]]
References:
[[@liFeatures2022]]