## 描述
引用[[@jyt0532HuanCunDuXieJiZhiJyt0532Blog]]所描述的：
>  ### Write-hit(就是你要更新的東西 也在緩存裡):
>  在這種情況下，客戶直接向緩存發寫需求沒問題，看是寫新資料或是更新舊資料都可以，更新了緩存之後 這時緩存就可以選擇同步(Synchronous) 或是非同步的(Asynchronous)更新DB 同步的更新叫做Write through 非同步的叫做Write back或是Write behind
### write-through caching
引用[[@jyt0532HuanCunDuXieJiZhiJyt0532Blog]]所描述的：
> #### Write through優缺點
> 每次寫入都同時修改緩存跟DB，當然優點就是一致性得以滿足
> 缺點就是慢，因為要寫兩個地方(比沒有緩存還慢)
> 使用時機就是當你寫完一個數據後，下次讀會發生的很快很多次，這樣就適合把latency花在寫


### write-back caching
引用[[@jyt0532HuanCunDuXieJiZhiJyt0532Blog]]所描述的：
> 寫入緩存後就回傳給客戶 我之後**有空**的時候再慢慢修改DB 保証了write lantency的下降

> Note: 通常大家都很忙 沒什麼空 但是修改DB的死線是cache的那個entry要被evict的時候 最起碼在那個時候 你要寫回DB 在那之前的cache hit都可以直接回傳

> 所以實作起來 每一個緩存的entry都要有一個dirty bit. 只要你修改過這個值 dirty bit就要設成true 等到evict的時候 如果dirty bit是true就要更新DB

> 但缺點也很明顯 通常DB的recover機制非常健全但緩存沒有太多recover機制 要是你的cache當機或是跳電 你的某些只寫在緩存而不在DB的資料就永遠消失了

> 使用時機就是讀寫發生的很平均 Write back機制讓讀寫都不會latency太高 但是要小心Crash的問題

## 複習
#🧠 Question :: ->->-> ``

---
Status: #🌱 
Tags:
[[Caching]] - [[Redis]] - [[Database]]
Links:
[[客戶端對緩存發讀需求主要有cache hit為主和cache miss為主這兩種策略]]
[[inline Caching 是客戶端直接以cache為主要儲存系統的風格 ，Look-Aside Caching 則是先以cache來處理，再來以DB作處理的風格]]
References:
[[@jyt0532HuanCunDuXieJiZhiJyt0532Blog]]