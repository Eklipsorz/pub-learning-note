
## 描述

> ## More Control in the Application Layer

> In contrast to inline caching, look-aside caching is declarative - the developer tells the application what to cache, not how to do it. For example, with inline caching, the developer must deploy code to the cache server. The developer must also imperatively handle cache misses. The developer optionally deploys code to allow writes to the cache to be pushed into the backing-store either synchronously or asynchronously.

> So, a key difference between inline and look-aside caching patterns is what the application code does versus what the cache does. In the look-aside caching pattern, there is more control in the application layer. In the inline caching pattern, code is deployed into the cache servers, and then the cache takes control of reading from and writing to the backing store.

重點:
- inline caching 和 look-aside caching 最大的不同在於: 資料上的管理，主要分為以下兩個
	- 使用資料的那一方會如何讀取/寫入資料
	- cache如何處理cache miss、cache hit、write miss、write hit這四種狀況
- 對於 **使用資料的那一方會如何讀取/寫入資料**之實際情況: 
	- 得由開發者告知應用程式如何合法從cache或者後備存儲資料的地方進行讀取或者寫入
		- 通常告知方式為下達代表特定目標的指令來完成 - cache server或後備存儲資料的伺服器收到該指令就解析成一系列如何實現該目標的指令來執行
	- 開發者不用在cache或者後備存儲資料的地方事先定義cache miss、cache hit、write miss、write hit這四種狀況
- 對於 **cache會如何處理cache miss、cache hit、write miss、write hit這四種狀況**
	- 得由開發者自行定義一系列指令在cache server如何處理cache miss、cache hit、write miss、write hit這四種狀況
		- 若資料不在伺服器上的話，得由cache server向後備存儲資料的地方索要
		- 通常告知方式為如何處理來達成目標的風格，而非指定目標
	- 開發者不需要應用程式

## 複習


#🧠 write-miss 下有哪些策略可用 ->->-> `allocate no write、allocate on write`

#🧠 write-hit下有哪些策略可用 ->->-> `write through、write behind`

#🧠 cache-miss下有哪些策略可用 ->->-> `read through、read aside`

#🧠 read through 對於client、cache、backup storage環境下，通常會對cache和backup storage構成甚麼樣的架構? 為什麼 ->->-> `inline caching，因為會需要前者`

#🧠 read aside 對於client、cache、backup storage環境下，通常會對cache和backup storage構成甚麼樣的架構 ->->-> `look-aside caching`

#🧠 Question :: ->->-> ``

#🧠 Question :: ->->-> ``

---
Status: #🌱 
Tags:
[[Caching]] - [[OS]]
Links:
References: