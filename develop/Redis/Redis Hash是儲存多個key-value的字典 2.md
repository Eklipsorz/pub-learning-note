## 描述

引用[[@yunshu_youpaiyunRedisCunChuDuiXiangXinXiShiYongHash]]所描述的 hash: 
> 在 Redis 中，Hash 常常用来缓存一些对象信息，如用户信息、商品信息、配置信息等，因此也被称为字典（dictionary），Redis 的字典使用 Hash table 作为底层实现， 一个 Hash table 里面可以有多个哈希表节点，而每个哈希表节点保存了字典中的一个键值对。实际上，Redis 数据库底层也是采用 Hash table 来存储键值对的。

> 前面说到 String 适合存储用户信息，而 Hash 结构也可以存储用户信息，不过是对每个字段单独存储，因此可以在查询时获取部分字段的信息

重點：
- redis 的hash實際上是字典結構
- hash上的每一個元素皆為key-value pair，hash上的key和value皆為字串
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

### 如何在 hash 結構上存取資料
如同[[dictionary 是如同字典一般儲存多個key-value pairs，key會是關鍵字，value則是解釋關鍵字的描述]]以及[[@RedisCunjsonZiLiaoShiXuanZestringHuanShihash]]所描述的hash操作
> -   hash型別：
	>   1.   取資料：根據redis鍵，然後遍歷整個hash鍵值對（相對string的取資料更加耗時）。
    >   2.  存資料：根據redis鍵，在value出存鍵值對
    >   3. 更新資料：根據redis鍵和hash key更新對應的資料

重點：由於key所對應的value會是一個hash table，在這裡會簡稱為hash
- 讀取資料：根據key值和其對應hash上的key值來讀取對應的value
- 寫入資料：根據key值和其對應hash上的key值來寫入對應的value
- 更新資料：根據key值和其對應hash上的key值來更新對應的value
- 刪除資料：根據key值和其對應hash上的key值來刪除指定的key-value pair(在hash上的key-value pair)

## 複習
#🧠 redis hash 是怎麼樣的型別->->-> `redis 的hash實際上是字典結構，字典上的每一個元素皆為key-value pair，每一個key都會對應特定的value。`
<!--SR:!2022-10-23,91,250-->

#🧠 redis hash 是賦予給誰的型別？ ->->-> `具體來說redis來說，它是一種以key-value pair為基本資料型態來儲存的資料庫，所以key通常會是字串，而value則是任意型別，hash則是可指定value的型別之一`
<!--SR:!2022-10-22,97,270-->

#🧠 redis hash vs. string 兩者間是如何儲存資料的？->->-> `較於String而言，hash可以將資料細分好幾個區塊來儲存，而String則是一股腦兒儲存整塊資料。`
<!--SR:!2022-11-03,83,210-->

#🧠 redis 如何在 hash 結構上存取資料? CRUD為？->->-> `讀取資料：根據key值和其對應hash上的key值來讀取對應的value，寫入資料：根據key值和其對應hash上的key值來寫入對應的value，更新資料：根據key值和其對應hash上的key值來更新對應的value，根據key值和其對應hash上的key值來刪除指定的key-value pair(在hash上的key-value pair)`
<!--SR:!2022-10-13,91,270-->

#🧠 redis： 為什麼string可以運用在處理大部分屬性值的操作上？為何不使用hash ->->-> `因爲比起使用hash來一個一個挑選屬性來找，不如直接一口氣獲取全部屬性值，然後去除不必要的屬性來會來得快`
<!--SR:!2022-09-18,27,250-->

---
Status: #🌱 
Tags:
[[RedisJSON 讓Redis 伺服器能夠以JSON形式來處理每個key上的value]]-[[Data Structure]]
Links:
[[dictionary 是如同字典一般儲存多個key-value pairs，key會是關鍵字，value則是解釋關鍵字的描述]]
References:
[[@RedisCunjsonZiLiaoShiXuanZestringHuanShihash]]