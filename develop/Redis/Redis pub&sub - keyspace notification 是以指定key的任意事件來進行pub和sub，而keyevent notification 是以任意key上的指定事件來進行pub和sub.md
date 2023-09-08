
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

Redis 觀測鍵和事件的種類主要分為：
- Key-space notification：以指定key上的任意事件來進行publish 和 subscribe
- Key-event notification：以任意key上的指定事件來進行publish 和 subscribe

內建頻道則會因而分成兩種:
- Key-space notification：在特定key值的任意事件上的事件訊息接收和傳遞
```
// keyspace 頻道會以下列作為其keyspace的prefix，而<db>為redis database name
__keyspace@<db>__
```
- Key-event notification：在發生特定事件的任意key值上的事件訊息接收和傳遞
```
// keyevent 頻道會以下列作為其keyevent的prefix，而<db>為redis database name
__keyevent@<db>__
```



### 舉例

> Keyspace notifications are implemented by sending two distinct types of events for every operation affecting the Redis data space. For instance a [`DEL`](https://redis.io/commands/del) operation targeting the key named `mykey` in database `0` will trigger the delivering of two messages, exactly equivalent to the following two [`PUBLISH`](https://redis.io/commands/publish) commands:

```
PUBLISH __keyspace@0__:mykey del
PUBLISH __keyevent@0__:del mykey
```

重點：
- 當0號資料庫上的mykey 鍵進行DEL處理，redis就會自動傳遞訊息至指定頻道，並且會一次傳遞兩種訊息：
```
// 向__keyspace@0__:mykey頻道 傳遞del這訊息，以此表明mykey這鍵值上出現del事件
PUBLISH __keyspace@0__:mykey del
// 向__keyevent@0__:del 頻道 傳遞mykey，以此表明目前發生del事件的key為mykey
PUBLISH __keyevent@0__:del mykey
```
- 當訂閱以下頻道，就能接收到0號資料庫下所有發生在mykey的事件
```
__keyspace@0__:mykey
```
- 當訂閱以下頻道，就能接收0號資料庫下所有發生del事件的鍵之事件
```
__keyevent@0__:del
```
## 複習

#🧠 Redis Pub/Sub 是什麼樣的機制 ->->-> `是Redis 用來在資料庫上實現key上的事件監聽和事件處理的手段，主要透過資料庫本身會在特定事件下向特定頻道發送(Publish)特定訊息，而使用者只需訂閱該頻道就能接收到訊息，就能夠順勢根據特定事件下的結果來實現事件處理`
<!--SR:!2023-11-16,301,230-->

#🧠  Redis Pub/Sub 這Publish-Subscribe下主要有哪兩個方式來去監測鍵和事件？ ->->-> `Key-space notification：以指定key上的任意事件來進行publish 和 subscribe、Key-event notification：以任意key上的指定事件來進行publish 和 subscribe`
<!--SR:!2023-10-29,110,227-->


#🧠 Redis Pub/Sub 下的 Key-space notification 和 Key-event notification 頻道各是以什麼作為前綴(prefix) ->->-> `__keyspace@<db>__:key 和 __keyevnt@<db>__:event，而<db>為redis database name`
<!--SR:!2024-04-03,267,226-->




#🧠 Redis Pub/Sub 下的 Key-space notification 和 Key-event notification 兩者專注什麼 (任意key？任意事件？)->->-> `前者專注於特定key值的任意事件，後者則是專注於發生特定事件下的任意key值`
<!--SR:!2025-02-15,585,246-->



#🧠 當0號資料庫上的mykey 鍵進行DEL處理，redis就會自動傳遞訊息至指定頻道，並且會一次傳遞兩種訊息，傳遞訊息方式會是PUBLISH \_\_keyspace@0\_\_:mykey del或者PUBLISH \_\_keyevent@0\_\_:del mykey，請解釋這些語法主要做了什麼？ ->->-> `向__keyspace@0__:mykey頻道 傳遞del這訊息，以此表明mykey這鍵值上出現del事件、向__keyevent@0__:del 頻道 傳遞mykey，以此表明目前發生del事件的key為mykey`
<!--SR:!2024-11-28,506,246-->



#🧠 若資料庫發送PUBLISH  \_\_keyspace@0\_\_:mykey del 和PUBLISH \_\_keyevent@0\_\_:del mykey，如何接收對應頻道的del 和 mykey (注意頻道名稱是哪些) ->->-> ` 訂閱名為__keyspace@0__:mykey頻道就能接收del；後者則是訂閱名為__keyevent@0__:del頻道就能接收mykey`
<!--SR:!2024-01-06,120,207-->


---
Status: #🌱 
Tags:
[[Subscribe & Publish]] - [[Redis]]
Links:
[[messaging pattern 是定義兩個程式模組如何連接和交流的風格]]
[[publish–subscribe是傳遞者可將訊息發布在指定頻道，接收者只需要訂閱指定頻道來接收訊息的messaging pattern]]
References:
[[@redisRedisKeyspaceNotifications]]
[[@redisdocJianKongJianTongZhiKeyspaceNotification]]
[[@redisRedisPubSub]]