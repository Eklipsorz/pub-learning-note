
## Redis Client 
- ioredis 
[[由於node-redis本身穩定性不高且沒金主支持而轉而較穩定的client - ioredis]]
[[ioredis - 只要redis client 實例一被建立就會自動連線，若要斷線就必須手動斷線]]

- node-redis
[[node-redis - 當createClient 帶有legacyMode參數時會於connect和quit出現錯誤]]

- disconnent vs quit
[[redit-  .quit() vs .disconnect()差別在於前者會於結束前允許執行後續來不及執行，後者是直接斷開連線]]

## 模組

- RedisJSON
[[RedisJSON 讓Redis 伺服器能夠以JSON形式來處理每個key上的value]]

- 問題：若一開始於Redis載入RedisJSON模組並設定JSON格式的value讓其儲存db的話，接著若以沒載入其模組的情況下執行Redis Server 會出錯
[[Redis 伺服器若讀取到錯誤格式的資料庫會無法執行]]


- RedisJSON JSONPath
[[RedisJSON JSONPath 是RedisJSON開發人員所針對JSONPath概念而開發出來的產品]]

- connect-redis
[[connect-redis 替伺服器建構以redis為主的session 儲存空間]]
[[connect-redis 支援 redis 4.x (npm) 必須要添加 legacyMode 為true的參數]]

## 使用策略
- Caching Strategy
[[Caching MOC]]

- Warmup the cache
[[Warmup the cache 是指正式之前插入常見key至緩存來增加cache hit機率]]

- Read/Write Splitting
[[Read-Write Splitting 是指在多個主機共享同個資料庫資料的情況下專門提供專門讀取資料的主機和專門寫資料的主機]]


## Redis 基礎知識
- 資料庫是否能自行建立？其名稱為
[[redis 本身的資料庫名稱皆為數字，且由系統自行建立，每個資料庫都是獨立的]]

- Redis 為什麼是以單執行緒作為主要處理
[[redis 主要採取單執行緒的原因是因為避免不必要的鎖成本、執行緒切換執行]]


## Redis + Lua
[[Redis 需要Lua指令是由於想透過從伺服器內部直接執行腳本來提昇指令被執行的效率以及替多個指令轉換成原子化操作]]

### 前置概念
- Dictionary (HashTable)
[[dictionary 是如同字典一般儲存多個key-value pairs，key會是關鍵字，value則是解釋關鍵字的描述]]

- hot、warm、cold
[[hot、cold、warm 是強調著資料的使用率，hot是頻繁存取的資料、cold是偶爾存取的資料、warm則是之間]]

- backup type
[[hot backup 是指在備份系統與實際要備份資料的系統同時併行下進行實時備份或者頻率高到像實時的備份任務]]
[[cold backup 是指在實際備份資料的系統離線下進行備份]]
[[warm backup 是備份系統與實際要備份資料的系統同時執行下進行備份頻率介於cold和hot之間的備份]]

- database cursor
[[Database Cursor 是一個用字串或數字去對應過去處理結果並透過該索引值來將呈現資料導向成對應處理結果之機制]]
[[Database Cursor 會使用Shared Lock來將要給開發者存取的資料集合鎖死，以避免被人修改]]
[[Forward-only cursor 是只紀錄使用者接下來要指向的資料集合，過去所遍歷的資料集合將會直接釋放]]

- Binary-Safe function
[[Binary-Safe function 是指一個在處理二進制內容的過程中會以二進制來處理且不會以特殊格式來看待並進而破壞內容的函式]]

- Thread switch
[[執行緒切換(Thread switch) 是指N個執行緒實際無法從環境同時拿到N個實體核心執行時，就會輪流獲取核心來執行]]

### 設定檔案
- redis.conf
[[redis.conf 是設定Redis 伺服器預設要執行的參數]]

### 型別

- String vs. Hash
[[Redis- String適用場景為讀取場景較多，且更新快取不頻繁；Hash適用場景為更新較為頻繁(尤其是指定特定key)，或者讀取特定key值]]

- Value 主要型別
[[Redis 的Value主要結構為 String 和 Hash]]
[[Redis Hash 遇到 巢狀結構的資料的話，又是面臨到要以String或者Hash來儲存的問題]]

- Simple Dynamic String
[[Redis Simple Dynamic String會根據實際儲存字串的內容來調整其記憶體空間]]
[[Redis 面對String 會以Binary-safe來處理，這表示它會以二進制格式來看待String]]

- Hash
[[Redis Hash是儲存多個key-value的字典]]

### Redis 如何處理過期的key
- passive deletion 和. active deletion
[[redis 刪除過期鍵值有兩種方式：鍵值有被存取才去檢查過期和刪除、每隔一段時間挑選幾個鍵來檢查過期和刪除]]

- redis key 的過期策略
[[redis key上的過期策略為active deletion + passive deletion]]

- key eviction
[[Key eviction 是Redis 釋放記憶體空間的策略]]
[[緩存用來決定哪些資料區塊先被釋放的演算法：LRU、LFU、FIFO]]

### Redis Sub/Pub
- 前置知識
[[messaging pattern 是定義兩個程式模組如何連接和交流的風格]]
[[publish–subscribe是傳遞者可將訊息發布在指定頻道，接收者只需要訂閱指定頻道來接收訊息的messaging pattern]]

- Keyspace notification & Keyevent notification
[[Redis pub&sub - keyspace notification 是以指定key的任意事件來進行pub和sub，而keyevent notification 是以任意key上的指定事件來進行pub和sub]]

### Redis 資料庫本身的指令
- quit
[[redis.quit 和 redis.disconnect 是對應redis上的指令嗎]]

- Scan
 [[Redis Scan 是按依據數量來對資料庫的資料來分頁並且提供開發者以指定cursor來導向對應的資料群組]]
 [[Redis Scan 是按依據數量來對資料庫的資料來分頁並且提供開發者以指定cursor來導向對應的資料群組]]

- KEYS
[[Redis KEYS 可以使用表達式來找到符合表達式的key]]
[[Redis KEYS 指令的缺點主要有沒分頁、資料越多成本越高的O(n)、前兩者導致的阻塞問題]]

- TTL
[[Redis TTL 指令回傳的鍵還剩多少秒要過期或者還能存活在緩存的時間]]

### master/slave
- master/slave 
[[redis master-slave 架構是 master主機負責對資料做寫入，slave主機負責對資料做存取]]

- redis sentinel
[[redis sentinel 模式是監測master+slave結構下的所有主機並根據是否故障來調整可用主機給客戶端使用]]