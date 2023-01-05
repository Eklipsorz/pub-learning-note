## 描述
> 缓存穿透是指用户请求的数据在缓存中不存在即没有命中，同时在数据库中也不存在，导致用户每次请求该数据都要去数据库中查询一遍。

> 如果短时间大量类似请求落在数据库上，造成数据库压力过大，可能导致数据库承受不住而宕机崩溃。

![](https://s6.51cto.com/images/blog/202205/05235853_6273f43dc9a6b82347.png?x-oss-process=image/watermark,size_14,text_QDUxQ1RP5Y2a5a6i,color_FFFFFF,t_100,g_se,x_10,y_10,shadow_20,type_ZmFuZ3poZW5naGVpdGk=)


重點：
- Cache Penetration 是指由於請求索求的資料原本不在緩存和資料庫而使得緩存無法替資料庫擋下請求，而被直接導向處於硬碟，但資料庫本身也找不到
- 若大量請求都是如此的話，會使資料庫負載提高，並進而讓資料庫承受不了而當機

### Cache Penetration 命名緣由
Cache 是指緩存，Penetration是指穿透某事物或者進入至某事物，Cache和Penetration合併一起就是說緩存穿透，在這裡會是指緩存被請求給穿透
> a movement into or through something or someone

### Cache Penetration 起因
主要起因為：
- 請求索求的資料原本就不在資料庫，這表示它正在索求原本不存在的東西，所以緩存也會跟著找不到，進而被穿透。

### 索取的東西原本就不存在資料庫：解決方案
> a)、将无效的key存放进Redis中：
> 
> 当出现Redis查不到数据，数据库也查不到数据的情况，我们就把这个key保存到Redis中，设置value="null"，并设置其过期时间极短，后面再出现查询这个key的请求的时候，直接返回null，就不需要再查询数据库了。但这种处理方式是有问题的，假如传进来的这个不存在的Key值每次都是随机的，那存进Redis也没有意义。

> b)、使用布隆过滤器：
>
> 如果布隆过滤器判定某个 key 不存在布隆过滤器中，那么就一定不存在，如果判定某个 key 存在，那么很大可能是存在(存在一定的误判率)。于是我们可以在缓存之前再加一个布隆过滤器，将数据库中的所有key都存储在布隆过滤器中，在查询Redis前先去布隆过滤器查询 key 是否存在，如果不存在就直接返回，不让其访问数据库，从而避免了对底层存储系统的查询压力。

![](https://s2.51cto.com/images/blog/202205/05235853_6273f43def1558136.png?x-oss-process=image/watermark,size_14,text_QDUxQ1RP5Y2a5a6i,color_FFFFFF,t_100,g_se,x_10,y_10,shadow_20,type_ZmFuZ3poZW5naGVpdGk=)

重點：
- 解法1：將原本不存在的資料放進緩存中，設定其資料的key-value pair，value會是null，但這會衍生另一個問題-有哪些原本不存在的資料？
- 解法2：設定Bloom Filter在緩存之前，每一次要對緩存進行存取都先透過Bloom Filter來確認索求的東西是否在緩存，若不存在就直接返回，不讓請求因而穿透去向資料庫發送請求。
	- 為什麼要採用Bloom Filter? 由於緩存通常儲存大量的key-value pair來預防大量請求，所以若採取其他的方式，很有可能會因為輸入資料變多而使驗證成本逐漸跟著提高，而Bloom Filter本身的時間和空間成本都是在常數時間，只是寫入的資料越多越會誤判，但現今有許多Bloom Filter版本來想辦法解決

## 複習
#🧠 Cache Penetration 命名緣由是什麼？ ->->-> `Cache 是指緩存，Penetration是指穿透某事物或者進入至某事物，Cache和Penetration合併一起就是說緩存穿透，在這裡會是指緩存被請求給穿透`
<!--SR:!2023-04-02,190,250-->

#🧠 Cache Penetration 是什麼樣的問題？ ->->-> `是指由於請求索求的資料原本不在緩存和資料庫而使得緩存無法替資料庫擋下請求，而被直接導向處於硬碟，但資料庫本身也找不到`
<!--SR:!2023-09-30,293,250-->

#🧠 若大量請求都有Cache Penetration這問題的話，會衍生出什麼樣的問題？ ->->-> `若大量請求都是如此的話，會使資料庫負載提高，並進而讓資料庫承受不了而當機`
<!--SR:!2023-01-27,147,250-->


#🧠 Cache Penetration 起因 是什麼？ ->->-> `請求索求的資料原本就不在資料庫，這表示它正在索求原本不存在的東西，所以緩存也會跟著找不到，進而被穿透。`
<!--SR:!2023-11-13,320,250-->

#🧠 Cache Penetration：索取的東西原本就不存在緩存和資料庫，請問解決方案為何 (提示：有兩個，好像有個叫filter跟null) ->->-> `將原本不存在的資料放進緩存中，設定其資料的key-value pair，value會是null，但這會衍生另一個問題-有哪些原本不存在的資料？、設定Bloom Filter在緩存之前，每一次要對緩存進行存取都先透過Bloom Filter來確認索求的東西是否在緩存，若不存在就直接返回，不讓請求因而穿透去向資料庫發送請求。`
<!--SR:!2023-03-05,66,230-->


#🧠 Cache Penetration：索取的東西原本就不存在緩存和資料庫，解決方案為何要採取Bloom Filter ? 為何不改用hash ->->-> `由於緩存通常儲存大量的key-value pair來預防大量請求，所以若採取其他的方式，很有可能會因為輸入資料變多而使驗證成本逐漸跟著提高，而Bloom Filter本身的時間和空間成本都是在常數時間，只是寫入的資料越多越會誤判，但現今有許多Bloom Filter版本來想辦法解決`
<!--SR:!2023-10-10,278,230-->

---
Status: #🌱 
Tags:
[[Redis] - [[Caching]] 
Links:
[[Bloom Filter 是透過K個雜湊函式和M個bit array 來組成一個快速篩檢元素是否存在緩存]]
[[Cache Avalanche 是指大量請求在cache上的大量key失效下而從cache被導向至處於硬碟的資料庫]]
[[Hotspot Invalid 是指由於某個熱門的資料在緩存失效而導致大量索求該資料的請求直接被轉向至資料庫]]
References:
[[@manbucoding2022NianRedisZuiXinMianShiTiDi8PianRedisHuanCunWenTiWx624642a80743cDeJiShuBoKe]]
[[@liuRedisKuaiQuXueBengJiChuan2021]]