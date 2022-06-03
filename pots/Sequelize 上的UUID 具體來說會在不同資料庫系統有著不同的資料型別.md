## 描述
引用[[@ModelBasicsSequelize]]所描述
> For UUIDs, use `DataTypes.UUID`. It becomes the `UUID` data type for PostgreSQL and SQLite, and `CHAR(36)` for MySQL. Sequelize can generate UUIDs automatically for these fields, simply use `DataTypes.UUIDV1` or `DataTypes.UUIDV4` as the default val

重點：
- Sequelize 上的UUID會在MySQL對應成char(36)
- Sequelize 上的UUID會在PostgreSQL和SQLite上會是對應著UUID
## 複習
#🧠  Sequelize 上的UUID會在MySQL對應成什麼樣的資料型別(提示：數字呢？還是字元呢？) ->->-> `Sequelize 上的UUID會在MySQL對應成char(36)`
<!--SR:!2022-06-06,3,250-->

#🧠 Sequelize 上的UUID會在PostgreSQL和SQLite上會是對應著什麼樣的資料型別 ->->-> `Sequelize 上的UUID會在PostgreSQL和SQLite上會是對應著UUID`
<!--SR:!2022-06-06,3,250-->

---
Status: #🌱 
Tags:
[[Database]] - [[Sequelize]]
Links:
[[UUID 是憑藉著產出的序號所給予的重疊率近為0而產出之特性的獨特序號]]
References:
[[@ModelBasicsSequelize]]