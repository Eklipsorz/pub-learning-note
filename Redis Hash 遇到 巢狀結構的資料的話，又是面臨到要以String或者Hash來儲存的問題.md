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

![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1653497774/blog/database/redis/key-to-userhash-and-clotheshash_m27vwx.png)


![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1653497774/blog/database/redis/key-to-userhash-and-string_a5ze0l.png)

---
Status: 
Tags:
[[Redis]] - [[Data Structure]]
Links:
[[Redis Hash是儲存多個key-value的字典]]
References:
[[@yunshu_youpaiyunRedisCunChuDuiXiangXinXiShiYongHash]]