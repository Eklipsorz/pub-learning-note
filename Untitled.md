## 描述


### Master-Master Replication
[[@karanpratansinghSystemDesignComplete]]
> Both masters serve reads/writes and coordinate with each other. If either master goes down, the system can continue to operate with both reads and writes.

![](https://raw.githubusercontent.com/karanpratapsingh/portfolio/master/public/static/courses/system-design/chapter-II/database-replication/master-master-replication.png)

重點：
- Master-Master Replication：是指每個資料庫服務的主機都皆為master主機，並同時相互對同份資料/自己master主機所分出的資料進行一致性、完整性、冗余問題進行維護
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
	- 當主機發生故障時，可以快速轉移至其他主機
- 缺點：考量到各自主機有自己要分享的副本給其他主機
	- 對於Master-Slave Replication 架構而言，設定和部署難度較難，
	- 由於全部主機都皆為master主機，會因為副本更新而使得同步延遲情況、一致性問題更加惡化
	- 當master主機增加以及延遲情況出現時，會容易出現資料衝突問題


## 複習
#🧠 Master-Master Replication ->->-> ``

---
Status: #🌱 
Tags:
[[Database]]
Links:
References:
[[@karanpratansinghSystemDesignComplete]]