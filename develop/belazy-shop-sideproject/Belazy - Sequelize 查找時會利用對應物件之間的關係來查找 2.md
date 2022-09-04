
比如定義Product 和Cart之間的關係，就定義以productId來對應Cart的productId，這會使系統誤判Cart擁有productId，
```
Product.hasMany(models.Cart, { foreignKey: 'productId' })
```

實際上Cart只有id、userId、sum

---
Status: #🌱 
Tags:
[[Database]] - [[sequelize]] - [[Side Project]]
Links:
References: