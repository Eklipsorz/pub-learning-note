## 描述

### String vs. Hash

#### 記憶體成本
記憶體成本：
- 以String作為Value的成本，相較於Hash，比較單純且比較少
- 以Hash作為Value的成本，相較於String，比較繁複且由於將資料切分開來儲存，每個要儲存的形式又是以key-value的形式，所以成本上會比較多

#### 表示多個屬性值資料的形式
表示存在多個屬性值的資料的形式：
- 以String來說的話，主要可以是將所有屬性值合併一個新字串，如下圖由key對應新字串
```
key -> <property1>:value1,<property2>:value2,<property3>:value3,...
```

- 以String來說的話，除了上述的方法，還有根據屬性額外建立key-value pair
```
key:<property1> -> value1
key:<property2> -> value2
key:<property3> -> value3
.
.
```

- 以Hash來說的話，會直接建立一個dictionary來儲存那些屬性值

```
key -> dictionary
```

#### 修改特定資料上的特定屬性
修改特定資料上特定屬性：若資料本身有多個屬性的屬性值
- 以String來說的話，若是採用主要可以將所有屬性值合併一個新字串，要修改特定屬性的值，就必須為了那個值，而將整筆資料都複製一份並刪除原本指定的屬性值，接著將新屬性值合併成一個新字串，比如說使用者資料有名字、性別、電話，假設原資料為
```
小明：男：0102103131
```
但若想修改小明的電話，理論上就只修改電話的值，但String沒獨立存放，因此只能先將先複製一份，從字串中刪掉舊電話，接著將新電話在與刪除後的字串合併，
```
小明：男：1234567890
```
- 以String來說的話，若是將key值和屬性名稱作為新key以及對應屬性值的話，就直接針對key和屬性名稱對應的屬性值來修改。
- 以Hash來說的話，要修改特定屬性的值，由於會將資料切分成好幾分獨立的部分來儲存，每個又是以key-value pair來表示，所以只要指定對應key就能直接修改

#### 新增特定資料上的特定屬性
新增特定屬性值至特定資料：若資料本身有多個屬性的屬性值
- 以String來說的話，若是採用主要可以將所有屬性值合併一個新字串，要修改特定屬性值，就必須為了那個值，而將原資料都複製一份並與新屬性值合併成一個新字串

- 以String來說的話，若是將key值和屬性名稱作為新key以及對應屬性值的話，就直接真對key和新屬性名稱來新增對應屬性值

- 以Hash來說的話，要新增特定資料上的特定屬性，就只需要指定hash 上key值就能直接新增

#### 刪除特定資料上的特定屬性
刪除特定資料上的特定屬性：若資料本身有多個屬性值
- 以String來說的話，若是採用主要可以將所有屬性值合併一個新字串，要刪除特定屬性值，就必須為了那個值，而將原資料都複製一份並刪去該屬性值來當作新字串來修改
- 以String來說的話，若是將key值和屬性名稱作為新key以及對應屬性值的話，就直接對key和屬性名稱來刪除對應的key-value pair
- 以Hash來說的話，要刪除特定資料上的特定屬性，就只需要指定hash上key值就能直接刪除


#### 讀取特定資料上的特定屬性
讀取特定資料上的特定屬性值：若資料本身有多個屬性的屬性值
- 以String來說的話，若是採用主要可以將所有屬性值合併一個新字串，要讀取特定屬性值，就必須為了那個值，將原資料都複製一份並刪去除了特定屬性值以外的屬性值來回傳。
- 以String來說的話，若是將key值和屬性名稱作為新key以及對應屬性值的話，就直接指定key和屬性名稱來回傳對應的value
- 以Hash 來說的話，要讀取特定資料上的特定屬性，就只需要指定hash上key值就能直接讀取該value

#### 對特定資料上的所有屬性進行操作
新增讀取/修改/刪除(擁有多個屬性值)整個特定資料的話
- 以String來說，就直接更改value值，不需要指定key來進行操作
- 以Hash來說，就必須指定每個key來進行操作


