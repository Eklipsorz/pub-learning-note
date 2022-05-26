
## 描述


若一開始於Redis載入RedisJSON模組並設定JSON格式的value讓其儲存db的話，接著若以沒載入其模組的情況下執行Redis Server 會出錯，其錯誤訊息如下：

```
15279:M 26 May 2022 22:54:41.469 # Internal error in RDB reading offset 0, function at rdb.c:2625 -> The RDB file contains module data I can't load: no matching module type 'ReJSON-RL'
[offset 0] Checking RDB file dump.rdb
[offset 26] AUX FIELD redis-ver = '7.0.0'
[offset 40] AUX FIELD redis-bits = '64'
[offset 52] AUX FIELD ctime = '1653576873'
[offset 67] AUX FIELD used-mem = '1136672'
[offset 79] AUX FIELD aof-base = '0'
[offset 81] Selecting DB ID 0
[offset 164] Checksum OK
[offset 164] \o/ RDB looks OK! \o/
[info] 4 keys read
[info] 0 expires
[info] 0 already expired
```


## 解法
流程：若資料本身不重要的話
- 先以載入RedisJSON的情況下執行redis-server
- 並刪除對應JSON格式的資料，進入redis-cli下達
```
FLUSHALL
```
- 重新以沒載入RedisJSON的情況下執行redis-server

---
Status: #📥 
Tags:
[[Redis]]
Links:
[[RedisJSON 讓Redis 伺服器能夠以JSON形式來處理每個key上的value]]
References:
