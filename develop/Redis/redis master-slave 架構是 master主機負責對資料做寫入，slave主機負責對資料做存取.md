## 描述

引用[[@feixiangdezhuRedisZhuCongMoShi]]所描述：
>   主（master）和 从（slave）部署在不同的服务器上，当主节点服务器写入数据时会同步到从节点的服务器上，一般主节点负责写入数据，从节点负责读取数据

![](https://pic2.zhimg.com/80/v2-5d1ddfcf9745f441c44222fda257f72d_720w.jpg)

引用[[@tienyuRedisLiuZhuCongFuZhi]]所描述：
> 主從複製模式提供讓 Master(主伺服器) 向任意數量的 Slave(附屬伺服器) 進行資料同步，以解決單點資料庫的問題。

> 主從複製模式最主要的目的是要實現讀寫分離和資料備份。Redis 讀寫分離的作法是 Master 可以進行讀取和寫入，其他的 Slave 只能讀取。透過 Slave 幫忙處理讀取的工作來減輕 Master 的負擔。

![](https://i.imgur.com/GLSvDQu.png)


重點：
- 主從架構是由一個master主機和多個slave主機所構成，每個主機都是redis資料庫系統
- master主機來主要負責控管資料上變更和存取，而slave則是接收從master主機所儲存的資料進行同步，從而透過這些主機來共同持有同一個redis資料庫
- 開始建構架構時，一開始會由master主機負責建立對應的redis資料庫A，並拿資料庫A的資料對其他slave主機進行資料庫的同步，而同步方式為hot backup，換言之，master主機和slave主機所共享的資料會實時更新，不會出現版本的問題
- master 主機負責的業務：
	- 與slave的資料庫同步：主要提供自己的redis 資料庫來同步slave主機上的redis資料庫
	- 架構上唯一負責對資料庫寫入的主機：由於是從自己redis 資料庫來共享，且考慮資料一致性的問題，所以會設定只有master主機能夠寫入
	- 架構上負責對資料庫讀取的主機：可藉由開發給人讀取來平攤緩存上的讀取請求負載
- slave 主機負責的業務：
	- 架構上負責對資料庫讀取的主機：可藉由開發給人讀取來平攤緩存上的讀取請求負載
## redis master-slave 架構優點
引用[[@feixiangdezhuRedisZhuCongMoShi]]所描述：
> 读写分离，提高效率
> 数据热备份，提供多个副本

重點：
- 優點是可以實現讀寫分離：負責幫助開發者進行寫入資料庫和讀取資料庫的伺服器都是不同的，從而平均分攤資料庫的壓力
- 由於同步方式是採用hot backup，所以每個主機的資料庫都是一致，所以當其中一個主機無法正常服務時，可以由其他正常的主機來頂替。

## redis master-slave 架構缺點
引用[[@feixiangdezhuRedisZhuCongMoShi]]所描述：
> 主节点故障，集群则无法进行工作，可用性比较低，从节点升主节点需要人工手动干预
> 单点容易造成性能低下
> 主节点的写受到限制（只有一个主节点）


重點：
- master主機故障時，master主機所建構的結構將會因為無法共享資料而失效，需要人工修復
- 寫入時只有一個master主機，所以寫入效能會有所限制
## 複習
#🧠 redis 的 主從架構是什麼？->->-> `主從架構是由一個master主機和多個slave主機所構成，每個主機都是redis資料庫系統，master主機來主要負責控管資料上變更和存取，而slave則是接收從master主機所儲存的資料進行同步，從而透過這些主機來共同持有同份資料`
<!--SR:!2024-11-20,498,248-->


#🧠 redis 的 主從架構剛開始建立時，結構上的主機是如何共享同一個資料？(盡量提到hot backup) ->->-> `-   開始建構架構時，一開始會由master主機負責建立對應的redis資料庫A，並拿資料庫A的資料對其他slave主機進行資料庫的同步，而同步方式為hot backup，換言之，master主機和slave主機所共享的資料會實時更新，不會出現版本的問題`
<!--SR:!2024-05-26,439,250-->

#🧠 redis 主從架構下的master 主機負責的業務是什麼->->-> `1. 負責處理同份資料的讀取請求/處理同份資料的寫入請求 2. 負責讓所有資料庫系統都擁有一樣的資料`
<!--SR:!2023-10-18,248,248-->



#🧠  redis 主從架構下的slave 主機負責的業務是什麼->->-> `1. 負責處理同份資料的讀取請求`
<!--SR:!2023-12-01,280,248-->


#🧠 redis master-slave 架構優點: ->->-> `優點是可以實現讀寫分離和熱備份機制`
<!--SR:!2024-07-04,300,208-->

#🧠  redis master-slave 架構如何實現讀寫分離(權限和使用者能用誰)？->->-> `master主機來主要負責控管資料上變更和存取，而slave則是接收從master主機所儲存的資料進行同步，從而透過這些主機來共同持有同一個redis資料庫，並且只賦予寫權限給master主機，讀權限則賦予master主機和slave主機`
<!--SR:!2025-02-04,582,248-->

#🧠   redis master-slave 架構上的master和slave之間的同步是什麼(提示：hot? warm? cold?) ？說明一下那種同步是指？->->-> `熱備份機制，具體來說當master主機的資料一發生變化就會同步至其他slave主機的資料庫，以此達到共享`
<!--SR:!2025-05-27,649,248-->

#🧠 redis (沒sentinel mode情況下) master-slave 架構缺點: (提示故障時可用性和寫入)->->-> `master主機故障時，master主機所建構的結構將會因為無法共享資料而失效，需要人工修復、寫入時只有一個master主機，所以寫入效能會有所限制`
<!--SR:!2024-12-23,531,230-->

### note
1. 讀寫分離英文為Read/Write Splitting



---
Status: #🌱 
Tags:
[[Redis]] - [[master-slave]]
Links:
References:
[[@tienyuRedisLiuZhuCongFuZhi]]
[[@feixiangdezhuRedisZhuCongMoShi]]