### 適用場景：String vs. Hash 
引用[[@RedisCunjsonZiLiaoShiXuanZestringHuanShihash]]所描述的場景：
> -   如果你的業務型別中對於快取的讀取快取的場景更多，並且更新快取不頻繁（或者每次更新都更新json資料中的大多數key），那麼選擇string型別作為儲存方式會比較好。
> -   如果你的業務型別中對於快取的更新比較頻繁（特別是每次只更新少數幾個鍵）時， 或者我們每次只想取json資料中的少數幾個鍵值時，我們選擇hash型別作為我們的儲存方式會比較好。
以及根據[[@yunshu_youpaiyunRedisCunChuDuiXiangXinXiShiYongHash]]所描述的：
> **适合用 String 存储的情况：**
>-   每次需要访问大量的字段
>-   存储的结构具有多层嵌套的时候
>**适合用 Hash 存储的情况：**
>-   在大多数情况中只需要访问少量字段
>-   自己始终知道哪些字段可用，防止使用 mget 时获取不到想要的数据

String 適用場景為：
- String 本身會是以單一值來存取，若是資料有多個屬性且用多個屬性值合併成一個單一值string，那麼會適用於存取大部分屬性的場景，因為獲取全部屬性會比呼叫一個屬性獲取來得更有效率


Hash 適用場景為：
- 清楚理解哪些key-value是可用的(否則會讀取到錯誤值或者空值)
- 更新較為頻繁，尤其是指定特定key值
- 讀取特定少量的key值
(理由是Hash是將資料切分成更細的key-value pair，所以可以透過key來對特定value進行操作)

#### String 應用案例
引用[[@yudiandemingziTanTanRedisWuZhongShuJuJieGouJiZhenShiYingYongChangJingYuDianDeMingZiBoKeYuan]]所描述：
> (1) `存储一些配置数据`
在前后分离式开发中，有些数据虽然存储在数据库，但是更改特别少。比如有个`全国地区表`。当前端发起请求后，后台如果每次都从关系型数据库读取，会影响网站整体性能。

> 我们可以在第一次访问的时候，将所有地区信息存储到redis字符串中，再次请求，直接从数据库中读取地区的json字符串，返回给前端。

> (2) `缓存对象`
> 将对象转为json存储，比如商品信息，用户信息。

> (3) `数据统计`
> redis整型可以用来记录网站访问量，某个文件的下载量,签到人数、视频访问量等等。（`自增自减`）

> (4) `时间内限制请求次数`
> 比如已登录用户请求短信验证码，验证码在5分钟内有效的场景。  当用户首次请求了短信接口，将用户id存储到redis 已经发送短信的字符串中，并且设置过期时间为5分钟。当该用户再次请求短信接口，发现已经存在该用户发送短信记录，则不再发送短信。


> (6) `分布式session`
> 当我们用nginx做负载均衡的时候，如果我们每个从服务器上都各自存储自己的session，那么当切换了服务器后，session信息会由于不共享而会丢失，我们不得不考虑第三应用来存储session。 通过我们用关系型数据库或者Redis等非关系型数据库。关系型数据库存储和读取性能远远无法跟Redis等非关系型数据库比。

重點：應用案例為
- 儲存執行環境上的環境變數、功能上所需要預載的資料，如一張顯示各地區的郵遞區號
- 將物件轉換為JSON 格式字串，比如商品資訊、使用者資訊
- 資料統計：如紀錄網站訪問量、某文件的下載量、喜歡數
- 時間內限制請求次數：比如說用戶請求發送短信驗證碼後，就不允許用戶在五分鐘內重新發送請求驗證碼。所以當用戶請求發送，伺服器便會紀錄該用戶的ID儲存在redis到已經發送短信內的亂數字串，並設定過期時間為5分鐘，接著用戶發送請求，伺服器就會依據userId來從redis找到對應字串，若找得到就不允許重複發送
```
// example 1: key -> value
userId -> 短信亂數字串
// example 2: key -> value
```
- 儲存 session ，替分散式系統集中管理/儲存session
	- 分散式系統是指由多個主機來擔任伺服器，但由於session本身是出自單個主機來生成和管理，所以無法跨主機，需要有個集中資料的主機，也就是redis主機


