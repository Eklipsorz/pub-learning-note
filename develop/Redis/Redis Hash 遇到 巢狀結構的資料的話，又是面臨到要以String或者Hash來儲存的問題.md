## 描述

當要用Redis儲存以下資料時，就會面臨到要選擇Hash來儲存或者是String來儲存
的這項問題，

```
// 該使用者的ID是1
{
  "name": "apple",
  "age": 25
}
```



那麼當選擇使用Hash的話，在redis上會是如下圖，由1這個key值去對應著儲存name和age的表格或者字典
![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1653497773/blog/database/redis/key-to-userhash_o7vjlv.png)

若是改以string儲存原有資料的話，那麼就會是如下圖，由1這個key值去對應著一個字串，字串包含著name和age
![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1653497773/blog/database/redis/key-to-string_ks1slg.png)


### 若添加一個另一份像是字典的資料呢？
若添加一個另一份像是字典的資料呢？比如像是添加clothes，裡面包裹著shirt和pants
```
{
  "name": "apple",
  "age": 25,
  "clothes": {
    "shirt": "gray",
    "pants": "read"
  }
}
```

這時又會面臨到要用string儲存clothes？還是用hash來儲存？
若選擇使用hash的話，會是如下圖：
![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1653497774/blog/database/redis/key-to-userhash-and-clotheshash_m27vwx.png)

若選擇使用string的話，會是如下圖：
![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1653497774/blog/database/redis/key-to-userhash-and-string_a5ze0l.png)


## 複習

#🧠 若一筆使用者資料儲存著名字為apple以及年齡為25的話，請問在redis分別使用string和hash來儲存會是如何->->-> ``
<!--SR:!2023-03-19,183,250-->

#🧠 若一筆使用者資料儲存著名字為apple、年齡為25、衣服穿著為shirt為灰色，pants為紅色的話，請問在redis分別使用string和hash來儲存會是如何 ->->-> ``
<!--SR:!2022-12-09,120,250-->


---
Status: #🌱 
Tags:
[[RedisJSON 讓Redis 伺服器能夠以JSON形式來處理每個key上的value]] - [[Data Structure]]
Links:
[[Redis Hash是儲存多個key-value的字典]]
References:
[[@yunshu_youpaiyunRedisCunChuDuiXiangXinXiShiYongHash]]