## 描述

引用[[@wikidataPublishSubscribePattern2022]]所描述：
> **publish–subscribe** is a [messaging pattern](https://en.wikipedia.org/wiki/Messaging_pattern "Messaging pattern") where senders of [messages](https://en.wikipedia.org/wiki/Message_passing "Message passing"), called publishers, do not program the messages to be sent directly to specific receivers, called subscribers, but instead categorize published messages into classes without knowledge of which subscribers, if any, there may be. Similarly, subscribers express interest in one or more classes and only receive messages that are of interest, without knowledge of which publishers, if any, there are.

重點：
- publish-subscribe 是指兩個程式模組如何連接和交流的messaging pattern
- publish-subscribe 中會將傳遞者為發表(傳遞)訊息的publisher，而接收者為接收訊息的subscribe，傳遞者和接收者會透過頻道(channel)來傳遞和接收
- 傳遞者只需要將訊息放置特定頻道，而接收者只需要訂閱特定頻道就能接收該頻道存放的訊息，如下圖
![](https://i.morioh.com/b6c9d9a00e.png)


## 複習
#🧠 publish-subscribe 是什麼樣的messaging pattern? ->->-> `publish-subscribe 中會將傳遞者為發表(傳遞)訊息的publisher，而接收者為接收訊息的subscribe，傳遞者和接收者會透過頻道(channel)來傳遞和接收， 傳遞者只需要將訊息放置特定頻道，而接收者只需要訂閱特定頻道就能接收該頻道存放的訊息`
<!--SR:!2022-07-12,28,250-->

#🧠 在publish-subscribe模式中，請問Publisher 要如何傳遞訊息至Subscriber，另外也定義一下Publisher 和 Subscriber 誰是sender和receiver ![](https://i.morioh.com/b6c9d9a00e.png) ->->-> `Publisher 是傳遞訊息至receiver的sender，而Subscriber則是接收自sender傳遞過來的訊息之receviver，Publisher 只需要將訊息傳遞至特定頻道，而接收者就從眾多頻道中挑選出想要接收的頻道，就即可收到對應頻道內所拿到的訊息。`
<!--SR:!2022-07-14,28,250-->



---
Status: #🌱 
Tags:
[[Message]] - [[Subscribe & Publish]]
Links:
[[messaging pattern 是定義兩個程式模組如何連接和交流的風格]]
References:
[[@wikidataPublishSubscribePattern2022]]