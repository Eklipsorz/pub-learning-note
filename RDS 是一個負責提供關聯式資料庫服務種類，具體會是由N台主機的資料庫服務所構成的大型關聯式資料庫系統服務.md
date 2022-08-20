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
- RDS 是指Relational Database Service，是一個負責管理的主機，主要管理雲端上的關聯式資料庫服務主機。
- 體是由RDS本身是，管理著以下種類的主機
	- N台(虛擬)主機的資料庫服務
	- 
- 資料上的管理、組織、維護都是由每個資料庫服務上的處理核心來負責
- 1個RDS實例的構成可以是由1個虛擬主機或者1個實體主機所構成

## 複習
#🧠 RDS 是什麼服務？以資料庫來說 ->->-> `是一個負責處理提供關聯式資料庫的服務種類`

#🧠  資料庫：RDS的全名是什麼？ ->->-> `Relational Database Service`

#🧠 RDS中誰負責資料實際上的管理、組織、維護 ->->-> `RDS每台主機下的每個資料庫處理核心來處理`

#🧠 RDS 是一個負責處理關連式資料庫請求的服務主機，具體如何構成？ ->->-> `由N台(虛擬)主機的資料庫服務所構成的大型關聯資料庫系統服務，資料上的管理、組織、維護都是由每個資料庫服務上的處理核心來負責`

#🧠 每一個RDS實例的構成可以是？ ->->-> `可以是由1個虛擬主機或者1個實體主機所構成`

---
Status: #🌱 
Tags:
[[Database]]
Links:
References:
[[@benlutkevichWhatAmazonRDS]]
[[@wikidataAmazonRelationalDatabase2022]]
[[@xiongbenxiongbenxiongFengSiXin74TiaoXiaoXi]]