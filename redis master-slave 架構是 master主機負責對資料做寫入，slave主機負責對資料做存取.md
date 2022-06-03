## 描述

引用[[@feixiangdezhuRedisZhuCongMoShi]]所描述：
>   主（master）和 从（slave）部署在不同的服务器上，当主节点服务器写入数据时会同步到从节点的服务器上，一般主节点负责写入数据，从节点负责读取数据

![](https://pic2.zhimg.com/80/v2-5d1ddfcf9745f441c44222fda257f72d_720w.jpg)

引用[[@tienyuRedisLiuZhuCongFuZhi]]所描述：
> 主從複製模式提供讓 Master(主伺服器) 向任意數量的 Slave(附屬伺服器) 進行資料同步，以解決單點資料庫的問題。

> 主從複製模式最主要的目的是要實現讀寫分離和資料備份。Redis 讀寫分離的作法是 Master 可以進行讀取和寫入，其他的 Slave 只能讀取。透過 Slave 幫忙處理讀取的工作來減輕 Master 的負擔。

![](https://i.imgur.com/GLSvDQu.png)


## redis master-slave 架構優點
引用[[@feixiangdezhuRedisZhuCongMoShi]]所描述：
> 读写分离，提高效率
> 数据热备份，提供多个副本

## 複習
#🧠 Question :: ->->-> ``

---
Status: #🌱 
Tags:
[[Redis]] - [[master-slave]]
Links:
References:
[[@tienyuRedisLiuZhuCongFuZhi]]
[[@feixiangdezhuRedisZhuCongMoShi]]
