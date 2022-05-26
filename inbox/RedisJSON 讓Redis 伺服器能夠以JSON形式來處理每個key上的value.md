
## 描述

引用[[@redisRedisJSON]]所描述的：
> RedisJSON is a [Redis](https://redis.io/) module that provides JSON support in Redis. RedisJSON lets your store, update, and retrieve JSON values in Redis just as you would with any other Redis data type. RedisJSON also works seamlessly with RediSearch to let you index and query your JSON documents.

以參考資料所提示的使用方法：
> We recommend you have Redis load the module during startup by adding the following to your `redis.conf` file:
```
	loadmodule /path/to/module/target/release/librejson.so
```

> On Mac OS, if this module has been built as a dynamic library use:

```
	loadmodule /path/to/module/target/release/librejson.dylib
```

> In the above lines replace `/path/to/module/` with the actual path to the module's library.

> Alternatively, you can have Redis load the module using the following command line argument syntax:

```bash
~/$ redis-server --loadmodule ./target/release/librejson.so
```


重點：
- RedisJSON 是一個Redis 官方模組，用途為讓Redis伺服器能以JSON形式來處理每個key上的value
- 如何使用RedisJSON 模組：
	- 在redis.conf 設定其模組
	```
	loadmodule /path/to/module/target/release/librejson.so
	```
	- 直接在執行redis-server一同載入該模組
	```bash
	~/$ redis-server --loadmodule ./target/release/librejson.so
	```

## 模組所在
https://github.com/RedisJSON/RedisJSON/releases

---
Status: #📥 
Tags:
[[JSON]] - [[Redis]]
Links:
References:
[[@redisRedisJSON]]