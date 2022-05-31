> ### ioredis介紹

> ![](http://claire-chang.com/wp-content/uploads/2020/02/ioredis.png)  
> ioredis是一個功能強大的功能強大的Redis客戶，已被世界上最大的在線商務公司阿里巴巴和許多其他了不起的公司所使用。  

> -   功能齊全。它支持Cluster，Sentinel，Pipelining，當然還支持Lua腳本和Pub / Sub（具有二進制消息的支持）。
> -   高性能。
> -   令人愉快的API。它與Node回調和本機Promise一起使用。
> -   命令參數和答复的轉換。
> -   ansparent key prefixing
> -   Lua腳本的抽象，允許您定義自定義命令。
> -   支持二進制數據。
> -   支持TLS。
> -   Support for offline queue and ready checking
> -   支持 ES6 類型, 如: `Map` and `Set`
> -   支持GEO命令（Redis 3.2不穩定）。
> -   複雜的錯誤處理策略。
> -   支持NAT映射。


老牌的redis client - node redis本身有版本上的相容性問題，且後面沒金主可以支持開發者，因此轉而使用ioredis