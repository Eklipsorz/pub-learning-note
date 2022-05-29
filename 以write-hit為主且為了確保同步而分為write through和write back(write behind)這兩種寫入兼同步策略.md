## 描述
引用[[@jyt0532HuanCunDuXieJiZhiJyt0532Blog]]所描述的：
>  ### Write-hit(就是你要更新的東西 也在緩存裡):
>  在這種情況下，客戶直接向緩存發寫需求沒問題，看是寫新資料或是更新舊資料都可以，更新了緩存之後 這時緩存就可以選擇同步(Synchronous) 或是非同步的(Asynchronous)更新DB 同步的更新叫做Write through 非同步的叫做Write back或是Write behind

重點：是以緩存(Cache/Memory)、資料庫(Disk)、客戶端(CPU)為主
- write hit 在這裡是指客戶端能夠在緩存寫入或者客戶端要更改的資料是在緩存
- 由於能夠在緩存進行寫入資料，這代表著緩存的資料是比資料庫的資料還新的，可選擇同步資料庫或者不同步，若不同步的話，只要當緩存崩潰時，整份資料將會永久性遺失；若同步的話，資料不至於會面臨到永久性遺失
- 不過通常會選擇同步，而通常會有兩個寫入兼同步策略：
	- write-through
	- write-back (behind)

### write-through 
引用[[@jyt0532HuanCunDuXieJiZhiJyt0532Blog]]所描述的：
> #### Write through優缺點
> 每次寫入都同時修改緩存跟DB，當然優點就是一致性得以滿足
> 缺點就是慢，因為要寫兩個地方(比沒有緩存還慢)
> 使用時機就是當你寫完一個數據後，下次讀會發生的很快很多次，這樣就適合把latency花在寫

![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1653832279/blog/database/caching/Write-Through-Diagram_xacorf.png)

![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1653832279/blog/database/caching/Write-Through-Steps_atyh3p.png)

### write-back
引用[[@jyt0532HuanCunDuXieJiZhiJyt0532Blog]]所描述的：
> 寫入緩存後就回傳給客戶 我之後**有空**的時候再慢慢修改DB 保証了write lantency的下降

> Note: 通常大家都很忙 沒什麼空 但是修改DB的死線是cache的那個entry要被evict的時候 最起碼在那個時候 你要寫回DB 在那之前的cache hit都可以直接回傳

> 所以實作起來 每一個緩存的entry都要有一個dirty bit. 只要你修改過這個值 dirty bit就要設成true 等到evict的時候 如果dirty bit是true就要更新DB

> 但缺點也很明顯 通常DB的recover機制非常健全但緩存沒有太多recover機制 要是你的cache當機或是跳電 你的某些只寫在緩存而不在DB的資料就永遠消失了

> 使用時機就是讀寫發生的很平均 Write back機制讓讀寫都不會latency太高 但是要小心Crash的問題




### note
引用[[@cloud-leeCPUCacheYuanLiTanTao]]所描述的 write hit & write miss 概念：
> ### [](https://hackmd.io/@drwQtdGASN2n-vt_4poKnw/H1U6NgK3Z?type=view#44-When-CPU-Wants-to-Write "44-When-CPU-Wants-to-Write")4.4 When CPU Wants to Write
>-   如果在 Cache 裡可以找到想要寫入的資料位置 -> **Write Hit**
>-   相反的，如果找不到 -> **Write Miss**


write hit 和 write miss 原理源自於CPU要寫入的位置或者要變更的資料是否源自於緩存(cache)：
1. hit 和 miss 是指的是CPU能夠寫入資料至緩存 和 CPU不能夠寫入資料至資料，等同於失去(miss)儲存緩存的機會
2. write hit：若CPU能夠在緩存找到的資料來更改或者能夠在緩存寫入(考慮緩存是否還有空間能夠寫)，那就表示write hit
3. write miss：若CPU不能夠在緩存找到的資料來更改或者不能夠在緩存寫入(考慮緩存是否還有空間能夠寫)，那就表示write miss


## 複習
#🧠 write hit 和 write miss 的 hit 和 miss 是指？ ->->-> `hit 和 miss 是指的是CPU能夠寫入資料至緩存 和 CPU不能夠寫入資料至資料，等同於失去(miss)儲存緩存的機會`

#🧠 write hit 和 write miss 原理源自於？請盡可能考量到空間是否還能夠存->->-> `CPU要寫入的位置是否還能夠在緩存寫或者要變更的資料是否源自於緩存(cache)，前者要考量緩存還有空間存，後者要考量變更的資料位置`


---
Status: #🌱 
Tags:
[[Caching]] - [[Redis]] - [[Database]]
Links:
[[客戶端對緩存發讀需求主要有cache hit為主和cache miss為主這兩種讀取策略]]
[[inline Caching 是客戶端直接以cache為主要儲存系統的風格 ，Look-Aside Caching 則是先以cache來處理，再來以DB作處理的風格]]
References:
[[@cloud-leeCPUCacheYuanLiTanTao]]
[[@jyt0532HuanCunDuXieJiZhiJyt0532Blog]]
