## 描述

> ### Write-miss(就是你要更新的東西 不在緩存裡):

> 在這種情況下 客戶直接向DB發寫需求 在這種情況下 客戶直接向緩存發寫需求沒問題

> 更新了DB之後 這時DB就可以選擇同步(Synchronous) 或是不更新緩存 同步的更新叫做Allocate on write 不更新的叫做Write around

### write around

> 寫的latency變小 仰賴Read-miss來更新緩存
> 
> 適合用在你寫完一個數據之後 下一次對於同一個數據的讀不會發生得太快 這樣就適合把latency花在讀


### allocate on write
> 一樣寫進兩個地方 如果下一次對於同一個數據的讀發生得很快 就適合這個

> 其實你仔細想想就知道 這其實跟Write-through是一樣的 都是緩存和DB都更新 差別只是原本緩存有沒有而已

## 複習
#🧠 Question :: ->->-> ``

---
Status: #🌱 
Tags:
[[Caching]] - [[Redis]] - [[Database]]
Links:
[[以write-hit為主的write through和write back(write behind)這兩種寫入策略通常會為了一致性而與資料庫同步資料]]
[[cache hit為主的方法是從緩存存取資料但很容易被人忽略同步問題，cache miss為主的方法是從資料庫讀取資料但能選擇同步]]
[[inline Caching 是客戶端直接以cache為主要儲存系統的風格 ，Look-Aside Caching 則是先以cache來處理，再來以DB作處理的風格]]
References:
[[@cloud-leeCPUCacheYuanLiTanTao]]
[[@jyt0532HuanCunDuXieJiZhiJyt0532Blog]]
