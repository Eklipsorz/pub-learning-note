## 為什麼需要Lua指令碼





  
  
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