## 描述

[[@wikidataAmazonRelationalDatabase2022]]
> It is a web service running "in the cloud" designed to simplify the setup, operation, and scaling of a relational database for use in applications


[[@xiongbenxiongbenxiongFengSiXin74TiaoXiaoXi]]
> RDS（Relational DataBase Service）中文译为关系型数据库服务，也就是我们常说的“云数据库”。从名字可以看出，RDS 的本质是基于关系型数据库搭建的服务体系，底层可以是各种开源的关系型数据库，比如 MySQL，也可以是各公司自研的数据库产品。


[[@benlutkevichWhatAmazonRDS]]
> Amazon Relational Database Service (RDS) is a managed SQL database service provided by Amazon Web Services (AWS). Amazon RDS supports an array of database engines to store and organize data. It also helps with relational database management tasks, such as data migration, backup, recovery and patching.

> Amazon RDS facilitates the deployment and maintenance of relational databases in the cloud. A cloud administrator uses Amazon RDS to set up, operate, manage and scale a relational instance of a cloud database. 
> 
> Amazon RDS is not itself a database; it is a service used to manage relational databases.

重點：
- RDS 是指Relational Database Service，概念上是提供關係式資料庫服務的雲端服務
- 具體是一個負責管理的服務主機，主要管理多台已架設關聯式資料庫服務的虛擬主機。
- 負責管理的主機業務內容：
	- 負責接收請求方的資料庫請求
	- 委派資料庫請求至適合的虛擬主機
	- 將處理結果回傳給請求方
![](https://miro.medium.com/max/1400/1*IDQ1KqkHYWwnwtioleYcNw.png)
- 資料上的實際管理、組織、維護都是由每個資料庫服務上的處理核心來負責
- 每一個被RDS所管理的主機，被稱之為RDS 實例(Instance) 

## 複習
#🧠 RDS 是什麼服務？以資料庫來說 ->->-> `提供關係式資料庫服務的雲端服務`

#🧠  資料庫：RDS的全名是什麼？ ->->-> `Relational Database Service`

#🧠 RDS 具體是什麼服務？ ->->-> `是一個負責管理的服務主機，主要管理多台已架設關聯式資料庫服務的虛擬主機`

#🧠 RDS 具體是是一個負責管理的服務主機，主要管理多台已架設關聯式資料庫服務的虛擬主機，其管理主機的業務有哪些？ ->->-> `	- 負責接收請求方的資料庫請求 - 委派資料庫請求至適合的虛擬主機 - 將處理結果回傳給請求方`

#🧠 RDS中誰負責資料實際上的管理、組織、維護 ->->-> `RDS每台主機下的每個資料庫處理核心來處理`


#🧠 每一個被RDS所管理的主機被稱之為什麼？ ->->-> `RDS 實例(Instance) `

---
Status: #🌱 
Tags:
[[Database]]
Links:
References:
[[@benlutkevichWhatAmazonRDS]]
[[@wikidataAmazonRelationalDatabase2022]]
[[@xiongbenxiongbenxiongFengSiXin74TiaoXiaoXi]]