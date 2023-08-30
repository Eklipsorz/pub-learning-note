

## 描述

ORM 本身會以物件形式來表示資料庫的任意資料，並且允許應用程式透過物件操作來轉換成對應SQL語法，並發送至資料庫系統。通常來說，ORM只有應用程式真的需要資料的時候，才會轉換成對應SQL發送，這是減少不必要資料庫操作的手段之一


比如說以

引用[[@huyangKePuWenShiMeShiORMZhongDeNZhiHu]]所描述
```text
posts = Post.objects.all()  #  获取所有的文章数据，注意此时不会执行sql语句  
result = []
for post in posts:   # 此时会执行select * from post的查询
    result.append({
        'title': post.title,
        'owner': post.owner.name,  # 此时会执行  select * from user where user_id = <post.user_id>
    })
```


重點：
- 當應用程式執行第一行來請求ORM時，ORM並不會直接轉換對應SQL來索求所有文章
- 等到真正需要所有文章的資料時，也就是透過每篇文章的資訊來找相關文章的擁有人資訊，ORM才會轉換對應SQL來索求



引用[[@0xbooShiMeShiWenTiYiJiRuHeJieJue]]所描述：
```
$users = User::where("age", ">", 18)->select();
foreach($users as $user){
  $balance = User::getFieldByUserId($user->user_id, "balance");
  $user['balance'] = $balance;
}
```

重點：
- 當應用程式執行第一行來請求ORM時，ORM也並不會直接轉換對應SQL來索求所有使用者
- 等到真正需要使用者的資料，也就是透過每個使用者的資訊來找相關存款的資訊，ORM才會轉換成對應SQL來索求

## 複習
#🧠 應用程式當使用ORM語法來操作對應物件時，若只是應用程式向ORM索求對應資訊，但應用程式對對應資訊沒任何存取操作的話，ORM會如何處理？（提示：是會直接轉換SQL語法來要？還是就算了，反正它沒要存取) ->->-> `ORM 到真正需要資料的時候，才會替應用程式轉換對應SQL語法來向資料庫系統發送請求，所以只有應用程式對指定資訊有任何存取操作，否則通常ORM收到就一律不轉換對應語法`
<!--SR:!2024-02-24,215,230-->

#🧠 以下為應用程式對於ORM下物件的語法，請說明ORM會如何處理應用程式所發送的請求？ ![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1654927260/blog/database/query/N_1-Problem-Example2_dme7so.png)->->-> `- 當應用程式執行第一行來請求ORM時，ORM並不會直接轉換對應SQL來索求所有文章- 等到真正需要所有文章的資料時，也就是透過每篇文章的資訊來找相關文章的擁有人資訊，ORM才會轉換對應SQL來索求`
<!--SR:!2024-01-13,135,230-->


#🧠 以下為應用程式對於ORM下物件的語法，請說明ORM會如何處理應用程式所發送的請求？![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1654927260/blog/database/query/N_1-Problem-Example1_xqkmom.png)->->-> `- 當應用程式執行第一行來請求ORM時，ORM也並不會直接轉換對應SQL來索求所有使用者 - 等到真正需要使用者的資料，也就是透過每個使用者的資訊來找相關存款的資訊，ORM才會轉換成對應SQL來索求`
<!--SR:!2024-02-09,218,230-->




---
Status: #🌱 
Tags:
[[Database]] - [[ORM]]
Links:
References:
[[@0xbooShiMeShiWenTiYiJiRuHeJieJue]]
[[@huyangKePuWenShiMeShiORMZhongDeNZhiHu]]