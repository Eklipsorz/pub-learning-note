## 為什麼需要Lua指令碼

**簡而言之：Lua指令碼帶來效能的提升**。

-   很多應用的服務任務包含多步redis操作以及使用多個redis命令，這時你可以使用Redis結合Lua指令碼，會為你的應用帶來更好的效能。
-   另外包含在一個Lua腳本里面的redis命令具備原子性，當你面對高併發場景下的redis資料庫操作時，可以有效避免多執行緒操作產生髒資料。



https://www.gushiciku.cn/pl/gcaZ/zh-tw



redis在2.6开始加入了lua脚本，使用lua脚本有如下好处:

-   **减少网络开销**。复合操作需要向Redis发送多次请求，如上例，而是用脚本功能完成同样的操作只需要发送一个请求即可，减少了网络往返时延。
-   **原子操作**。Redis会将整个脚本作为一个整体执行，中间不会被其他命令插入。换句话说在编写脚本的过程中无需担心会出现竞态条件，也就无需使用事务。事务可以完成的所有功能都可以用脚本来实现
-   **复用**。客户端发送的脚本会永久存储在Redis中，这就意味着其他客户端（可以是其他语言开发的项目）可以复用这一脚本而不需要使用代码完成同样的逻辑

  
  
作者：夏天嘚花花  
链接：https://www.jianshu.com/p/14f9c56ac874  
来源：简书  
著作权归作者所有。商业转载请联系作者获得授权，非商业转载请注明出处。

##### 在redis客户端里面执行lua命令

**EVAL命令**  
格式  
注意点: 这个keys的个数不能省略，假如没有KEYS入参数，要将他设置成0

```ruby
127.0.0.1:6379> eval "要执行的lua命令" key的个数 [KEYS[1]...] [AVRG[1]...]
例子
127.0.0.1:6379> eval "return redis.call('SET',KEYS[1],ARGV[1])" 1 foo bar
OK
127.0.0.1:6379> eval "return redis.call('SET','name','gulugulu')" #没有写key个数，程序报错
(error) ERR wrong number of arguments for 'eval' command
127.0.0.1:6379> eval "return redis.call('SET','name','gulugulu')" 0
OK

```

例子1：執行redis 的set 指令，並設定兩個參數名稱分別為KEYS[\1]、ARGV[\1]，後面的數字是指定要傳入多少個KEY，在這裡只有設定foo->bar，所以為1個，接著將foo放入KEYS陣列的第一個元素，再將bar放入ARGV陣列的第一個元素
```
127.0.0.1:6379> eval "return redis.call('SET',KEYS[1],ARGV[1])" 1 foo bar
```


例子3：沒設定參數，直接以常數來設定，那麼就設定要放入指令的參數為0
```
127.0.0.1:6379> eval "return redis.call('SET','name','gulugulu')" 0
OK
```



https://www.freecodecamp.org/news/a-quick-guide-to-redis-lua-scripting/