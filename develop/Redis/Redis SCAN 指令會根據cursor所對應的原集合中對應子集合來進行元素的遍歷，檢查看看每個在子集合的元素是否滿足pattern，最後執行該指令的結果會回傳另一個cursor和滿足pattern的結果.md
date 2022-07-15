




## 描述

> While `SCAN` does not provide guarantees about the number of elements returned at every iteration, it is possible to empirically adjust the behavior of `SCAN` using the **COUNT** option. Basically with COUNT the user specified the _amount of work that should be done at every call in order to retrieve elements from the collection_. This is **just a hint** for the implementation, however generally speaking this is what you could expect most of the times from the implementation.

重點：
- Redis Scan Cursor 指令如下，每當被執行時，就會從原集合(KEY集合)中挑選cursor對應的索引值來取得COUNT個元素當作子集合，然後對子集合的每個元素進行遍歷，然後逐個查看元素是否滿足pattern，若滿足的話，本次迭代就會紀錄其元素，若沒滿足的話，就會跳過，直到遍歷完畢之後。

```
SCAN <cursor> MATCH <pattern> COUNT <count>
```

- 具體會回傳兩個元素分別為：
	-  cursor：另一個cursor，但具體會對應的索引值會是 原集合中的當前cursor 對應的索引值 + COUNT
	-  當前目前子集合的遍歷所滿足pattern的元素有哪些，以陣列來表示

> SCAN, SSCAN, HSCAN and ZSCAN return a two elements multi-bulk reply, where the first element is a string representing an unsigned 64 bit number (the cursor), and the second element is a multi-bulk with an array of elements.

- 若cursor 對應的索引值算法是依據特定算法而算出來的

[[@bondarenkoAnswerRedisHow2015]] 
- 若cursor 為0的話，那麼對應的索引值即為原集合的索引
### 範例
假設key集合有，那麼SCAN切割出來的子任務有五個或者說SCAN會執行五次迭代，每個任務都從集合來拿一個key，每次拿的key皆為不同，任務1會拿到key1，任務2會拿到key2，任務3會拿到key3，任務4會拿到key4，任務5會拿到key5，
```
key1
key2
key3
key4
key5
```

每個任務都會從pattern來比對拿到的key是否相符，結果任務3拿到的key相符，那麼每個任務的結果會是
```
// 任務1
empty
// 任務2
empty
// 任務3
key3
// 任務4
empty
// 任務5
empty
```


## 複習

#🧠  當Redis 伺服器執行 SCAN cursor 指令時，會如何執行？->->-> `每當被執行時，就會從原集合(KEY集合)中挑選cursor對應的索引值來取得COUNT個元素當作子集合，然後對子集合的每個元素進行遍歷，然後逐個查看元素是否滿足pattern，若滿足的話，本次迭代就會紀錄其元素，若沒滿足的話，就會跳過，直到遍歷完畢之後。`

#🧠 當Redis 伺服器執行 SCAN cursor 指令後的回應結果會是什麼？ ->->-> `具體會回傳兩個元素分別為： -  cursor：另一個cursor，但具體會對應的索引值會是 原集合中的當前cursor 對應的索引值 + COUNT -  當前目前子集合的遍歷所滿足pattern的元素有哪些，以陣列來表示`

#🧠 當Redis 伺服器執行 SCAN cursor ->->-> ``



#🧠 Redis SCAN 每個子任務會如何從集合取出資料？如何處理？結果會是什麼？舉一個例子，以五個SCAN子任務為例 ->->-> `Redis SCAN 所切割出來的子任務會被分配key集合的不同部分，然後按照pattern來篩選出滿足的key，其處理結果會包含著未滿足和滿足的。 每個任務都從集合來拿一個key，每次拿的key皆為不同，任務1會拿到key1，任務2會拿到key2，任務3會拿到key3，任務4會拿到key4，任務5會拿到key5，每個任務都會從pattern來比對拿到的key是否相符，結果任務3拿到的key相符，那麼每個任務的結果會是只有任務3有結果，其餘皆沒有結果`
<!--SR:!2022-07-20,26,250-->

#🧠  Redis SCAN COUNT參數是做什麼用 ->->-> `參數是用來指定每一次呼叫從key 集合獲取的key數量，也就是每個呼叫所要負責比對的key數量`
<!--SR:!2022-07-22,28,250-->

---
Status: #🌱 
Tags:
[[Redis]] - [[Database]]
Links:
[[Redis Scan 是按依據數量來對資料庫的資料來分頁並且提供開發者以指定cursor來導向對應的資料群組]]
References:
[[@redisSCAN]]
[[@bondarenkoAnswerRedisHow2015]]