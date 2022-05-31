


根據[[@redisRedisKeyspaceNotifications]]所描述

> Keyspace notifications allow clients to subscribe to Pub/Sub channels in order to receive events affecting the Redis data set in some way.

Keyspace notifications


> Examples of events that can be received are:

> -   All the commands affecting a given key.
> -   All the keys receiving an LPUSH operation.
> -   All the keys expiring in the database 0.

> ### Type of events[](https://redis.io/docs/manual/keyspace-notifications/#type-of-events)

> Keyspace notifications are implemented by sending two distinct types of events for every operation affecting the Redis data space. For instance a [`DEL`](https://redis.io/commands/del) operation targeting the key named `mykey` in database `0` will trigger the delivering of two messages, exactly equivalent to the following two [`PUBLISH`](https://redis.io/commands/publish) commands:

```
PUBLISH __keyspace@0__:mykey del
PUBLISH __keyevent@0__:del mykey
```

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

[[@redisRedisPubSub]]