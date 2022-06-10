
## 描述

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

### 為何衍生？

### 實務層面：為何要特別提起這問題


## 複習
#🧠 Question :: ->->-> ``

---
Status: #🌱 
Tags:
[[Database]] - [[ORM]]
Links:
References:
