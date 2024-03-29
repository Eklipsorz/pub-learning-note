## 描述


引用[[@jyt0532HuanCunDuXieJiZhiJyt0532Blog]]所描述的策略：
> 客戶直接向緩存發讀需求
> cache hit(就是東西在cache): 那就直接回傳 皆大歡喜
> cache miss: 分兩種
> - Read through: cache負責跟DB要正確的資料 **寫進cache**之後 再回傳給客戶
> - Read aside: 那客戶負責跟DB要正確的資料 要到之後呢 可以叫客戶去更新緩存(Demand-fill)
> 如果你想減少一些讀的latency 也可以建個Kafka 讓緩存subscribe一個Kafka topic 只要有讀request到DB DB就publish這個讀的內容 緩存收到後自己更新

重點：假設環境有客戶端、緩存、資料庫
- 以Cache hit 為主：當客戶端要找的東西A就在緩存，就直接回傳處於緩存中的東西A，通常很容易忽略掉資料庫的資料同步需求，出現以下異常現象：
	-  **緩存的資料是舊的，資料庫的資料是新，而客戶端只會存取緩存舊資料** 
	-  **緩存的資料是新的，資料庫的資料是舊的**
- 以Cache miss 為主：當客戶端要的東西A在緩存裡找不到，就會去資料庫裡找，而這表示緩存資料不是最新的，通常可以選擇是否讓緩存與資料庫保持同步，若不同步的話，總會花更多時間去資料庫尋找資料；若同步的話，總會有提升效能的機會。
- 無論是否同步，Cache miss為主的讀取策略主要會有：
	- Read Through
	- Read Aside

### Read Through
Read Through ：如同字面上的意思，讀取會穿過緩存來進行，首先，客戶端會向緩存系統從緩存找東西，但找不到，由緩存系統負責向資料庫索要東西A，緩存系統會將找到的資料寫進緩存，並通知客戶端來讀取


#### 若緩存選擇回寫資料至緩存
在這裏假定寫定緩存，然後再回傳緩存中的東西A，這樣過程會像是下圖這樣，透過(穿過緩存)來存取東西A：
	![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1653765958/blog/database/caching/Read-Through-Diagram_w98usw.png)
Read Through 步驟：
- 步驟1 是客戶端向緩存系統索要東西A讀取，但緩存系統那邊沒有
- 步驟2 緩存系統由於沒有東西A，緩存就向資料庫索要東西A，並從那獲得
- 步驟3 緩存將獲取到的東西A寫入至緩存，並回傳該東西A給客戶端或者通知客戶端存取
	![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1653765958/blog/database/caching/Read-Through-Steps_zyjmyk.png)
	
### Read Through 和 Read Aside差別

[[@itrendeyitianHuanCunDeWuZhongSheJiMoShiMeiRiTouTiao]]描述：
> Read-Through 的方式與 Cache-Aside 的方式很接近，區別在於，Cache-Aside 是通過應用程式來更新緩存中的數據，而 Read-Through 則是通過緩存自身來更新數據，也就是說應用和資料庫之間不直接進行連接。  
  
  重點：
  - Read Through 和 Read Aside 共同點是在於兩者都是在cache miss情況下而跑去讀取資料庫
  - Read Through 和 Read Aside 差別是在於後者是客戶端通過存取資料庫的資料，來同步緩存資料，前者則是因爲客戶端向緩存索要，但它沒有，所以只好由緩存自己向資料庫索要資料來同步緩存，接著回傳給客戶端

	
### Read Aside
Read Aside：如同字面上的意思，讀取不到東西就往另一邊讀取，在這裡會優先讀取一旁的緩存，接著找不到東西再從資料庫找，首先，客戶端會負責向緩存索要東西A，但找不到，所以再由客戶端向另一邊的資料庫找東西A，找到東西A後，就由客戶端來決定是否將東西A寫入至緩存，這裏假定是客戶端是決定回寫，過程就如下圖這樣，就先往一邊找，找不到就往另一邊找：
	![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1653767516/blog/database/caching/Read-Aside-Diagram_koz5ym.png)
	
