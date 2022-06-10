
## 描述

### 案例1 
引用[[@0xbooShiMeShiWenTiYiJiRuHeJieJue]]所描述：
> `N+1` 是ORM（对象关系映射）关联数据读取中存在的一个问题。

> 在介绍什么是`N+1`问题之前，首先思考一个问题：
假设现在有一个用户表（User）和一个余额表（Balance），这两个表通过`user_id`进行关联。现在有一个需求是**查询年龄大于18岁的用户，以及用户各自的余额**。

> 这个问题并不难，但对于新手而言，可能常常会犯的一个错误就是在循环中进行查询。

```
$users = User::where("age", ">", 18)->select();
foreach($users as $user){
  $balance = User::getFieldByUserId($user->user_id, "balance");
  $user['balance'] = $balance;
}
```

> 这样做是非常糟糕的，数据量小还少，在数据量较大的情况下，是非常消耗数据库性能的。通过Mysql 查询日志，可以看到查询用户表是一次，因为有四个符合该条件的用户，查询用户表关联的余额表是四次。

![](https://segmentfault.com/img/remote/1460000039421846)

> `N+1`问题就是这样产生的：查询主表是一次，查询出N 条记录，根据这N 条记录，查询关联的副（从）表，共需要N 次。所以，应该叫`1+N` 问题更合适一些。

> 其实，如果稍微了解一点SQL，根本不用这么麻烦，直接使用`IN` 一次就搞定了。对于这类问题，ORM 其实为我们提供了相应的方案，那就是使用『预加载功能』

重點：
- N + 1  Queri

### 案例2
引用[[@huyangKePuWenShiMeShiORMZhongDeNZhiHu]]所描述
> 接下来我们有一个需求，展示一个文章列表页，列表页上展示的信息包括：文章标题，文章作者名称。就这两个字段，也不需要分页。

> 我们要查询出这样的数据要怎么做呢。在ORM的世界中，我们直观的做法是这样:

```text
posts = Post.objects.all()  #  获取所有的文章数据，注意此时不会执行sql语句  by the5fire
result = []
for post in posts:   # 此时会执行select * from post的查询
    result.append({
        'title': post.title,
        'owner': post.owner.name,  # 此时会执行  select * from user where user_id = <post.user_id>
    })
```

> 写到这就明白了吧。每次循环都要查一下user表，也就是说，如果我第一次查询是10条记录，那么最终我需要执行的查询语句就是10 + 1 = 11条语句。如果我第一次查询出来的是N条记录，那么最终需要执行的sql语句就是N+1次。

> 这就是N+1的问题。

> 但是如果懂SQL的话，就知道，其实这就是一个简单的JOIN语句。一条语句就能查出所有的数据，搞什么N+1.

```text
SELECT t1.title, t2.name from post as t1 INNER JOIN user as t2 ON t2.id = t1.owner_id;
```


https://zhuanlan.zhihu.com/p/27323883

https://dosmanthus.medium.com/rails-n-1-queries-problem-73dfe5f99182
https://medium.com/@chaowu.dev/rails-n-1-query-41aa92ffb92e
https://segmentfault.com/a/1190000039421843
https://chuyi.inow.tw/2013/02/eager-loading-and-lazy-loading/
https://www.796t.com/content/1519841049.html
https://ithelp.ithome.com.tw/articles/10223194

### 為何衍生？


1. 原本預期： 當向資料庫發送一筆Query來索要特定集合的N筆紀錄，那麼實際資料庫收到的Query就一個
2. 實際情況：當向資料庫發送一筆Query來索要特定集合的N筆紀錄，那麼會因沒事先紀錄與特定集合相關連的集合而發送N+1筆Queries來實現


預期會有的實現：當向資料庫發送一筆Query來索要特定集合A的N筆紀錄，那麼會預期系統會事先向資料庫索要與特定集合相關連的表格集合B並記錄下來，接著讓特定集合A的每一筆紀錄(總數為N筆)都去從表格集合B找到相關連的紀錄，比如：

特定集合A為產品表格，而與特定集合A相關連的表格集合B是庫存量，那麼系統就會先向資料庫索要庫存量來紀錄，然後讓特定集合A的每筆紀錄透過外鍵來從庫存量找到相關連的紀錄


實際會有的實現：當向資料庫發送一筆Query 來索要特定集合A的N筆紀錄，實際上系統並不會事先紀錄與特定集合A相關連的表格集合B，那麼為此，特定集合A的每一筆紀錄都必須向資料庫發送一筆Query 來索要表格集合B，接著從表格集合B找到相關連的紀錄。

為此總共的Query數會是如下，1是指原本向資料庫索要特定集合A個N筆紀錄之Query，而N個Queries是指特定集合A的每一筆所發出額外的一筆Query，而這Query是向資料庫索要著表格集合B。
```
1 + N 個Queries
```

### 實務層面：為何要特別提起這問題
N + 1 Queries Problem 描述著額外產出的Query，而Query越多，資料庫負擔就越重，所以實務上提到它乃是因為它是在增加資料庫的不必要處理負擔前提下，來實現主要的Query 。

### 常見的發生地點
一般來說，SQL官方提供的語法都會特別事先紀錄相關連的表格，但若考慮ORM需要從應用程式層面來轉換SQL語法的話，就不一定能夠特別關注這問題，因此常見的問題乃是因為 **ORM 是否會事先儲存相關連的表格來做處理**


## 複習
#🧠 Database：N+1 問題是什麼？ ->->-> `N + 1 Queries Problem當向資料庫發送一筆Query來索要特定集合的N筆紀錄，那麼會因沒事先紀錄與特定集合相關連的集合而發送N+1筆Queries來實現`
<!--SR:!2022-06-13,3,250-->

#🧠 Database：N+1 問題的發生主因是什麼？ ->->-> `沒事先紀錄與特定集合相關連的集合`
<!--SR:!2022-06-13,3,250-->

#🧠 Database：N+1 問題發生在哪個常見場合 ->->-> `一般來說，SQL官方提供的語法都會特別事先紀錄相關連的表格，但若考慮ORM需要從應用程式層面來轉換SQL語法的話，就不一定能夠特別關注這問題，因此常見的問題乃是因為 **ORM 是否會事先儲存相關連的表格來做處理**
<!--SR:!2022-06-13,3,250-->
`

#🧠 Database：N+1 問題之前，系統預期如何處理1個索要特定集合的Query?->->-> `預期會有的實現：當向資料庫發送一筆Query來索要特定集合A的N筆紀錄，那麼會預期系統會事先向資料庫索要與特定集合相關連的表格集合B並記錄下來，接著讓特定集合A的每一筆紀錄(總數為N筆)都去從表格集合B找到相關連的紀錄`
<!--SR:!2022-06-13,3,250-->

---
Status: #🌱 
Tags:
[[Database]] - [[ORM]]
Links:
References:
[[@0xbooShiMeShiWenTiYiJiRuHeJieJue]]
[[@huyangKePuWenShiMeShiORMZhongDeNZhiHu]]