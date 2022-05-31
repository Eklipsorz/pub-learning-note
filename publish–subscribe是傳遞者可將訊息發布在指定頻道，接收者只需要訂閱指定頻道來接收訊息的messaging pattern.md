引用[[@wikidataPublishSubscribePattern2022]]所描述：
> **publish–subscribe** is a [messaging pattern](https://en.wikipedia.org/wiki/Messaging_pattern "Messaging pattern") where senders of [messages](https://en.wikipedia.org/wiki/Message_passing "Message passing"), called publishers, do not program the messages to be sent directly to specific receivers, called subscribers, but instead categorize published messages into classes without knowledge of which subscribers, if any, there may be. Similarly, subscribers express interest in one or more classes and only receive messages that are of interest, without knowledge of which publishers, if any, there are.

重點：
- publish-subscibe 是指兩個程式模組如何連接和交流的messaging pattern
- publish-subscribe 中會將傳遞者為發表(傳遞)訊息的publisher，而接收者為接收訊息的subscribe，傳遞者和接收者會透過頻道(channel)來傳遞和接收
- 傳遞者只需要將訊息放置特定頻道，而接收者只需要訂閱特定頻道就能接收該頻道存放的訊息，如下圖
![](https://i.morioh.com/b6c9d9a00e.png)

---
Status: #📥 
Tags:
[[Message]] - [[Subscribe & Publish]]
Links:
[[messaging pattern 是定義兩個程式模組如何連接和交流的風格]]
References:
[[@wikidataPublishSubscribePattern2022]]