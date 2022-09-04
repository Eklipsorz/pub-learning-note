
Belazy - sequelize 部分update不能修改身為主鍵的屬性，比如透過find系列獲取到的物件，若對物件進行主鍵修改，會被sequelize 禁止
```
const cart = await Cart.findOne(...)
await cart.update({id: ....})
```

恐怕是由於怕update的過程會一直用到舊的主鍵值來找到它。


## 解法
透過Model的update方法：從User表格中找到id:41並修改，而非透過找到物件來修改，即可完成

[[@janmeierCanUpdatePrimary]] 所描述：

> Just tested this again, and I discovered a problem - updating the primary key also updates the where clause (`SET "id"=44 WHERE "id" = 44`)

> You should use bulk update instead:

```
return User.update({
      id: 44
    }, {
      where: {
        id: 41
      }
    })
```

---
Status: #🌱 
Tags:
[[Side Project]] - [[Database]] - [[sequelize]]
Links:
References:
[[@janmeierCanUpdatePrimary]]