
## 描述
### Redis 介紹
引用[[@linNodeJsShiYong2018]]所述：

> Redis 是一種內存資料庫(in-memory)的架構，可以被當作一個簡易的資料庫(key-value database) 
引用[[@ithomeDay23RubyRails]]所述：

> Single Thread I/O Multiplex


redis ：
- 是以記憶體來構築的資料庫，資料庫內部的資料皆由key-value pair所構成。
- redis server 是以單執行緒來執行


> Redis 使用 RAM 來存取資料所以相對來得快速，缺點是重開機後記憶體就會被釋放掉，但 Redis 有個功能 persistence 可以解決這個問題，此外 Redis 也能設定資料的生命週期(Expire)當你在儲存資料的時候，你可以新增一個 Expire time 的參數，時間一到之後，這個 key 就會自動被清除 

redis 優點：
- 由於資料庫建立在記憶體上，所以存取較快速
- 能設定紀錄的過期時間：設定Expire time參數來定義時間，時間一到就會清除對應的紀錄

缺點：
- 會隨著記憶體重開機而跟著釋放資料，不過可採取persistence功能，讓同樣內容的資料儲存在硬碟和記憶體，當記憶體那份資料被釋放時，可由硬碟上的資料還原過來


### 安裝方式

流程為：
- 先至redis官方下載，並解壓縮出對應的目錄
- 移動至其目錄下的src子目錄，然後下達make來編譯redis-server和redis-cli
> 並輸入 make，系統會自動幫你編譯產出 redis-server 與 redis-cli。 



### redis-server
主要負責建立redis 資料庫的伺服器，用以接收請求和處理請求，預設port 為**6379**

若要指定其他port，指令會是如下，其中[port]會是指定伺服器接收請求的port，執行完便會直接執行redis-server來架設redis伺服器
```
./redis-server --port [port]
```

若沒添加的話，就預設為6379
```
./redis-server
```

#### 讓redis-server 變成 daemon

執行以下指令，就能使redis-server在背景下執行並於那接收/處理請求
```
 src/redis-server --daemonize yes 
```

關閉該redis-server 所有相關的process
```
pkill -u $USER redis-server 
```
### redis-cli
引用[[@redisRedisCLI]]所述：
> The `redis-cli` (Redis command line interface) is a terminal program used to send commands to and read replies from the Redis server.

redis-cli 是個與redis server相連接的介面程式：
- 附加一組指令來遠端操控對應redis server
- 可指定連接哪一個redis server




### redis-cli 指令

#### SET
SET 指令為設定對應key所擁有的value值，用法為
```
SET key value
```

e.g., SET something hi

設定一個紀錄，其中它的key為something，而對應的value會是hi

#### GET
GET 指令為回傳對應key的value，用法為
```
GET key
```
e.g., GET something

回傳一筆key值為something的紀錄所擁有的value值

## 複習


#🧠 Redis 系統是多執行緒？還是單執行緒？ ->->-> `單執行緒`
<!--SR:!2022-06-25,8,250-->


---
Status: #🌱 
Tags:
[[RedisJSON 讓Redis 伺服器能夠以JSON形式來處理每個key上的value]] - [[NoSQL]]
Links:
[[node.js 透過node-redis程式來與redis server連線並下達對應資料庫指令]]
References:
[[@linNodeJsShiYong2018]]
[[@ithomeDay23RubyRails]]
[[@redisRedisCLI]]
