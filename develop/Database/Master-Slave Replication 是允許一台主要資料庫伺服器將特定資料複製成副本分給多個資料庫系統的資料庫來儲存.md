## 描述


### Master-Slave Replication
[[@karanpratansinghSystemDesignComplete]]

> ## Master-Slave Replication

> The master serves reads and writes, replicating writes to one or more slaves, which serve only reads. Slaves can also replicate additional slaves in a tree-like fashion. If the master goes offline, the system can continue to operate in read-only mode until a slave is promoted to a master or a new master is provisioned.

![](https://raw.githubusercontent.com/karanpratapsingh/portfolio/master/public/static/courses/system-design/chapter-II/database-replication/master-slave-replication.png)


[[@mariadbDatabaseMasterSlaveReplication2013]]
> Master-slave replication enables data from one database server (the master) to be replicated to one or more other database servers (the slaves).

[[@developpaperMySQLMasterslaveReplication]]
>The implementation of read-write separation is based on the master-slave replication architecture: one master and multiple slaves, only write to the master library, and the master library will automatically synchronize the data to the slave library.

 重點：
 - Master-Slave Replication 是一台主要資料庫系統將特定資料複製成副本分給多個資料庫系統上的資料庫來儲存，以此讓多個資料庫系統共享同份資料，並由主要資料庫伺服器進行資料上的維護&管理
 - 在這裡負責提供資料副本的資料庫伺服器是master主機，接收到副本的資料庫伺服器是slave主機
 - 技術細節：
	 - Slave 主機可以切分額外的Slave子結構
	 - 如果master主機離線，同份資料的存取就僅剩下讀取，除非有slave主機承擔起master主機或者有新的master主機加入。
- 可應用於
	- Read/Write Splitting 技術


### 權限： master & slave 
 - 權限：在擁有同份資料的情況下，master主機會擁有讀取資料、寫入資料、以目前資料內容作為副本傳遞至其他主機上。slave 主機只會有讀取資料的權限

### 業務內容：master & slave
 -  master 主機 業務內容：
	- 因權限而負責處理同份資料的寫入請求
	- 因權限而負責處理同份資料的讀取請求
	- 因權限而負責處理同份資料的同步資料副本至其他slave主機

- slave 主機業務內容：
	- 因權限而負責處理同份資料的讀取請求

#### Advantages & Disadvantages

> ### Advantages

> -   Backups of the entire database of relatively no impact on the master.
> -   Applications can read from the slave(s) without impacting the master.
> -  Slaves can be taken offline and synced back to the master without any downtime.

> ### Disadvantages

> -   Replication adds more hardware and additional complexity.
> -   Downtime and possibly loss of data when a master fails.
> -   All writes also have to be made to the master in a master-slave architecture.
> -   The more read slaves, the more we have to replicate, which will increase replication lag.

重點：
- 優點為
	- 資料備份
	- 應用程式可從Slave 主機讀取資料，不用跑到Master主機
	- Slave 主機可以憑藉數量優勢，暫時以離線去從Master 主機獲取新資料
- 缺點：
	- 從master 主機製作副本並分發至slaves的成本較高：硬體需求、計算需求
	- 當master 主機出現問題時，可能會出現資料上的遺失
	- 所有寫入請求都只能集中在單一的master主機
	- slave主機數量越多，製作副本並分發的成本就越高，同時會增加replication lag的情況

#### Replication lag
[[@karanpratansinghSystemDesignComplete]]
> 資料要從發生寫入的地方，複製到另一個地方，這中間的時間差就是**replication lag**

> This is the difference between the current time and the original timestamp at which the primary database committed the transaction that is currently being applied on the replica.


重點：
- replication lag：是指當master主機的資料庫系統上發生資料更改、寫入時，從資料一被更改到資料複製到其他主機且讓其他主機採用的時間差。

## 複習

#🧠 Master-Slave Replication 是什麼樣的技術？->->-> `Master-Slave Replication 是一台主要資料庫系統將特定資料複製成副本分給多個資料庫系統上的資料庫來儲存，以此讓多個資料庫系統共享同份資料，並由主要資料庫伺服器進行資料上的維護&管理`


#🧠 Master-Slave Replication 技術下，Master 和Slave是指什麼？ ->->-> `在這裡負責提供資料副本的資料庫伺服器是master主機，接收到副本的資料庫伺服器是slave主機`

#🧠 Master-Slave Replication 技術下的Master和Slave都是什麼？ ->->-> `擁有資料庫服務的主機`

#🧠 Master-Slave Replication 技術下的Master主機的權限為何？ ->->-> `master主機會擁有讀取資料、寫入資料、以目前資料內容作為副本傳遞至其他主機上`

#🧠 Master-Slave Replication 技術下的Slave主機的權限為何？ ->->-> `slave 主機只會有讀取資料的權限`

#🧠 Master-Slave Replication 技術下的Master主機的業務內容為何？ ->->-> `	- 因權限而負責處理同份資料的寫入請求 - 因權限而負責處理同份資料的讀取請求 - 因權限而負責處理同份資料的同步資料副本至其他slave主機`

#🧠 Master-Slave Replication 技術下的Slave主機的業務內容為何？ ->->-> `- 因權限而負責處理同份資料的讀取請求`

#🧠 Master-Slave Replication 技術 可應用什麼技術？ ->->-> `Read/Write Splitting 技術`

#🧠 Replication lag 是什麼？ ->->-> `是指當master主機的資料庫系統上發生資料更改、寫入時，從資料一被更改到資料複製到其他主機且讓其他主機採用的時間差。`


#🧠 Replication lag 是指當master主機的資料庫系統上發生資料更改、寫入時，從資料一被更改到資料複製到其他主機且讓其他主機採用的時間差，請問其他主機有限定於slave主機嗎 ->->-> `並沒有，主要被分到的任意主機是否採用`


#🧠 Master-Slave Replication 技術下，如果master主機離線，其他主機還能正常作用嗎？ ->->-> `能，如果master主機離線，同份資料的存取就僅剩下讀取，除非有slave主機承擔起master主機或者有新的master主機加入。`

#🧠 Master-Slave Replication 技術下，如果其中一台slave主機離線，其他主機還能正常作用嗎？  ->->-> `能，還有其他slave主機可以提供同份資料的讀請求以及master提供同份資料的寫請求`

#🧠 Master-Slave Replication 技術下，優點為何？(共有三個：備、分、獲取)->->-> `	- 資料備份 - 應用程式可從Slave 主機讀取資料，不用跑到Master主機 - Slave 主機可以憑藉數量優勢，暫時以離線去從Master 主機獲取新資料`

#🧠  Master-Slave Replication 技術下，缺點為何？(共有四個：成本、遺失、寫、lag)->->-> `- 從master 主機製作副本並分發至slaves的成本較高：硬體需求、計算需求 - 當master 主機出現問題時，可能會出現資料上的遺失 - 所有寫入請求都只能集中在單一的master主機 - slave主機數量越多，製作副本並分發的成本就越高，同時會增加replication lag的情況`

---
Status: #🌱 
Tags
[[Database]]
Links:
[[Database Replication  是將資料進行同結構同內容的複製來製作成多個副本分發至其他系統上]]
[[Read-Write Splitting 是指在多個主機共享同個資料庫資料的情況下專門提供專門讀取資料的主機和專門寫資料的主機]]
[[Master-Master Replication 架構是每個資料庫系統皆為主要資料庫系統，都會將特定資料複製成副本給所有資料庫系統的資料庫，以此讓多個資料庫系統共享資料]]
References:
[[@mariadbDatabaseMasterSlaveReplication2013]]
[[@karanpratansinghSystemDesignComplete]]
[[@developpaperMySQLMasterslaveReplication]]