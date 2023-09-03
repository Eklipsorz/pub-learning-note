
## 描述
[[@IntroductionLookAsideCaching]]
> ## More Control in the Application Layer

> In contrast to inline caching, look-aside caching is declarative - the developer tells the application what to cache, not how to do it. For example, with inline caching, the developer must deploy code to the cache server. The developer must also imperatively handle cache misses. The developer optionally deploys code to allow writes to the cache to be pushed into the backing-store either synchronously or asynchronously.

> So, a key difference between inline and look-aside caching patterns is what the application code does versus what the cache does. In the look-aside caching pattern, there is more control in the application layer. In the inline caching pattern, code is deployed into the cache servers, and then the cache takes control of reading from and writing to the backing store.

重點:
- inline caching 和 look-aside caching 最大的不同在於: 資料上的管理，主要分為以下三個
	- 使用資料的那一方會如何讀取/寫入資料
	- cache如何處理cache miss、cache hit、write miss、write hit這四種狀況
	- 由於前兩者對於如何實現而構成的結構
- 對於 **使用資料的那一方會如何讀取/寫入資料** 和  **cache會如何處理cache miss、cache hit、write miss、write hit這四種狀況**之實際情況: 
	- look-aside caching
		- 得由開發者事先告知應用程式如何合法從cache或者後備存儲資料的地方進行讀取或者寫入
			- 通常告知方式為下達代表特定目標的指令來處理cache miss、cache hit、write miss、write hit這四種狀況 - cache server或後備存儲資料的伺服器收到該指令就解析成一系列如何實現該目標的指令來執行
		- 開發者不用在cache或者後備存儲資料的地方事先定義cache miss、cache hit、write miss、write hit這四種狀況
	- inline caching
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
<!--SR:!2023-09-18,18,230-->

#🧠 write-hit下有哪些策略可用 ->->-> `write through、write behind`
<!--SR:!2023-09-20,20,230-->

#🧠 cache-miss下有哪些策略可用 ->->-> `read through、read aside`
<!--SR:!2023-09-05,13,250-->

#🧠 read through 對於client、cache、backup storage環境下，通常會對cache和backup storage構成甚麼樣的架構? 為什麼 ->->-> `inline caching，因為會需要前者`
<!--SR:!2023-09-05,13,250-->

#🧠 read aside 對於client、cache、backup storage環境下，通常會對cache和backup storage構成甚麼樣的架構 ->->-> `look-aside caching`
<!--SR:!2023-09-30,27,250-->

#🧠 inline caching 為什麼叫做inline ? ->->-> `因為整體架構下的每個元件會並排一塊，每個元件會與較近的元件相連`
<!--SR:!2023-09-05,13,250-->

#🧠 look-aside caching 為什麼叫做look-aside?  ->->-> `因為整體架構下，每個元件都可以向任意一邊進行相連來進行操作`
<!--SR:!2023-09-29,26,250-->

#🧠 inline caching 和 look-aside caching最大的不同在於甚麼地方? ->->-> `資料上的管理`
<!--SR:!2023-10-04,31,250-->

#🧠 inline caching 和 look-aside caching最大的不同在於資料上的管理，請詳細解釋?->->-> `- 使用資料的那一方會如何讀取/寫入資料 - cache如何處理cache miss、cache hit、write miss、write hit這四種狀況 - 由於前兩者對於如何實現而構成的結構`
<!--SR:!2023-09-28,25,250-->

#🧠  inline caching 和 look-aside caching:  對於 **使用資料的那一方會如何讀取/寫入資料**之實際情況而言會是? ->->-> `look-aside caching 得由開發者事先告知應用程式如何合法從cache或者後備存儲資料的地方進行讀取或者寫入； inline caching 開發者不需要在應用程式去處理cache miss、cache hit、write miss、write hit這四種狀況`
<!--SR:!2023-10-01,28,250-->

