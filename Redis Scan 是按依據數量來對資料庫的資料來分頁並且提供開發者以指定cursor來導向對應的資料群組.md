
## 描述

### 為何需要Scan指令
由於[[Redis KEYS 指令的缺點主要有沒分頁、資料越多成本越高的O(n)、前兩者導致的阻塞問題]]

### 解法
> **因此为了解决这一点，Redis在2.8版本的时候提出了一个scan命令，主要用于解决keys命令可能导致整个Redis实例停顿的问题。**

> **scan是一种迭代命令，主要是对keys命令进行了分解，即原本使用一个keys请求一次匹配获取所有符合的key的操作，分解了多次scan操作。每次scan操作返回匹配的key的一个子集，这样每个scan请求的操作时间很短，多次scan请求之间可以执行其他命令，故减少对其他命令执行的阻塞。当最后一个scan请求发现没有数据可返回了，则操作完成，汇总该次所有scan请求的数据，从而达到与keys命令一次获取的数据相同。**

> **由于scan命令需要执行多次，即相当于执行了多个命令，存在多次命令请求和响应周期，故整体执行时间可能要比keys命令长。**

引用[[@redisSCAN]]所描述的：
> SCAN is a cursor based iterator. This means that at every call of the command, the server returns an updated cursor that the user needs to use as the cursor argument in the next call.

> An iteration starts when the cursor is set to 0, and terminates when the cursor returned by the server is 0. The following is an example of SCAN iteration:

```
redis 127.0.0.1:6379> scan 0
1) "17"
2)  1) "key:12"
    2) "key:8"
    3) "key:4"
    4) "key:14"
    5) "key:16"
    6) "key:17"
    7) "key:15"
    8) "key:10"
    9) "key:3"
   10) "key:7"
   11) "key:1"
redis 127.0.0.1:6379> scan 17
1) "0"
2) 1) "key:5"
   2) "key:18"
   3) "key:0"
   4) "key:2"
   5) "key:19"
   6) "key:13"
   7) "key:6"
   8) "key:9"
   9) "key:11"
```



> In the example above, the first call uses zero as a cursor, to start the iteration. The second call uses the cursor returned by the previous call as the first element of the reply, that is, 17.

> As you can see the **SCAN return value** is an array of two values: the first value is the new cursor to use in the next call, the second value is an array of elements.




## 描述

## 複習
#🧠 Question :: ->->-> ``

---
Status: #🌱 
Tags:
[[Redis]] - [[Databse]]
Links:
[[Database Cursor 會使用Shared Lock來將要給開發者存取的資料集合鎖死，以避免被人修改]]
[[Database Cursor 是一個將連續資料按照指定數量來分群組，並透過群組名稱來滑動資料來改變顯示資料的元件]]
[[Redis KEYS 指令的缺點主要有沒分頁、資料越多成本越高的O(n)、前兩者導致的阻塞問題]]
[[Redis KEYS 可以使用表達式來找到符合表達式的key]]
References:

[[@redisSCAN]]
[[@RedisZhongYouBiaoDieDaiQiScanGuMingDiPen]]