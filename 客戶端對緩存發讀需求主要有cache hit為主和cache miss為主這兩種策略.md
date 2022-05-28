## 描述
引用[[@jyt0532HuanCunDuXieJiZhiJyt0532Blog]]所描述的策略：
> 客戶直接向緩存發讀需求
> cache hit(就是東西在cache): 那就直接回傳 皆大歡喜
> cache miss: 分兩種
> - Read through: cache負責跟DB要正確的資料 **寫進cache**之後 再回傳給客戶
> - Read aside: 那客戶負責跟DB要正確的資料 要到之後呢 可以叫客戶去更新緩存(Demand-fill)
> 如果你想減少一些讀的latency 也可以建個Kafka 讓緩存subscribe一個Kafka topic 只要有讀request到DB DB就publish這個讀的內容 緩存收到後自己更新

重點：假設環境有客戶端、緩存、資料庫
- 以Cache hit 為主：當客戶端要找的東西A就在緩存，就直接回傳處於緩存中的東西A。
- 以Cache miss 為主：當客戶端要的東西A在緩存裡找不到，就會去資料庫裡找，找法有分種
	- Read Through ：如同字面上的意思，讀取會穿過緩存來進行，首先，客戶端會向緩存找東西，但找不到，所以由緩存負責向資料庫索要東西A，找到後就寫進緩存，然後再回傳緩存中的東西A，這樣過程會像是下圖這樣，透過(穿過緩存)來存取東西A
	![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1653765958/blog/database/caching/Read-Through-Diagram_w98usw.png)
	Read Through 步驟：
	步驟1 是客戶端向緩存索要東西A讀取，但緩存沒有
	步驟2 緩存由於沒有東西A，緩存就向資料庫索要東西A，並從那獲得
	步驟3 緩存將獲取到的東西A寫入至緩存，以便未來客戶端直接向緩存尋找增加效率。
	![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1653765958/blog/database/caching/Read-Through-Steps_zyjmyk.png)
	- Read Aside：如同字面上的意思，讀取會先讀取一旁的緩存，接著再從資料庫找，首先，客戶端會負責向緩存索要東西A，但找不到，所以再由客戶端向另一邊的資料庫找東西A，找到東西A後，就由客戶端來將東西A寫入至緩存，過程就如下圖這樣，就先往一邊找，找不到就往另一邊找
	![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1653767516/blog/database/caching/Read-Aside-Diagram_koz5ym.png)
	Read Aside 步驟：
	步驟1 是客戶端向緩存索要東西A讀取，但緩存沒有
	步驟2 緩存由於沒有東西A，客戶端就向資料庫索要東西A，並從那獲得
	步驟3 客戶端將獲取到的東西A寫入至緩存，以便未來客戶端直接向緩存尋找增加效率。
	![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1653767516/blog/database/caching/Read-Aside-Steps_fmb5p7.png)
### note
cache hit 和 cache miss 原為CPU對於緩存能不能找到想要東西的用語：
1. cache hit: 當CPU能夠從緩存找到想要的東西，就表示cache hit
2. cache miss：當CPU不能夠從緩存找到想要的東西，就表示cache miss

在這裡是將CPU比喻成客戶端來表示，緩存會是以用記憶體為主的資料庫，而硬碟會是以硬碟為主的資料庫：
1. cache hit: 當客戶端能夠從緩存找到想要的東西，就表示cache hit
2. cache miss：當客戶端不能夠從緩存找到想要的東西，就表示cache miss

## 複習
#🧠 cache hit 和 cache miss 緣由是什麼？分別是什麼意思->->-> `cache hit 和 cache miss 原為CPU對於緩存能不能找到想要東西的用語，cache hit: 當CPU能夠從緩存找到想要的東西，就表示cache hit、cache miss：當CPU不能夠從緩存找到想要的東西，就表示cache miss，而套用在資料庫、緩存、客戶端環境的話，就是將CPU比喻成客戶端來表示，緩存會是以用記憶體為主的資料庫，而硬碟會是以硬碟為主的資料庫`

#🧠 以Cache hit 為主的caching 策略會是什麼(提示：就如同我要吃東西，就要打開裝滿食物的箱子，接著會做？？)->->-> `當客戶端要找的東西A就在緩存，就直接回傳處於緩存中的東西A。`

#🧠 以Cache miss 為主的caching策略會是什麼->->-> `Read Through ：如同字面上的意思，讀取會穿過緩存來進行，首先，客戶端會向緩存找東西，但找不到，所以由緩存負責向資料庫索要東西A，找到後就寫進緩存，然後再回傳緩存中的東西A，這樣過程會像是下圖這樣，透過(穿過緩存)來存取東西A，Read Aside：如同字面上的意思，讀取會先讀取一旁的緩存，接著再從資料庫找，首先，客戶端會負責向緩存索要東西A，但找不到，所以再由客戶端向另一邊的資料庫找東西A，找到東西A後，就由客戶端來將東西A寫入至緩存`


#🧠 Caching 策略：Read Through步驟是什麼？以這圖來說明	![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1653765958/blog/database/caching/Read-Through-Steps_zyjmyk.png)  ->->-> `	步驟1 是客戶端向緩存索要東西A讀取，但緩存沒有，步驟2 緩存由於沒有東西A，緩存就向資料庫索要東西A，並從那獲得，步驟3 緩存將獲取到的東西A寫入至緩存，以便未來客戶端直接向緩存尋找增加效率。`

#🧠 Caching 策略：Read Aside步驟是什麼？以這圖來說明![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1653767516/blog/database/caching/Read-Aside-Diagram_koz5ym.png)->->-> `	步驟1 是客戶端向緩存索要東西A讀取，但緩存沒有，步驟2 緩存由於沒有東西A，客戶端就向資料庫索要東西A，並從那獲得，步驟3 客戶端將獲取到的東西A寫入至緩存，以便未來客戶端直接向緩存尋找增加效率。`

---
Status: #🌱 
Tags:
[[Caching]] - [[Redis]] - [[Database]]
Links:
[[以write-hit為主要分為write through caching和write back(write behind) caching]]
[[inline Caching 是客戶端直接以cache為主要儲存系統的風格 ，Look-Aside Caching 則是先以cache來處理，再來以DB作處理的風格]]
References:
[[@jyt0532HuanCunDuXieJiZhiJyt0532Blog]]