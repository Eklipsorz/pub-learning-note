

## Client + Cache + DB 策略
- 以結構來分類的策略
[[inline Caching 是客戶端直接以cache為主要儲存系統的風格 ，Look-Aside Caching 則是先以cache來處理，再來以DB作處理的風格]]

- 以讀法來分類的的策略
[[cache hit為主的方法是從緩存存取資料但很容易被人忽略同步問題，cache miss為主的方法是從資料庫讀取資料但能選擇同步]]

 - 以寫法來分類的的策略
 [[以write-hit為主的write through和write back(write behind)這兩種寫入策略通常會為了一致性而與資料庫同步資料]]