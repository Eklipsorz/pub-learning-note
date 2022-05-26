## 描述

### String vs. Hash
1. 記憶體成本：
- 以String作為Value的成本，相較於Hash，比較單純且比較少
- 以Hash作為Value的成本，相較於String，比較繁複且由於將資料切分開來儲存，每個要儲存的形式又是以key-value的形式，所以成本上會比較多

2. 新增/讀取/修改/刪除特定資料：若資料本身有多個屬性的屬性值
- 以String來說的話，要修改特定屬性的值，就必須為了那個值，而整筆資料(包含未要修改的屬性值)都要一起改，比如說使用者資料有名字、性別、電話，假設原資料為
```
小明：男：0102103131
```
但若想修改小明的電話，理論上就只修改電話的值，但String沒獨立存放，因此只能整筆資料一起改
```
小明：男：1234567890
```
- 以Hash來說的話，要修改特定屬性的值，由於會將資料切分成好幾分獨立的部分來儲存，每個又是以key-value pair來表示，所以只要指定對應key就能直接修改

3. 新增讀取/修改/刪除全部資料的話
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
- 讀取(整份或者大多數鍵值)資料、更新快取不頻繁(或者每次都更新json資料的大多數key)的場景 
(理由是String 記憶體成本比Hash較小，且String是整個包含資料)

Hash 適用場景為：
- 清楚理解哪些key-value是可用的(否則會讀取到錯誤值或者空值)
- 更新較為頻繁，尤其是指定特定key值
- 讀取特定少量的key值
(理由是Hash是將資料切分成更細的key-value pair，所以可以透過key來對特定value進行操作)

## 複習

#🧠  Redis 記憶體成本: string vs. hash ->->-> `以String作為Value的成本，相較於Hash，比較單純且比較少；以Hash作為Value的成本，相較於String，比較繁複且由於將資料切分開來儲存，每個要儲存的形式又是以key-value的形式，所以成本上會比較多`

#🧠 新增/讀取/修改/刪除特定資料： string vs. hash ->->-> `以String來說的話，要修改特定屬性的值，就必須為了那個值，而整筆資料(包含未要修改的屬性值)都要一起改；要修改特定屬性的值，由於會將資料切分成好幾分獨立的部分來儲存，每個又是以key-value pair來表示，所以只要指定對應key就能直接修改`

#🧠 新增讀取/修改/刪除全部資料的話：string vs. hash ->->-> `以String來說，就直接更改value值，不需要指定key來進行操作；以Hash來說，就必須指定每個key來進行操作`

#🧠 redis 上的string適用場景？ 理由是？ ->->-> ` 讀取(整份或者大多數鍵值)資料、更新快取不頻繁(或者每次都更新json資料的大多數key)的場景 ，(理由是String 記憶體成本比Hash較小，且String是整個包含資料) `
<!--SR:!2022-05-29,3,250-->

#🧠  redis 上的Hash 適用場景為？理由是？ ->->-> `清楚理解哪些key-value是可用的(否則會讀取到錯誤值或者空值)、 更新較為頻繁，尤其是指定特定key值、讀取特定少量的key值，理由是Hash是將資料切分成更細的key-value pair，所以可以透過key來對特定value進行操作)`
<!--SR:!2022-05-29,3,250-->



---
Status: #🌱 
Tags:
[[Redis]]
Links:
[[Redis Simple Dynamic String會根據實際儲存字串的內容來調整其記憶體空間]]
[[Redis Hash是儲存多個key-value的字典]]
[[Redis Hash 遇到 巢狀結構的資料的話，又是面臨到要以String或者Hash來儲存的問題]]
References:
[[@yunshu_youpaiyunRedisCunChuDuiXiangXinXiShiYongHash]]
[[@RedisCunjsonZiLiaoShiXuanZestringHuanShihash]]
