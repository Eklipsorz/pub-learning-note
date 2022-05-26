## 描述

Redis  主要是以key-value pair為主，

value  可以是string 和 hash ，比如以下是某個使用者的資料
```
name = tom
age = 28
```

若使用string的話，會是下圖中的前兩個來表示，但若是採用hash的話，則會是下圖中的最後一個來表示

![](https://p1-jj.byteimg.com/tos-cn-i-t2oaga2asx/gold-user-assets/2018/10/3/1663a75da4aca1ed~tplv-t2oaga2asx-zoom-in-crop-mark:1304:0:0:0.image)


### String
主要會是採用SDS(Simple Dynamic String)來定義字串
[[Redis Simple Dynamic String會根據實際儲存字串的內容來調整其記憶體空間]]
### Hash
主要是以Dictionary形式來定義Hash
[[Redis Hash是儲存多個key-value的字典]]
[[Redis Hash 遇到 巢狀結構的資料的話，又是面臨到要以String或者Hash來儲存的問題]]

### String 和 Hash 適用場景

> 


---
Status: #🌱 
Tags:
[[RedisJSON 讓Redis 伺服器能夠以JSON形式來處理每個key上的value]] - [[Operating System]]
Links:
[[Redis Simple Dynamic String會根據實際儲存字串的內容來調整其記憶體空間]]
[[Redis Hash是儲存多個key-value的字典]]
References:

[[@yunshu_youpaiyunRedisCunChuDuiXiangXinXiShiYongHash]]
