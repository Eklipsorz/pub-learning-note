## 描述


### Master-Slave Replication
[[@karanpratansinghSystemDesignComplete]]

> ## Master-Slave Replication

> The master serves reads and writes, replicating writes to one or more slaves, which serve only reads. Slaves can also replicate additional slaves in a tree-like fashion. If the master goes offline, the system can continue to operate in read-only mode until a slave is promoted to a master or a new master is provisioned.

![](https://raw.githubusercontent.com/karanpratapsingh/portfolio/master/public/static/courses/system-design/chapter-II/database-replication/master-slave-replication.png)

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

## 複習


---
Status: #🌱 
Tags
[[Database]]
Links:
[[Database Replication  是將資料進行同結構同內容的複製來製作成多個副本分發至其他系統上]]
References:
[[@karanpratansinghSystemDesignComplete]]