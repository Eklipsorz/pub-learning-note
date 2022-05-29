## 描述


引用[[@jyt0532HuanCunDuXieJiZhiJyt0532Blog]]所描述的策略：
> 客戶直接向緩存發讀需求
> cache hit(就是東西在cache): 那就直接回傳 皆大歡喜
> cache miss: 分兩種
> - Read through: cache負責跟DB要正確的資料 **寫進cache**之後 再回傳給客戶
> - Read aside: 那客戶負責跟DB要正確的資料 要到之後呢 可以叫客戶去更新緩存(Demand-fill)
> 如果你想減少一些讀的latency 也可以建個Kafka 讓緩存subscribe一個Kafka topic 只要有讀request到DB DB就publish這個讀的內容 緩存收到後自己更新

重點：假設環境有客戶端、緩存、資料庫
- 以Cache hit 為主：當客戶端要找的東西A就在緩存，就直接回傳處於緩存中的東西A，不同步資料庫的資料，這容易出現 **緩存的資料是舊的，資料庫的資料是新，而客戶端只會存取緩存舊資料** 的異常現象
- 以Cache miss 為主：當客戶端要的東西A在緩存裡找不到，就會去資料庫裡找，而這表示緩存資料不是最新的，通常可以選擇是否讓緩存與資料庫保持同步，若不同步的話，總會花更多時間去資料庫尋找資料；若同步的話，總會有提升效能的機會。
- 無論是否同步，Cache miss為主的讀取策略主要會有：
	- Read Through
	- Read Aside

### Read Through
Read Through ：如同字面上的意思，讀取會穿過緩存來進行，首先，客戶端會向緩存找東西，但找不到，所以由緩存負責向資料庫索要東西A，找到後，緩存可選擇是否寫進緩存

#### 若緩存不選擇回寫資料至緩存
若選擇不寫緩存，那麼就會由緩存直接回傳資料庫結果，這樣會使效能因而下降，且客戶端只是麻煩緩存幫忙向資料庫要資料。

#### 若緩存選擇回寫資料至緩存
在這裏假定寫定緩存，然後再回傳緩存中的東西A，這樣過程會像是下圖這樣，透過(穿過緩存)來存取東西A：
	![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1653765958/blog/database/caching/Read-Through-Diagram_w98usw.png)
Read Through 步驟：
- 步驟1 是客戶端向緩存索要東西A讀取，但緩存沒有
- 步驟2 緩存由於沒有東西A，緩存就向資料庫索要東西A，並從那獲得
- 步驟3 緩存將獲取到的東西A寫入至緩存，以便未來客戶端直接向緩存尋找增加效率。
	![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1653765958/blog/database/caching/Read-Through-Steps_zyjmyk.png)
	
### Read Aside
Read Aside：如同字面上的意思，讀取會先讀取一旁的緩存，接著再從資料庫找，首先，客戶端會負責向緩存索要東西A，但找不到，所以再由客戶端向另一邊的資料庫找東西A，找到東西A後，就由客戶端來決定是否將東西A寫入至緩存，這裏假定是客戶端是決定回寫，過程就如下圖這樣，就先往一邊找，找不到就往另一邊找：
	![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1653767516/blog/database/caching/Read-Aside-Diagram_koz5ym.png)
	
Read Aside 步驟：在這裡是假定客戶端是決定將資料庫的資料回寫至緩存。
- 步驟1 是客戶端向緩存索要東西A讀取，但緩存沒有
- 步驟2 緩存由於沒有東西A，客戶端就向資料庫索要東西A，並從那獲得
- 步驟3 客戶端將獲取到的東西A寫入至緩存，以便未來客戶端直接向緩存尋找增加效率。
	![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1653767516/blog/database/caching/Read-Aside-Steps_fmb5p7.png)
	
### note
cache hit 和 cache miss 原為CPU對於緩存能不能找到想要東西的用語：
1. cache hit: 當CPU能夠從緩存找到想要的東西，就表示cache hit
2. cache miss：當CPU不能夠從緩存找到想要的東西，就表示cache miss

在這裡是將CPU比喻成客戶端來表示，緩存會是以用記憶體為主的資料庫，而硬碟會是以硬碟為主的資料庫：
1. cache hit: 當客戶端能夠從緩存找到想要的東西，就表示cache hit
2. cache miss：當客戶端不能夠從緩存找到想要的東西，就表示cache miss

