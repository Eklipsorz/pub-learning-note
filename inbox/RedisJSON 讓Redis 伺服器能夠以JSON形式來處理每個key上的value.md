
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
其模組主要會是以Rust語言所撰寫的，若要安裝的話，勢必會搭配其套件管理器-cargo來下載安裝其他該模組所依賴的套件，並編譯出RedisJSON模組
https://github.com/RedisJSON/RedisJSON/releases

## 模組安裝方式
流程為
- 下載RedisJSON模組
- 安裝Rust以及其套件管理器-cargo
```
curl --proto '=https' --tlsv1.2 -sSf https://sh.rustup.rs | sh
```
- 於RedisJSON模組原始碼首頁下執行以下指令
```
cargo build --release
```
- 測試其模組是否為正常功能下的模組
```
cargo test --features test
```
- 檢查RedisJSON首頁下的target目錄是否有以下模組
```
/target/release/librejson.dylib
```

## 模組相關問題
[[Redis 伺服器若讀取到錯誤格式的資料庫會無法執行]]

---
Status: #📥 
Tags:
[[JSON]] - [[Redis]]
Links:
[[Redis 伺服器若讀取到錯誤格式的資料庫會無法執行]]
References:
[[@redisRedisJSON]]