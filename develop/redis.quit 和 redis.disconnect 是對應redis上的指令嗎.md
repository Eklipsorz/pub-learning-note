## 描述



### redis 官方頂多有kill 和 quit

引用 [[@redisQUIT]] 所描述的quit：
> The `CLIENT KILL` command closes a given client connection.

引用 [[@redisQUIT]] 所描述的quit：
> Ask the server to close the connection. The connection is closed as soon as all pending replies have been written to the client

重點：
- client kill指令會替客戶端向伺服器發出斷線請求
- quit指令會替客戶端向伺服器發出斷線請求，並於斷線前將目前接收到的請求先完成一遍且不再接收任何請求，只要一執行完畢就直接斷線
- 在斷線前收到的請求會是以佇列(Queue)形式來存放


### 在node-redis上的函式
引用[[@NodeRedis2022]]所描述：
#### .disconnect()
> #### `.disconnect()`

> Forcibly close a client's connection to Redis immediately. Calling `disconnect` will not send further pending commands to the Redis server, or wait for or parse outstanding responses.

> await client.disconnect();

重點：
- disconnect 是直接讓客戶端與redis 伺服器斷線，不論在斷線是否還有請求，都是先斷線

#### .QUIT() / .quit()
> #### `.QUIT()`/`.quit()`

> Gracefully close a client's connection to Redis, by sending the [`QUIT`](https://redis.io/commands/quit) command to the server. Before quitting, the client executes any remaining commands in its queue, and will receive replies from Redis for each of them.

重點：
- 直接從client端發送redis資料庫系統本身就有的quit指令

### 在ioredis上的函式
引用[[@liFeatures2022]]所描述
> By default, ioredis will try to reconnect when the connection to Redis is lost except when the connection is closed manually by `redis.disconnect()` or `redis.quit()`.

### 總結
.quit() 會是對應資料庫上的quit指令，而disconnect未指明，但應該會是指client kill

## 複習
#🧠 redis client實現上在斷線上會有相關的disconnect和quit，請問這兩個有什麼差別->->-> `disconnect只會直接與伺服器斷線，而quit則是除了斷線以外，還會注意斷線前有哪些請求還未完成，並先讓伺服器處理這些請求並且不再接收任何請求，接著再來斷線`

#🧠 redis client 端上的.quit()和.disconnect()對應哪些redis 本身提供的指令->->-> `.quit()對應至quit指令，而.disconnect()則對應著直接斷線的client kill指令`

---
Status: #🌱 
Tags:
[[Redis]] - [[Redis Client]]
Links:
[[redit-  .quit() vs .disconnect()差別在於前者會於結束前允許執行後續來不及執行，後者是直接斷開連線]]
References:
[[@redisQUIT]]
[[@NodeRedis2022]]
[[@liFeatures2022]]