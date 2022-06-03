## 描述

引用[[@feixiangdezhuRedisZhuCongMoShi]]所描述：
>   主（master）和 从（slave）部署在不同的服务器上，当主节点服务器写入数据时会同步到从节点的服务器上，一般主节点负责写入数据，从节点负责读取数据

![](https://pic2.zhimg.com/80/v2-5d1ddfcf9745f441c44222fda257f72d_720w.jpg)

引用[[@tienyuRedisLiuZhuCongFuZhi]]所描述：
> 主從複製模式提供讓 Master(主伺服器) 向任意數量的 Slave(附屬伺服器) 進行資料同步，以解決單點資料庫的問題。

> 主從複製模式最主要的目的是要實現讀寫分離和資料備份。Redis 讀寫分離的作法是 Master 可以進行讀取和寫入，其他的 Slave 只能讀取。透過 Slave 幫忙處理讀取的工作來減輕 Master 的負擔。

![](https://i.imgur.com/GLSvDQu.png)


重點：
- 主從架構是由一個master主機和多個slave主機所構成，每個主機都是redis資料庫系統，
- master主機來主要負責控管資料上變更和存取，而slave則是接收從master主機所儲存的資料進行同步，從而透過這些主機來共同持有同一個redis資料庫
- 開始建構架構時，一開始會由master主機負責建立對應的redis資料庫A，並拿資料庫A的資料對其他slave主機進行資料庫的同步，換言之，讓slave主機的redis 資料庫內容會是資料庫A的內容
- master 主機負責的業務：
	- 與slave的資料庫同步：主要提供自己的redis 資料庫來同步slave主機上的redis資料庫
	- 架構上唯一負責對資料庫寫入的主機：由於是從自己redis 資料庫來共享，且考慮資料一致性的問題，所以會設定只有master主機能夠寫入
	- 架構上負責對資料庫讀取的主機
- slave 主機負責的業務：
	- 架構上負責對資料庫讀取的主機
## redis master-slave 架構優點
引用[[@feixiangdezhuRedisZhuCongMoShi]]所描述：
> 读写分离，提高效率
> 数据热备份，提供多个副本

重點：
- 

## 複習
#🧠 Question :: ->->-> ``


### note
1. 讀寫分離英文為Read/Write Splitting
2. 


---
Status: #🌱 
Tags:
[[Redis]] - [[master-slave]]
Links:
References:
[[@tienyuRedisLiuZhuCongFuZhi]]
[[@feixiangdezhuRedisZhuCongMoShi]]
