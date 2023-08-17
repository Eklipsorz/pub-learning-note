
## 描述
[[@http___zotero.org_users_9524198_items_4GBXZ7K7]]
> ## More Control in the Application Layer

> In contrast to inline caching, look-aside caching is declarative - the developer tells the application what to cache, not how to do it. For example, with inline caching, the developer must deploy code to the cache server. The developer must also imperatively handle cache misses. The developer optionally deploys code to allow writes to the cache to be pushed into the backing-store either synchronously or asynchronously.

> So, a key difference between inline and look-aside caching patterns is what the application code does versus what the cache does. In the look-aside caching pattern, there is more control in the application layer. In the inline caching pattern, code is deployed into the cache servers, and then the cache takes control of reading from and writing to the backing store.

重點:
- inline caching 和 look-aside caching 最大的不同在於: 資料上的管理，主要分為以下三個
	- 使用資料的那一方會如何讀取/寫入資料
	- cache如何處理cache miss、cache hit、write miss、write hit這四種狀況
	- 由於前兩者對於如何實現而構成的結構
- 對於 **使用資料的那一方會如何讀取/寫入資料**之實際情況: 
	- 得由開發者告知應用程式如何合法從cache或者後備存儲資料的地方進行讀取或者寫入
		- 通常告知方式為下達代表特定目標的指令來處理cache miss、cache hit、write miss、write hit這四種狀況 - cache server或後備存儲資料的伺服器收到該指令就解析成一系列如何實現該目標的指令來執行
	- 開發者不用在cache或者後備存儲資料的地方事先定義cache miss、cache hit、write miss、write hit這四種狀況
- 對於 **cache會如何處理cache miss、cache hit、write miss、write hit這四種狀況**
	- 得由開發者自行定義一系列指令在cache server如何處理cache miss、cache hit、write miss、write hit這四種狀況
		- 若資料不在伺服器上的話，得由cache server向後備存儲資料的地方索要
		- 通常告知方式為如何處理來達成目標的風格，而非指定目標
	- 開發者不需要在應用程式去處理cache miss、cache hit、write miss、write hit這四種狀況
- 整體架構:
	- inline caching
![](https://content.cdntwrk.com/files/aHViPTYzOTc1JmNtZD1pdGVtZWRpdG9yaW1hZ2UmZmlsZW5hbWU9aXRlbWVkaXRvcmltYWdlXzU4OWUzYTI0MTA5MTUucG5nJnZlcnNpb249MDAwMCZzaWc9ZjAzYzE4NGI2MzkwNjRiYThiNTQ0YjZhMzc2NzBiOTE%253D)
	- look-aside caching
![](https://content.cdntwrk.com/files/aHViPTYzOTc1JmNtZD1pdGVtZWRpdG9yaW1hZ2UmZmlsZW5hbWU9aXRlbWVkaXRvcmltYWdlXzU4OWUzYTBmZjJkMGQucG5nJnZlcnNpb249MDAwMCZzaWc9NGRlMTVhODA3NmFlYTdhNDMxOGU1MmQ0OTc2ZWY2ZDI%253D)
## 複習


#🧠 write-miss 下有哪些策略可用 ->->-> `allocate no write、allocate on write`

#🧠 write-hit下有哪些策略可用 ->->-> `write through、write behind`

#🧠 cache-miss下有哪些策略可用 ->->-> `read through、read aside`

#🧠 read through 對於client、cache、backup storage環境下，通常會對cache和backup storage構成甚麼樣的架構? 為什麼 ->->-> `inline caching，因為會需要前者`

#🧠 read aside 對於client、cache、backup storage環境下，通常會對cache和backup storage構成甚麼樣的架構 ->->-> `look-aside caching`

#🧠 inline caching 為什麼叫做inline ? ->->-> `因為整體架構下的每個元件會並排一塊，每個元件會與較近的元件相連`

#🧠 look-aside caching 為什麼叫做look-aside?  ->->-> `因為整體架構下，每個元件都可以向任意一邊進行相連來進行操作`

#🧠 inline caching 和 look-aside caching最大的不同在於甚麼地方? ->->-> `資料上的管理`

#🧠 inline caching 和 look-aside caching最大的不同在於資料上的管理，請詳細解釋?->->-> `- 使用資料的那一方會如何讀取/寫入資料 - cache如何處理cache miss、cache hit、write miss、write hit這四種狀況 - 由於前兩者對於如何實現而構成的結構`

#🧠 Question :: ->->-> ``

#🧠 Question :: ->->-> ``


---
Status: #🌱 
Tags:
[[Caching]] - [[OS]]
Links:
[[@http___zotero.org_users_9524198_items_4GBXZ7K7]]
References: