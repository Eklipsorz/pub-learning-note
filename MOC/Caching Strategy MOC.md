

## Client + Cache + DB 策略
- 以結構來分類的策略
[[inline Caching 是客戶端直接以cache為主要儲存系統的風格 ，Look-Aside Caching 則是先以cache來處理，再來以DB作處理的風格]]

- 以讀法來分類的的策略
[[客戶端對緩存發讀需求主要有cache hit為主和cache miss為主這兩種同步資料的策略]]

 - 以寫法來分類的的策略
 [[以write-hit為主要分為write through和write back(write behind)這兩種同步策略]]