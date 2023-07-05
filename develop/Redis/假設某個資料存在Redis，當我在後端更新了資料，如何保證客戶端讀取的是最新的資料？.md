

## 描述
引用[[@bravo1988QuNianDeYiCiMianShiRuHeBiMianHuanCunZangDu]]所描述：
> 假設某個資料存在Redis，當我在後端更新了資料，如何保證客戶端讀取的是最新的資料？

重點：
- 在這裡是要求保證客戶端讀取的資料是最新的，但沒指定客戶端讀取的資料來源是資料庫？還是緩存？
- 通常會是假定緩存，所以會更新成以下問題 **當我在後端更新了資料庫，如何保證緩存讀取到的資料是最新的？**

### 一開始的解答

> 我当时的回答是：找到更新数据的入口，每次更新DB都同步或异步更新缓存。比如
>```java
>public void update(){
> 1.更新数据库
> 2.更新缓存（同步或异步）
>}
> ```

> 面试官紧接着问我，如果A线程刚更新完缓存，B线程又来更新数据库，且尚未更新缓存，此时C线程从缓存中读到的就是旧的数据了。

![](https://pic4.zhimg.com/80/v2-7c211b78f016452666d8dde7a7a8d23f_720w.jpg)

> 我当时也是年轻啊，直接说：加锁，把1和2设置为原子操作。

> 实际上，加锁也是解决不了问题的，因为Redis和DB又不是同一个连接，不在一个事务里…

重點：
- 一開始解答，


## 複習

---
Status: #🌱 
Tags:
[[Redis]] - [[Database]]
Links:
[[redis dirty read 是指redis儲存(讀取)與資料庫不一致的資料]]
References:
[[@bravo1988QuNianDeYiCiMianShiRuHeBiMianHuanCunZangDu]]
