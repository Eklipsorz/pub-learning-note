## 描述
> 為什麼redis可以實現分散式鎖呢？
> 我們以購票舉例，購票視窗前的這個鎖，是每位旅客都可以看到的。
> 這裡我們可以得出一個結論，一把鎖首先要具有的屬性是：想要獲得鎖的人都可以看到。


https://zhuanlan.zhihu.com/p/93460690

> ### **上锁**

> 上锁的第一步就是先通过 setnx 命令占坑，为了防止死锁，通常在占坑之后还会设置一个过期时间 expire，如下所示：

```text
setnx key value
expire key seconds
```

> 以上命令不是一个原子性操作，所谓原子性操作是指命令在执行过程中并不会被其它的线程或者请求打断，以上如果 setnx 执行成功之后，出现网络闪断 expire 命令便不会得到执行，会导致死锁出现。

> 也许你会想到使用事物来解决，但是事物有个特点，要么成功要么失败，都是一口气执行完成的，在我们上面的例子中，expire 是需要先根据 setnx 的结果来判断是否需要进行设置，显然事物在这里是行不通的，社区也有很多库来解决这个问题，现在 Redis 官方 2.8 版本之后支持 set 命令传入 setnx、expire 扩展参数，这样就可以一条命令一口气执行，避免了上面的问题，如下所示：

> -   value：建议设置为一个随机值，在释放锁的时候会进一步讲解
> -   EX seconds：设置的过期时间
> -   PX milliseconds：也是设置过期时间，单位不一样
> -   NX|XX：NX 同 setnx 效果是一样的

```text
set key value [EX seconds] [PX milliseconds] [NX|XX]
```

重點：
- Redis SET 指令系列本身可以設定key-value pair
- 但是若要以SET指令來上鎖，還需要設定過期時間的指令，為此，以前寫法會是如下：
```
setnx key value
expire key seconds
```
 在Redis上，這兩段指令並不會以transaction或者原子化操作來進行，所以若在第一行執行後，突然被中斷，此時的鎖將會變成因為沒設定過期時間而被鎖死
- 因此Redis在往後版本提供SET指令可以一次設定SET和過期，使兩個指令轉換成一個指令來執行，從而實現原子化
```
set key value [EX seconds] [PX milliseconds] [NX|XX]
```



## 複習


---
Status: 
Tags:
Links:
References:
