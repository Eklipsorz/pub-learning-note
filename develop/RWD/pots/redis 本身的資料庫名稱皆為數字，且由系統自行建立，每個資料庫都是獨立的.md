
## 描述

引用[[@putianRedisZiLiaoKuDeAnZhuangYuJiChuMingLing]]所描述
> ### 多資料庫概念

> Redis支援多個資料庫，並且每個資料庫的資料是隔離的不能共享，並且基於單機才有，如果是叢集就沒有資料庫的概念。  

> Redis是-個字典結構的儲存伺服器，而實際上-個Redis例項提供了 多個用來儲存資料的字典，  
> 客戶端可以指定將資料儲存在哪個字典中。這與我們熟知的在一個關聯式資料庫例項中可以建立多個資料庫類似,  
> 所以可以將其中的每個字典都理解成一個獨立的資料庫。  
> 每個資料庫對外都是一個從0開始的遞增數字命名，Redis預設支援16個資料庫(可以通過配置檔案支援更多，無上限) ,  
> 可以通過配置databases來修改這一數字. 客戶端與Redis建立連線後會自動選擇0號資料庫,


引用[[@oreillyMultipleRedisDatabases]]所描述
> Redis comes with support for multiple databases, which is very similar to the concept in SQL databases. In SQL databases, such as MySQL, PostgreSQL, and Oracle, you can define a name for your databases. However, Redis databases are represented by numbers.

引用[[@dhruvpathakHowCreateOwn2016]]所描述的：具體是能不能自行建立資料庫
> You don't create a database in Redis with a command - the number of databases is defined in the configuration file with the databases directive (the default value is 16). To switch between the databases, call SELECT.

重點：
- Redis 可以建立多個獨立的資料庫，但資料庫名稱只能以數字來代表，不能夠像其他資料庫系統以特定字串來取名
- Redis 上不允許使用者建立資料庫，其資料庫系統會按照設定檔案所指示的資料庫數量多寡來事先建立資料庫，每個資料庫名稱皆為：
	- 資料庫名稱皆為數字，每一個資料庫所拿到的數字都是獨立且不同
	- 從0這個數字開始分配，接著分配完就從1分配，後續就按照+1的遞增速率來分配，
	- 預設上，redis會有16個資料庫，所以名稱會是0-15
- 預設上，若沒在客戶端指定與哪個資料庫進行連線，會是指定0號資料庫

## 複習

#🧠 Redis 可以擁有多個資料庫嗎？ 每個資料庫都是獨立的？->->-> `可以擁有，每個資料庫都是獨立`
<!--SR:!2022-12-04,113,250-->

#🧠 使用者可以自行在Redis建立資料庫嗎？ ->->-> `Redis 上不允許使用者建立資料庫`
<!--SR:!2023-03-28,187,250-->

#🧠 若使用者不能在Redis自行建立資料庫，那誰能夠增加？其名稱為何->->-> `預設上，會是由Redis本身按照設定檔案來建立多個資料庫，每個資料庫名稱都皆為數字，若指定建立3個，那就會是0-2這個三個數字來分配三個資料庫名稱`
<!--SR:!2023-02-26,166,250-->

#🧠 Redis: 若沒在客戶端指定與哪一個資料庫進行連線，會指定哪個資料庫 ->->-> `預設上，若沒在客戶端指定與哪個資料庫進行連線，會是指定0號資料庫`
<!--SR:!2022-09-26,72,250-->


---
Status: #🌱 
Tags:
[[Redis]] 
Links:
References:
[[@dhruvpathakHowCreateOwn2016]]
[[@oreillyMultipleRedisDatabases]]
[[@dhruvpathakHowCreateOwn2016]]
[[@putianRedisZiLiaoKuDeAnZhuangYuJiChuMingLing]]