## 複習

#🧠 以Cache hit 為主的讀取策略容易引發什麼樣的問題 ->->-> `Cache hit就表示緩存出現著客戶端想要讀取的資料，但這並不表示這資料會與資料庫的資料是一致的，所以會容易出現 **緩存的資料是舊的，資料庫的資料是新，而客戶端只會存取緩存上的舊資料** 的異常現象`

#🧠  以Cache miss 為主的讀取策略需要考量到什麼? (提示：能否在緩存、資料庫找到？)->->-> `Cache miss就表示資料庫的資料是比緩存還新的，這時會有面臨到若一直往資料庫存取，會有效能下降的問題，因此會選擇將資料庫的資料同步在緩存以增加效能`

#🧠 Cache 讀取策略：Read Aside 中是否能讓客戶端選擇回寫資料至緩存或者不回寫->->-> `理論上，Read Aside是可以讓客戶端有選擇去回寫資料至緩存，畢竟都用上緩存且資料庫的資料是最新，若選擇不回寫的話，客戶端會一直犧牲效能來讀取資料庫；若選擇回寫的話，客戶端就有提升效能的機會來讀取緩存`

#🧠 cache hit 和 cache miss 緣由是什麼？分別是什麼意思->->-> `cache hit 和 cache miss 原為CPU對於緩存能不能找到想要東西的用語，cache hit: 當CPU能夠從緩存找到想要的東西，就表示cache hit、cache miss：當CPU不能夠從緩存找到想要的東西，就表示cache miss`
<!--SR:!2022-06-01,3,250-->

#🧠 以Cache hit 為主的讀取策略會是什麼(提示：就如同我要吃東西，就要打開裝滿食物的箱子，接著會做？？)->->-> `當客戶端要找的東西A就在緩存，就直接回傳處於緩存中的東西A。`
<!--SR:!2022-06-01,3,250-->

#🧠 以Cache miss 為主的讀取策略，若假定不會為了同步而回寫資料至緩存，其結果會是->->-> `那麼客戶端就會一直讀取資料庫而使效能下降`

#🧠 無論是否同步，以Cache miss 為主的讀取策略會是什麼？ ->->-> `Read Through ：如同字面上的意思，讀取會穿過緩存來進行，首先，客戶端會向緩存找東西，但找不到，所以由緩存負責向資料庫索要東西A，找到後，緩存就有選擇是否就寫進緩存，無論是否同步，緩存都會回傳東西A至客戶端，Read Aside：如同字面上的意思，讀取會先讀取一旁的緩存，接著再從資料庫找，首先，客戶端會負責向緩存索要東西A，但找不到，所以再由客戶端向另一邊的資料庫找東西A，找到東西A。`


#🧠 Caching 讀取策略：Read Through步驟是什麼？這裏假定緩存決定回寫，以這圖來說明	![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1653765958/blog/database/caching/Read-Through-Steps_zyjmyk.png)  ->->-> `	步驟1 是客戶端向緩存索要東西A讀取，但緩存沒有，步驟2 緩存由於沒有東西A，緩存就向資料庫索要東西A，並從那獲得，步驟3 緩存將獲取到的東西A寫入至緩存，以便未來客戶端直接向緩存尋找增加效率。`
<!--SR:!2022-06-01,3,250-->

#🧠 Caching 讀取策略：Read Aside步驟是什麼？這裏假定客戶端決定回寫，以這圖來說明![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1653767516/blog/database/caching/Read-Aside-Diagram_koz5ym.png)->->-> `	步驟1 是客戶端向緩存索要東西A讀取，但緩存沒有，步驟2 緩存由於沒有東西A，客戶端就向資料庫索要東西A，並從那獲得，步驟3 客戶端將獲取到的東西A寫入至緩存，以便未來客戶端直接向緩存尋找增加效率。`
<!--SR:!2022-06-01,3,250-->

---
Status: #☀️ 
Tags:
[[Caching]] - [[Redis]] - [[Database]]
Links:
[[以write-hit為主且為了確保同步而分為write through和write back(write behind)這兩種寫入策略]]
[[inline Caching 是客戶端直接以cache為主要儲存系統的風格 ，Look-Aside Caching 則是先以cache來處理，再來以DB作處理的風格]]
References:
[[@jyt0532HuanCunDuXieJiZhiJyt0532Blog]]