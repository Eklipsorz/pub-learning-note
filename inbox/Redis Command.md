Redis  主要是以key-value pair為主，

value  可以是string 和 hash ，比如以下是某個使用者的資料
```
name = tom
age = 28
```

若使用string的話，會是下圖中的前兩個來表示，但若是採用hash的話，則會是下圖中的最後一個來表示

![](https://p1-jj.byteimg.com/tos-cn-i-t2oaga2asx/gold-user-assets/2018/10/3/1663a75da4aca1ed~tplv-t2oaga2asx-zoom-in-crop-mark:1304:0:0:0.image)

HSET、HGET、