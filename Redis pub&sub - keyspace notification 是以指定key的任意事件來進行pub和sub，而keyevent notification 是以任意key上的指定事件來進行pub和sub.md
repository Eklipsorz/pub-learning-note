
## 描述

根據[[@redisRedisKeyspaceNotifications]]所描述

> Keyspace notifications allow clients to subscribe to Pub/Sub channels in order to receive events affecting the Redis data set in some way.

Keyspace notifications


> Examples of events that can be received are:

> -   All the commands affecting a given key.
> -   All the keys receiving an LPUSH operation.
> -   All the keys expiring in the database 0.

> Note: Redis Pub/Sub is _fire and forget_ that is, if your Pub/Sub client disconnects, and reconnects later, all the events delivered during the time the client was disconnected are lost.


重點：
- Redis 本身有Key-space notification 和 Key-event notification 這兩種Publish-Scbscribe模式
- 在這個機制下的Publisher：使用者可建立指定頻道來傳遞，而Redis會替部分Redis指令添加傳遞訊息至指定頻道
- 在這個機制下的Subscriber：而用者只需要去訂閱特定頻道就即可收到對應頻道的訊息並做些處理，因此可以應用於事件處理
- Redis Pub/Sub 機制會是fire and forget，也就是說訊息只要被發送就會忘了訊息是自己發送，這會導致無法管控訊息，進而降低訊息的可靠性-訊息能夠被正確送達目的地
	- 當訂閱頻道的客戶端突然斷線時，它就會丟失在斷線期間所應該要接收到的訊息

### Redis pub&sub 種類

主要分為：
- Key-space notification：以指定key上的任意事件來進行publish 和 subscribe
- Key-event notification：以任意key上的指定事件來進行publish 和 subscribe


### 舉例

> Keyspace notifications are implemented by sending two distinct types of events for every operation affecting the Redis data space. For instance a [`DEL`](https://redis.io/commands/del) operation targeting the key named `mykey` in database `0` will trigger the delivering of two messages, exactly equivalent to the following two [`PUBLISH`](https://redis.io/commands/publish) commands:

```
PUBLISH __keyspace@0__:mykey del
PUBLISH __keyevent@0__:del mykey
```

重點：
- 當0號資料庫上的mykey 鍵進行DEL處理，redis就會自動傳遞訊息至指定頻道，並且會一次傳遞兩種訊息：
```
// 向__keyspace@0__頻道 傳遞mykey 出現del處理
PUBLISH __keyspace@0__:mykey del
// 向__keyevent@0__頻道 傳遞現在出現del處理的key是 mykey
PUBLISH __keyevent@0__:del mykey
```


订阅第一个频道 `__keyspace@0__:mykey` 可以接收 `0` 号数据库中所有修改键 `mykey` 的事件， 而订阅第二个频道 `__keyevent@0__:del` 则可以接收 `0` 号数据库中所有执行 `del` 命令的键。



> The first channel listens to all the events targeting the key `mykey` and the other channel listens only to `del` operation events on the key `mykey`

> The first kind of event, with `keyspace` prefix in the channel is called a **Key-space notification**, while the second, with the `keyevent` prefix, is called a **Key-event notification**.
> In the previous example a `del` event was generated for the key `mykey` resulting in two messages:

> -   The Key-space channel receives as message the name of the event.
> -   The Key-event channel receives as message the name of the key.

> It is possible to enable only one kind of notification in order to deliver just the subset of events we are interested in.



---
Status: #📥 
Tags:
[[Subscribe & Publish]] - [[Redis]]
Links:
[[messaging pattern 是定義兩個程式模組如何連接和交流的風格]]
[[publish–subscribe是傳遞者可將訊息發布在指定頻道，接收者只需要訂閱指定頻道來接收訊息的messaging pattern]]
References:
[[@redisRedisKeyspaceNotifications]]
[[@redisdocJianKongJianTongZhiKeyspaceNotification]]
[[@redisRedisPubSub]]