Read Aside 步驟：在這裡是假定客戶端是決定將資料庫的資料回寫至緩存。
- 步驟1 是客戶端向緩存索要東西A讀取，但緩存沒有
- 步驟2 緩存由於沒有東西A，客戶端就向資料庫索要東西A，並從那獲得
- 步驟3 客戶端將獲取到的東西A寫入至緩存，以便未來客戶端直接向緩存尋找增加效率。
	![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1653767516/blog/database/caching/Read-Aside-Steps_fmb5p7.png)
	
### note
cache hit 和 cache miss 原為CPU對於緩存能不能找到想要東西的用語：
- cache是指緩存儲存(讀取)這行為，hit和miss則是分別指命中或者落空，合併在一起就是緩存儲存命中到和緩存儲存落空，更通俗點cache hit就是指緩存儲存成功，cache miss是指緩存儲存失敗
- 若CPU想要存取的東西就在緩存找到，代表緩存有命中到或者意謂著緩存系統有成功儲存到CPU想要的東西
- 若CPU想要存取的東西在緩存裡找不到，就代表著緩存落空或者意味著緩存系統沒成功儲存到CPU想要的東西。
- 另外設計者也預期系統能夠優先從最近最快速的儲存空間-緩存來讀取資料，若無法做到，就預期落空；若做到，就預期命中

在這裡是將CPU比喻成客戶端來表示，緩存會是以用記憶體為主的資料庫，而硬碟會是以硬碟為主的資料庫：
1. cache hit: 當客戶端能夠從緩存找到想要的東西，就表示cache hit
2. cache miss：當客戶端不能夠從緩存找到想要的東西，就表示cache miss

## 複習



#🧠 Cache hit & Cache miss: Read Aside 原意是什麼？ (提示：當讀取不到東西的話，旁邊還有東西可以讀，那你會怎麼做？)->->-> `當讀取不到就讀取另一邊東西`
<!--SR:!2025-04-11,610,244-->

#🧠 Cache hit 和 Cache miss在設計者的預期會是如何？ ->->-> `另外設計者也預期系統能夠優先從最近最快速的儲存空間-緩存來讀取資料，若無法做到，就預期落空；若做到，就預期命中`
<!--SR:!2025-02-08,582,245-->

#🧠 以Cache hit 為主的讀取策略容易忽略掉什麼樣的問題(提示：通常都只想著先拿著資料) ->->-> `Cache hit就表示緩存出現著客戶端想要讀取的資料，但這並不表示這資料會與資料庫的資料是一致的，所以會容易出現 **緩存的資料是舊的，資料庫的資料是新，而客戶端只會存取緩存上的舊資料** 以及 **緩存是新的，資料庫是舊的**等異常現象`
<!--SR:!2023-10-04,280,230-->

#🧠  以Cache miss 為主的讀取策略需要考量到什麼? (提示：客戶端讀取的效率)->->-> `Cache miss就表示資料庫的資料是比緩存還新的，這時會有面臨到若一直往資料庫存取，會有效能下降的問題，因此會選擇將資料庫的資料同步在緩存以增加效能`
<!--SR:!2023-11-04,244,210-->

#🧠 Cache 讀取策略：Read Aside 中是否能讓客戶端選擇回寫資料至緩存或者不回寫->->-> `理論上，Read Aside是可以讓客戶端有選擇去回寫資料至緩存，畢竟都用上緩存且資料庫的資料是最新`
<!--SR:!2025-04-18,616,245-->

#🧠 Cache 讀取策略 Read Aside 中原本有給客戶端選擇回寫資料至緩存或者不回寫，那麼若選擇不回寫，會發生什麼樣的結果->->-> `若選擇不回寫的話，客戶端會一直犧牲效能來讀取資料庫`
<!--SR:!2024-08-05,476,245-->

#🧠 Cache 讀取策略 Read Aside 中原本有給客戶端選擇回寫資料至緩存或者不回寫，那麼若選擇回寫，會發生什麼樣的結果->->-> `若選擇回寫的話，客戶端就有提升效能的機會來讀取緩存`
<!--SR:!2025-04-21,620,245-->

