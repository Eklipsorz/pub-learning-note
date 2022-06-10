




## 描述

> While `SCAN` does not provide guarantees about the number of elements returned at every iteration, it is possible to empirically adjust the behavior of `SCAN` using the **COUNT** option. Basically with COUNT the user specified the _amount of work that should be done at every call in order to retrieve elements from the collection_. This is **just a hint** for the implementation, however generally speaking this is what you could expect most of the times from the implementation.

重點：
- SCAN不保證每一次迭代都能按照預期那樣得到固定數量的結果
- SCAN COUNT參數是用來指定每一次呼叫從key 集合獲取的key數量，也就是每個呼叫所要負責比對的key數量

## 複習
#🧠 Question :: ->->-> ``

---
Status: 
Tags:
Links:
References:
[[@redisSCAN]]