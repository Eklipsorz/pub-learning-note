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
 - Master-Slave Replication 是允許一台主要資料庫伺服器將特定資料複製成副本分給多個資料庫系統上的資料庫來儲存，以此讓多個資料庫系統共享同份資料，並由主要資料庫伺服器進行資料上的維護&管理
 - 在這裡負責提供資料副本的資料庫伺服器是master主機，接收到副本的資料庫伺服器是slave主機
 - 在擁有同份資料的情況下，master主機會擁有讀取資料、寫入資料、以目前資料內容作為副本傳遞至其他主機上。slave 主機只會有讀取資料的權限
 - 技術細節：
	 - Slave 主機可以切分額外的Slave子結構
	 - 如果master主機離線，同份資料的存取就僅剩下讀取，除非有slave主機承擔起master主機或者有新的master主機加入。
- 可應用於
	- Read/Write Splitting 場景



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
- replication lag：是指當master主機的資料庫系統上發生資料更改、寫入時，從資料一被更改到資料複製到slave主機且讓slave主機採用的時間差。

## 複習


---
Status: #🌱 
Tags
[[Database]]
Links:
[[Database Replication  是將資料進行同結構同內容的複製來製作成多個副本分發至其他系統上]]
[[Read-Write Splitting 是指在多個主機共享同個資料庫資料的情況下專門提供專門讀取資料的主機和專門寫資料的主機]]
References:
[[@mariadbDatabaseMasterSlaveReplication2013]]
[[@karanpratansinghSystemDesignComplete]]
[[@developpaperMySQLMasterslaveReplication]]