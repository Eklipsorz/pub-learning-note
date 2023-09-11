## 描述


### Master-Master Replication
[[@karanpratansinghSystemDesignComplete]]
> Both masters serve reads/writes and coordinate with each other. If either master goes down, the system can continue to operate with both reads and writes.

![](https://raw.githubusercontent.com/karanpratapsingh/portfolio/master/public/static/courses/system-design/chapter-II/database-replication/master-master-replication.png)



重點：
- Master-Master Replication：是指每個資料庫系統皆為主要資料庫系統，都會將特定資料複製成副本給所有資料庫系統的資料庫來儲存，以此讓多個資料庫系統共享資料。
- 資料分享模式：
	- 每台Master主機各有一份資料要分享給其他主機
	- 多個Master主機共同分享同一份資料給其他主機
- 技術細節：
	- 當任何一台master發生問題時，仍能憑藉master數量優勢使得同份資料的讀寫存取請求都能正常被處理
	- 每一台主機皆因為master主機而可供使用者進行同份資料的讀/寫


###  優缺點
[[@karanpratansinghSystemDesignComplete]]
> ### Advantages
> -   Applications can read from both masters.
> -   Distributes write load across both master nodes.
> -   Simple, automatic, and quick failover.

> ### Disadvantages
> -   Not as simple as master-slave to configure and deploy.
> -   Either loosely consistent or have increased write latency due to synchronization.
> -   Conflict resolution comes into play as more write nodes are added and as latency increases.

重點：
- 優點為：
	- 在此架構下，每台主機都能對同份資料進行讀和寫
	- 對於Master-Slave Replication 架構而言，寫請求較能憑藉寫權限的主機數增而能夠被平攤
	- 當主機發生故障時，可以切換成其他主機來使用
- 缺點：考量到各自主機有自己要分享的副本給其他主機
	- 對於Master-Slave Replication 架構而言，設定和部署難度較難，
	- 由於全部主機都皆為master主機，會因為副本更新而使得同步延遲情況惡化
	- 由於每一台都有寫的權限，會有race condition相關問題
	- 當master主機增加以及延遲情況出現時，會容易出現資料衝突問題


## 複習
#🧠 Master-Master Replication 是什麼？ ->->-> `指每個資料庫系統皆為主要資料庫系統，都會將特定資料複製成副本給所有資料庫系統的資料庫來儲存，以此讓多個資料庫系統共享資料。`
<!--SR:!2023-10-28,259,250-->

#🧠 在Master-Master Replication架構下，當任何一台master發生問題時，能正常處理資料庫請求嗎？為什麼 ->->-> `可以，仍能憑藉master數量優勢使得同份資料的讀寫存取請求都能正常被處理`
<!--SR:!2024-11-03,489,250-->

#🧠 在Master-Master Replication架構下，資料分享模式：->->-> `每台Master主機各有一份資料要分享給其他主機、多個Master主機共同分享同一份資料給其他主機`
<!--SR:!2024-06-02,391,250-->

#🧠 Master-Master Replication架構的優點為何？(提示：共有三個，讀寫、平攤、容錯) ->->-> `	- 在此架構下，每台主機都能對同份資料進行讀和寫 - 對於Master-Slave Replication 架構而言，寫請求較能憑藉寫權限的主機數增而能夠被平攤 - 當主機發生故障時，可以切換成其他主機來使用`
<!--SR:!2023-10-28,155,230-->

#🧠 Master-Master Replication架構的缺點為何？(提示：共有四個，難度、延遲、race、增加) ->->-> `	- 對於Master-Slave Replication 架構而言，設定和部署難度較難，- 由於全部主機都皆為master主機，會因為副本更新而使得同步延遲情況惡化- 由於每一台都有寫的權限，會有race condition相關問題 - 當master主機增加以及延遲情況出現時，會容易出現資料衝突問題`
<!--SR:!2023-09-30,18,150-->



---
Status: #🌱 
Tags:
[[Database]]
Links:
[[Master-Slave Replication 是允許一台主要資料庫伺服器將特定資料複製成副本分給多個資料庫系統的資料庫來儲存]]
References:
[[@karanpratansinghSystemDesignComplete]]