#🧠  inline caching 和 look-aside caching:  對於 **cache會如何處理cache miss、cache hit、write miss、write hit這四種狀況**之實際情況而言會是? ->->-> `look-aside caching: 開發者不用在cache或者後備存儲資料的地方事先定義cache miss、cache hit、write miss、write hit這四種狀況； inline caching: 得由開發者自行定義一系列指令在cache server如何處理cache miss、cache hit、write miss、write hit這四種狀況`
<!--SR:!2023-09-04,12,250-->

#🧠 inline caching - 得由開發者自行定義一系列指令在cache server如何處理cache miss、cache hit、write miss、write hit這四種狀況，其指令的風格為何? 為什麼是xx?->->-> `imperative 風格，因為沒必要額外定義代表目標的指令以及解析其指令的成本`
<!--SR:!2023-09-27,24,250-->

#🧠  look-aside caching- 得由開發者事先告知應用程式如何合法從cache或者後備存儲資料的地方進行讀取或者寫入之代碼風格為何? 為什麼是xx? ->->-> `declarative 風格，因為要保持該應用程式的易讀性，所以會以該應用程式所用的程式語言來表達其目標，而非以額外的語言形式來表達。`
<!--SR:!2023-09-11,12,248-->

#🧠 在look-aside caching中，為何開發者不用特定設定cache server或者後備資料中心面對cache miss、cache hit、write miss、write hit這四種狀況，而是直接從應用程式來指示?  ->->-> `1. 讓cache server或者後備資料中心的可重複使用率提升 `
<!--SR:!2023-09-12,9,248-->


#🧠  look-aside caching- 得由開發者事先告知應用程式如何合法從cache或者後備存儲資料的地方進行讀取或者寫入，其中事先告知/發送請求的代碼形式會是? 若server收到該請求會如何執行->->-> `通常會是以應用程式下的程式語言來構築，應用程式當發送時會轉換成該server能解析的形式，然後當server收到對應指令時會進一步解析成一系列如何實現該目標的指令來執行`
<!--SR:!2023-10-03,30,250-->

#🧠 inline caching 得由開發者自行定義一系列指令在cache server如何處理cache miss、cache hit、write miss、write hit這四種狀況，其中指令的代碼形式為什麼? ->->-> `通常會是該server能夠直接解析的形式`
<!--SR:!2023-09-04,12,250-->


#🧠 inline caching上，若以client、cache server、database server為例來畫該架構圖 ->->-> ![](https://content.cdntwrk.com/files/aHViPTYzOTc1JmNtZD1pdGVtZWRpdG9yaW1hZ2UmZmlsZW5hbWU9aXRlbWVkaXRvcmltYWdlXzU4OWUzYTI0MTA5MTUucG5nJnZlcnNpb249MDAwMCZzaWc9ZjAzYzE4NGI2MzkwNjRiYThiNTQ0YjZhMzc2NzBiOTE%253D)
<!--SR:!2023-09-04,12,250-->

#🧠 在look-aside caching上，若以client、cache server、database server為例來畫該架構圖  ->->-> ![](https://content.cdntwrk.com/files/aHViPTYzOTc1JmNtZD1pdGVtZWRpdG9yaW1hZ2UmZmlsZW5hbWU9aXRlbWVkaXRvcmltYWdlXzU4OWUzYTBmZjJkMGQucG5nJnZlcnNpb249MDAwMCZzaWc9NGRlMTVhODA3NmFlYTdhNDMxOGU1MmQ0OTc2ZWY2ZDI%253D)
<!--SR:!2023-10-05,32,250-->


#🧠 在inline-caching 中，為何通常不用特定在應用程式端點指示如何處理write-hit、write-miss、cache-hit、cache-miss ->->-> `因為應用程式端點會受限於結構上而無法輕易存取後備資料中心的資料，導致沒辦法妥善處理那四種狀況`
<!--SR:!2023-09-04,1,228-->




---
Status: #🌱 
Tags:
[[Caching]] - [[OS]]
Links:
[[@IntroductionLookAsideCaching]]
References: