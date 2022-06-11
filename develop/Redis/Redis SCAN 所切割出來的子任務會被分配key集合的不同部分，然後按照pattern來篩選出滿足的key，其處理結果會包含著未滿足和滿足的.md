




## 描述

> While `SCAN` does not provide guarantees about the number of elements returned at every iteration, it is possible to empirically adjust the behavior of `SCAN` using the **COUNT** option. Basically with COUNT the user specified the _amount of work that should be done at every call in order to retrieve elements from the collection_. This is **just a hint** for the implementation, however generally speaking this is what you could expect most of the times from the implementation.

重點：
- SCAN不保證每一次迭代都能按照預期那樣得到固定數量的結果
- SCAN COUNT參數是用來指定每一次呼叫從key 集合獲取的key數量，也就是每個呼叫所要負責比對的key數量
- COUNT 參數語法，預設會是10
```
SCAN <cursor> MATCH <pattern> COUNT <count>
```


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
#🧠 Redis SCAN 每個子任務會如何從集合取出資料？如何處理？結果會是什麼？舉一個例子，以五個SCAN子任務為例 ->->-> `Redis SCAN 所切割出來的子任務會被分配key集合的不同部分，然後按照pattern來篩選出滿足的key，其處理結果會包含著未滿足和滿足的。 每個任務都從集合來拿一個key，每次拿的key皆為不同，任務1會拿到key1，任務2會拿到key2，任務3會拿到key3，任務4會拿到key4，任務5會拿到key5，每個任務都會從pattern來比對拿到的key是否相符，結果任務3拿到的key相符，那麼每個任務的結果會是只有任務3有結果，其餘皆沒有結果`

#🧠  Redis SCAN COUNT參數是做什麼用 ->->-> `參數是用來指定每一次呼叫從key 集合獲取的key數量，也就是每個呼叫所要負責比對的key數量`

---
Status: #🌱 
Tags:
[[Redis]] - [[Database]]
Links:
[[Redis Scan 是按依據數量來對資料庫的資料來分頁並且提供開發者以指定cursor來導向對應的資料群組]]
References:
[[@redisSCAN]]