#🧠 cache hit 和 cache miss 命名緣由是什麼？分別是什麼意思->->-> `cache是指緩存儲存這行為，hit和miss則是分別指命中或者落空，合併在一起就是緩存儲存命中到和緩存儲存落空，更通俗點cache hit就是指緩存儲存成功，cache miss是指緩存儲存失敗，若CPU想要存取的東西就在緩存找到，代表緩存有命中到或者意謂著緩存系統有成功儲存到CPU想要的東西；若CPU想要存取的東西在緩存裡找不到，就代表著緩存落空或者意味著緩存系統沒成功儲存到CPU想要的東西`
<!--SR:!2024-12-27,554,245-->

#🧠 以Cache hit 為主的讀取策略會是什麼(提示：就如同我要吃東西，就要打開裝滿食物的箱子，接著會做？？)->->-> `當客戶端要找的東西A就在緩存，就直接回傳處於緩存中的東西A。`
<!--SR:!2023-10-26,310,250-->

#🧠 以Cache miss 為主的讀取策略，若假定不會為了同步而回寫資料至緩存，其結果會是？(提示：效能、高負載下的硬碟和記憶體)->->-> `那麼客戶端就會一直讀取資料庫而使效能下降、讀寫會因硬碟存取不快而無法在高負載的情況下維持資料上的一致性`
<!--SR:!2023-11-18,254,190-->

#🧠 無論是否同步，以Cache miss 為主的讀取策略會是什麼？ ->->-> `Read Through ：如同字面上的意思，讀取會穿過緩存來進行，首先，客戶端會向緩存找東西，但找不到，所以由緩存負責向資料庫索要東西A，找到後，緩存就有選擇是否就寫進緩存，無論是否同步，緩存都會回傳東西A至客戶端，Read Aside：如同字面上的意思，讀取會先讀取一旁的緩存，接著再從資料庫找，首先，客戶端會負責向緩存索要東西A，但找不到，所以再由客戶端向另一邊的資料庫找東西A，找到東西A。`
<!--SR:!2023-12-22,345,250-->


#🧠 Caching 讀取策略：Read Through步驟是什麼？以這圖來說明	![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1653765958/blog/database/caching/Read-Through-Steps_zyjmyk.png)  ->->-> `	步驟1 是客戶端向緩存索要東西A讀取，但緩存沒有，步驟2 緩存由於沒有東西A，緩存就向資料庫索要東西A，並從那獲得，步驟3 緩存將獲取到的東西A寫入至緩存，以便未來客戶端直接向緩存尋找增加效率。`
<!--SR:!2024-12-22,500,242-->


#🧠 Caching 讀取策略：Read Aside步驟是什麼？這裏假定客戶端決定回寫，以這圖來說明![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1653767516/blog/database/caching/Read-Aside-Diagram_koz5ym.png)->->-> `	步驟1 是客戶端向緩存索要東西A讀取，但緩存沒有，步驟2 緩存由於沒有東西A，客戶端就向資料庫索要東西A，並從那獲得，步驟3 客戶端將獲取到的東西A寫入至緩存，以便未來客戶端直接向緩存尋找增加效率。`
<!--SR:!2025-01-05,507,242-->


#🧠 以Cache miss為主的同步方式：Read Through 和 Read Aside兩者間的共同點為？->->-> `Read Through 和 Read Aside 共同點是在於兩者都是在cache miss情況下而跑去讀取資料庫`
<!--SR:!2023-10-20,240,242-->


#🧠 以Cache miss為主的同步方式：Read Through 和 Read Aside兩者間的差異點為？ ->->-> `Read Through 和 Read Aside 差別是在於後者是客戶端通過存取資料庫的資料，來同步緩存資料，前者則是因爲客戶端向緩存索要，但它沒有，所以只好由緩存自己向資料庫索要資料來同步緩存，接著回傳給客戶端`
<!--SR:!2024-12-23,500,242-->



---
Status: #☀️ 
Tags:
[[Caching]] - [[Redis]] - [[Database]]
Links:
[[以write-hit為主的write through和write back(write behind)這兩種寫入策略通常會為了一致性而與資料庫同步資料]]
[[inline Caching 是客戶端直接以cache為主要儲存系統的風格 ，Look-Aside Caching 則是先以cache來處理，再來以DB作處理的風格]]
References:
[[@jyt0532HuanCunDuXieJiZhiJyt0532Blog]]
[[@itrendeyitianHuanCunDeWuZhongSheJiMoShiMeiRiTouTiao]]