#### Hash 應用案例
引用[[@yudiandemingziTanTanRedisWuZhongShuJuJieGouJiZhenShiYingYongChangJingYuDianDeMingZiBoKeYuan]]所描述：
> `购物车列表`
> 以_用户id为key_，_商品id为field_，_商品数量为value_，恰好构成了购物车的3个要素，如下图所示。

![](https://img2020.cnblogs.com/blog/1090617/202112/1090617-20211209211822193-1510156486.png)


重點：
- 購物車下會有的產品清單

## 複習


#🧠  Redis 記憶體成本: string vs. hash ->->-> `以String作為Value的成本，相較於Hash，比較單純且比較少；以Hash作為Value的成本，相較於String，比較繁複且由於將資料切分開來儲存，每個要儲存的形式又是以key-value的形式，所以成本上會比較多`
<!--SR:!2023-09-15,288,250-->

#🧠 Redis上 string 和 hash 分別如何表示存在多個屬性值的資料的形式(提示：string有兩個方法，hash有一個方法)->->-> `string主要有兩個方法分別為將多個屬性值組合一個字串作為value，或者將key與屬性名稱構成新的key，然後其value為對應key上的特定屬性值；hash就直接以dictionary來製作多個key-value pairs就即可完成`
<!--SR:!2024-03-10,394,250-->

#🧠 Redis 上 string 和hash 分別如何一次性修改(擁有多個屬性值)資料上的特定屬性 ->->-> ` 以String來說的話，若是採用主要可以將所有屬性值合併一個新字串，要修改特定屬性的值，就必須為了那個值，而將整筆資料都複製一份並刪除原本指定的屬性值，接著將新屬性值合併成一個新字串；若還是String的話，但這次是將key值和屬性名稱作為新key以及對應屬性值的話，就直接針對key和屬性名稱對應的屬性值來修改；以Hash來說的話，要修改特定屬性的值，只要指定對應key和hash key就能直接修改`
<!--SR:!2025-04-16,664,270-->

#🧠 Redis 上 string 和hash分別如何一次性新增(擁有多個屬性值)資料上的特定屬性 ->->-> `以String來說的話，若是採用主要可以是將所有屬性值合併一個新字串，要修改特定屬性值，就必須為了那個值，而將原資料都複製一份並與新屬性值合併成一個新字串；若是將key值和屬性名稱作為新key以及對應屬性值的話，就直接真對key和新屬性名稱來新增對應屬性值；以Hash來說的話，要修改特定屬性的值，只要指定對應key和hash key就能直接新增`
<!--SR:!2023-12-20,345,250-->

#🧠 Redis 上 string 和hash分別如何一次性刪除(擁有多個屬性值)資料上的特定屬性 ->->-> `以String來說的話，若是採用主要可以將所有屬性值合併一個新字串，要刪除特定屬性值，就必須為了那個值，而將原資料都複製一份並刪去該屬性值來當作新字串來修改；若是將key值和屬性名稱作為新key以及對應屬性值的話，就直接對key和屬性名稱來刪除對應的key-value pair；以Hash來說的話，要刪除特定資料上的特定屬性，就只需要指定hash上key值就能直接刪除`
<!--SR:!2024-03-30,408,250-->

#🧠 Redis 上 string 和hash分別如何一次性讀取(擁有多個屬性值)資料上的特定屬性->->-> `以String來說的話，若是採用主要可以將所有屬性值合併一個新字串，要讀取特定屬性值，就必須為了那個值，將原資料都複製一份並刪去除了特定屬性值以外的屬性值來回傳；若是將key值和屬性名稱作為新key以及對應屬性值的話，就直接指定key和屬性名稱來回傳對應的value；以Hash 來說的話，要讀取特定資料上的特定屬性，就只需要指定hash上key值就能直接讀取該value`
<!--SR:!2025-06-22,675,250-->

#🧠 Redis 上 string 和 hash 分別如何一次性處理新增/讀取/修改/刪除資料上的所有屬性 ->->-> `以String來說，就直接更改value值，不需要指定key來進行操作；以Hash來說，就必須指定每個key來進行操作`
<!--SR:!2023-12-06,148,231-->


#🧠 redis 上的string適用場景？ 理由是？ ->->-> ` String 本身會是以單一值來存取，若是資料有多個屬性且用多個屬性值合併成一個單一值string，那麼會適用於存取大部分屬性的場景，因為獲取全部屬性會比呼叫一個屬性獲取來得更有效率`
<!--SR:!2024-01-02,194,231-->

#🧠  redis 上的Hash 適用場景為？理由是？ ->->-> `清楚理解哪些key-value是可用的(否則會讀取到錯誤值或者空值)、 更新較為頻繁，尤其是指定特定key值、讀取特定少量的key值，理由是Hash是將資料切分成更細的key-value pair，所以可以透過key來對特定value進行操作)`
<!--SR:!2024-09-14,492,251-->

#🧠 請列舉Redis 上的string能應用到什麼樣的功能(提示：環境變數、JSON字串、統計資料、時間內限制請求次數、儲存session和分散式系統下的資料)  ->->-> `1. 儲存執行環境上的環境變數、功能上所需要預載的資料，如一張顯示各地區的郵遞區號。2.將物件轉換為JSON 格式字串，比如商品資訊、使用者資訊。3. 資料統計：如紀錄網站訪問量、某文件的下載量、喜歡數。4. 時間內限制請求次數：比如說用戶請求發送短信驗證碼後，就不允許用戶在五分鐘內重新發送請求驗證碼。所以當用戶請求發送，伺服器便會紀錄該用戶的ID儲存在redis到已經發送短信內的亂數字串，並設定過期時間為5分鐘，接著用戶發送請求，伺服器就會依據userId來從redis找到對應字串，若找得到就不允許重複發送 5. 儲存 session ，替分散式系統集中管理/儲存session`
<!--SR:!2023-09-26,26,191-->


#🧠 (重複) 請列舉Redis 上的string能應用到什麼樣的功能(提示：環境變數、JSON字串、統計資料、時間內限制請求次數、儲存session和分散式系統下的資料)  ->->-> `1. 儲存執行環境上的環境變數、功能上所需要預載的資料，如一張顯示各地區的郵遞區號。2.將物件轉換為JSON 格式字串，比如商品資訊、使用者資訊。3. 資料統計：如紀錄網站訪問量、某文件的下載量、喜歡數。4. 時間內限制請求次數：比如說用戶請求發送短信驗證碼後，就不允許用戶在五分鐘內重新發送請求驗證碼。所以當用戶請求發送，伺服器便會紀錄該用戶的ID儲存在redis到已經發送短信內的亂數字串，並設定過期時間為5分鐘，接著用戶發送請求，伺服器就會依據userId來從redis找到對應字串，若找得到就不允許重複發送 5. 儲存 session ，替分散式系統集中管理/儲存session`
<!--SR:!2023-10-02,29,191-->


#🧠 請列舉Redis 上的hash能應用到什麼樣的功能(提示：購物車)  ->->-> `購物車下會有的產品清單`
<!--SR:!2023-12-06,196,231-->


---
Status: #🌱 
Tags:
[[RedisJSON 讓Redis 伺服器能夠以JSON形式來處理每個key上的value]]
Links:
[[Redis Simple Dynamic String會根據實際儲存字串的內容來調整其記憶體空間]]
[[Redis Hash是儲存多個key-value的字典]]
[[Redis Hash 遇到 巢狀結構的資料的話，又是面臨到要以String或者Hash來儲存的問題]]
References:
[[@yunshu_youpaiyunRedisCunChuDuiXiangXinXiShiYongHash]]
[[@RedisCunjsonZiLiaoShiXuanZestringHuanShihash]]
[[@yudiandemingziTanTanRedisWuZhongShuJuJieGouJiZhenShiYingYongChangJingYuDianDeMingZiBoKeYuan]]
