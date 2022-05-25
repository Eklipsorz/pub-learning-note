## 描述

引用[[@yunshu_youpaiyunRedisCunChuDuiXiangXinXiShiYongHash]]所描述的 hash: 
> 在 Redis 中，Hash 常常用来缓存一些对象信息，如用户信息、商品信息、配置信息等，因此也被称为字典（dictionary），Redis 的字典使用 Hash table 作为底层实现， 一个 Hash table 里面可以有多个哈希表节点，而每个哈希表节点保存了字典中的一个键值对。实际上，Redis 数据库底层也是采用 Hash table 来存储键值对的。

> 前面说到 String 适合存储用户信息，而 Hash 结构也可以存储用户信息，不过是对每个字段单独存储，因此可以在查询时获取部分字段的信息

重點：
- redis 的hash實際上是字典結構
- hash上的每一個元素皆為key-value pair
- 相較於String而言，hash可以將資料細分好幾個區塊來儲存，而String則是一股腦兒儲存整塊資料，假如使用者資訊是由年齡、身高、性別、名稱、電話所構成，字串就直接儲存一個大字串來包含這些內容
	```
	年齡：身高：性別：名稱：電話
	```
	而字典則是將資料細分成年齡、身高、性別、名稱、電話來分別儲存這五個
	```
	年齡： <年齡>
	身高： <身高>
	性別： <性別>
	名稱： <名稱>
	電話： <電話>
	```



## 複習
#🧠 redis hash 是怎麼樣的型別->->-> `redis 的hash實際上是字典結構，字典上的每一個元素皆為key-value pair，每一個key都會對應特定的value。`

#🧠 redis hash 是賦予給誰的型別？ ->->-> `具體來說redis來說，它是一種以key-value pair為基本資料型態來儲存的資料庫，所以key通常會是字串或者數字，而value則是任意型別，hash則是可指定value的型別之一`

#🧠 redis hash vs. string 兩者間是如何儲存資料的？->->-> `較於String而言，hash可以將資料細分好幾個區塊來儲存，而String則是一股腦兒儲存整塊資料。`

---
Status: #🌱 
Tags:
[[Redis]]-[[Data Structure]]
Links:
[[dictionary 是如同字典一般儲存多個key-value pairs，key會是關鍵字，value則是解釋關鍵字的描述]]
References: