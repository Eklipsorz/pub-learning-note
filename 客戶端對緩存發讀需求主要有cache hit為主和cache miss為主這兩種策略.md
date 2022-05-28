## 描述
引用[[@jyt0532HuanCunDuXieJiZhiJyt0532Blog]]所描述的策略：
> 客戶直接向緩存發讀需求
> cache hit(就是東西在cache): 那就直接回傳 皆大歡喜
> cache miss: 分兩種
> - Read through: cache負責跟DB要正確的資料 **寫進cache**之後 再回傳給客戶
> - Read aside: 那客戶負責跟DB要正確的資料 要到之後呢 可以叫客戶去更新緩存(Demand-fill)

重點：假設環境有客戶端、緩存、資料庫
- 以Cache hit 為主：當客戶端要找的東西A就在緩存，就直接回傳處於緩存中的東西A。
- 以Cache miss 為主：當客戶端要的東西A在緩存裡找不到，就會去資料庫裡找，找法有分種
	- Read Through ：如同字面上的意思，讀取會穿過緩存來進行，首先，緩存負責向資料庫索要東西A，找到後就寫進緩存，然後再回傳緩存中的東西A，這樣過程會像是下圖這樣，透過(穿過緩存)來存取東西A
	![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1653765958/blog/database/caching/Read-Through-Diagram_w98usw.png)
	Read Through 步驟：
	步驟1 是客戶端向緩存索要東西A讀取，但緩存沒有
	步驟2 緩存由於沒有東西A，緩存就向資料庫索要東西A，並從那獲得
	步驟3 緩存將獲取到的東西A寫入至快取，以便未來客戶端直接向快取尋找增加效率。
	![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1653765958/blog/database/caching/Read-Through-Steps_zyjmyk.png)
	- Read Aside：如同字面上的意思，讀取會先讀取一旁的緩存，接著再從資料庫找。
### note
1. cache hit: 當東西能夠在緩存找到，就表示cache hit
2. cache miss：當東西在緩存裡找不到，就表示cache miss


## 複習
#🧠 Question :: ->->-> ``

---
Status: #🌱 
Tags:
[[Caching]] - [[Redis]] - [[Database]]
Links:
References:
[[@jyt0532HuanCunDuXieJiZhiJyt0532Blog]]