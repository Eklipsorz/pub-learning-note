## 描述



### redis 官方頂多有kill 和 quit

引用 [[@redisQUIT]] 所描述的quit：
> Ask the server to close the connection. The connection is closed as soon as all pending replies have been written to the client

重點：
- quit()會替客戶端向伺服器發出斷線請求，並於斷線前將目前接收到的請求先完成一遍且不再接收任何請求，只要一執行完畢就直接斷線
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

重點

### 在ioredis上的函式
引用[[@liFeatures2022]]所描述
> By default, ioredis will try to reconnect when the connection to Redis is lost except when the connection is closed manually by `redis.disconnect()` or `redis.quit()`.

## 複習
#🧠 Question :: ->->-> ``

---
Status: #🌱 
Tags:
[[Redis]] - [[Redis Client]]
Links:
References:
[[@redisQUIT]]
[[@NodeRedis2022]]
[[@liFeatures2022]]