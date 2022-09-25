
## 描述

### 為何需要Scan指令
由於[[Redis KEYS 指令的缺點主要有沒分頁、資料越多成本越高的O(n)、前兩者導致的阻塞問題]]

### 解法


> **因此为了解决这一点，Redis在2.8版本的时候提出了一个scan命令，主要用于解决keys命令可能导致整个Redis实例停顿的问题。**

> **scan是一种迭代命令，主要是对keys命令进行了分解，即原本使用一个keys请求一次匹配获取所有符合的key的操作，分解了多次scan操作。每次scan操作返回匹配的key的一个子集，这样每个scan请求的操作时间很短，多次scan请求之间可以执行其他命令，故减少对其他命令执行的阻塞。当最后一个scan请求发现没有数据可返回了，则操作完成，汇总该次所有scan请求的数据，从而达到与keys命令一次获取的数据相同。**

> **由于scan命令需要执行多次，即相当于执行了多个命令，存在多次命令请求和响应周期，故整体执行时间可能要比keys命令长。**

重點：
- Scan 指令主要解決KEYS的分頁、阻塞問題而提出來，
```
// Queue結構會是如下：當KEYS因為資料太多而執行過慢，會卡住其他指令
KEYS <- Others
```
- Scan 指令會將獲取KEYS的執行拆解成多個獲取KEY的小指令來重新放到Redis的執行佇列中，同時允許其他任務可以在他們之間，每個小指令所要獲取的KEY數就會跟著變少、執行時間也會跟著變短，最後會將子任務的獲取順序來組合組合成一個完整KEYS結果
```
// Queue結構會是如下：執行Scan之前
Scan <- command A <- command B <- command C
// Queue結構會是如下：執行Scan之後，Scan會被拆解成更細小的Scan指令重新放入佇列中執行
Scan1 <- command A <- Scan1 <- command A <- command C <- Scan2 <- Scan3
```
- 每一個小指令會回傳兩個東西：
	- 下一個Cursor號碼(包含對應任務和對應資料集合)
	- 目前小指令所獲取的KEYS
>  As you can see the **SCAN return value** is an array of two values: the first value is the new cursor to use in the next call, the second value is an array of elements.

- 每一個小指令會是Cursor所對應的資料集合，而一開始Cursor=0所對應的資料集合會是最一開始獲取到的KEYS，若小指令回傳下一個Cursor是0的話，代表目前指定的小指令就是最後一個小指令，不會再有其他獲取KEYS的指令 或者 目前所對應的資料集合就是最後一個
>  An iteration starts when the cursor is set to 0, and terminates when the cursor returned by the server is 0.


#### Scan 好處
由於Scan會被拆解小指令，所以會有：
- 分頁化
- 獲取KEYS過程中不會阻塞其他指令

#### Scan 壞處
由於Scan會被拆解小指令，若中間插入其他任務的話，其整體的執行時間可能會比單個獲取KEYS任務還要久

#### Redis Scan 案例
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


重點：
- 一開始會對目前資料中進行Scan，並拆分成兩個子指令-scan，執行完scan 0 就會回傳下一個cursor號碼為17以及目前scan子指令所獲取到的keys
- 接著當scan指定為17時，就表示要求獲取curson所對應的資料集合，也就是原本接續在scan 0所對應的資料集合之後。


## 複習
#🧠 Redis Scan 如何解決Redis KEYS的問題(沒分頁化、會有阻塞的可能) ->->-> `Scan 指令會將獲取KEYS的執行拆解成多個獲取KEY的小指令來重新放到Redis的執行佇列中，同時允許其他任務可以在他們之間，每個小指令所要獲取的KEY數就會跟著變少、執行時間也會跟著變短`
<!--SR:!2022-09-27,73,250-->

#🧠 Redis Scan 若拆分成多個迭代的話，他們是怎麼實現？如何印出他們的處理結果->->-> `每個迭代都會從原本key集合取出特定不重的key子集合來比對迭代所被賦予的pattern是否滿足，滿足的key會記錄起來，最後滿足pattern的key子集合會以cursor來命名，來讓開發者藉由不同cursor來快速找到對應迭代下的處理結果`
<!--SR:!2022-10-29,68,250-->

#🧠 Redis Scan 若拆分成多個迭代的話，會是指什麼？以指令和佇列來說的話 ->->-> `每一個迭代會各為一個指令來放進Queue 來執行`
<!--SR:!2022-10-11,55,250-->


#🧠 Redis Scan 中的每一個Cursor 代表著什麼？(提示：資料？子任務)->->-> `對應的資料集合以及能夠獲取對應集合的子scan任務`
<!--SR:!2023-03-17,175,250-->

#🧠  Redis Scan 語法形式會是什麼 (提示：只需要scan 和 cursor號碼) ->->-> `SCAN <cursor>`
<!--SR:!2023-03-24,180,250-->

#🧠  Redis Scan 語法的回傳結果會是什麼 (提示：有兩個) ->->-> `下一個Cursor號碼(包含對應任務和對應資料集合)、目前小指令所獲取的KEYS或者目前cursor所對應的資料集合`
<!--SR:!2022-09-27,73,250-->

#🧠  Redis Scan 語法為SCAN 0會是什麼意思->->-> `每一個小指令會是Cursor所對應的資料集合，而一開始Cursor=0所對應的資料集合會是最一開始獲取到的KEYS`
<!--SR:!2023-03-03,165,250-->

#🧠  Redis Scan 執行後得到的下一個cursor號碼為0，代表著什麼？->->-> `若小指令回傳下一個Cursor是0的話，代表目前指定的小指令就是最後一個小指令，不會再有其他獲取KEYS的指令 或者 目前所對應的資料集合就是最後一個`
<!--SR:!2022-12-29,125,250-->

#🧠 Redis Scan好處是什麼？ ->->-> `分頁化、獲取KEYS過程中不會阻塞其他指令`
<!--SR:!2022-09-28,74,250-->

#🧠  Redis Scan 壞處是什麼？(提示：記憶體和CPU)->->-> `要多花記憶體成本去儲存過去處理完畢的資料集合、由於Scan會被拆解小指令，若中間插入其他任務的話，其整體的執行時間可能會比單個獲取KEYS任務還要久`
<!--SR:!2023-03-19,175,250-->

---
Status: #🌱 
Tags:
[[Redis]] - [[Database]]
Links:
[[Database Cursor 會使用Shared Lock來將要給開發者存取的資料集合鎖死，以避免被人修改]]
[[Database Cursor 是一個用字串或數字去對應過去處理結果並透過該索引值來將呈現資料導向成對應處理結果之機制]]
[[Redis KEYS 指令的缺點主要有沒分頁、資料越多成本越高的O(n)、前兩者導致的阻塞問題]]
[[Redis KEYS 可以使用表達式來找到符合表達式的key]]
[[Redis SCAN 指令會根據cursor所對應的原集合中對應子集合來進行元素的遍歷，檢查看看每個在子集合的元素是否滿足pattern，最後執行該指令的結果會回傳另一個cursor和滿足pattern的結果]]
References:

[[@redisSCAN]]
[[@RedisZhongYouBiaoDieDaiQiScanGuMingDiPen]]