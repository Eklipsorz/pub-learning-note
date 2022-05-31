

老牌的redis client - node redis本身有版本上的相容性問題，且後面沒金主可以支持開發者，因此轉而使用ioredis


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