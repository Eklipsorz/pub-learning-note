## 描述

引用[[@wikidataTongYongWeiYiShiBieMa2022]]所描述
> 通用唯一辨識碼(UUID)是用於電腦體系中以辨識資訊的一個128位元識別碼。 根據標準方法生成，不依賴中央機構的註冊和分配，UUID具有唯一性，這與其他大多數編號方案不同。重複UUID碼概率接近零，可以忽略不計。

重點：
- UUID 全名為**U**niversally **U**nique **Id**entifier
- UUID 主旨為不依賴中央機構的註冊和分配來提供獨特且唯一的序號
- 具體則是依據著產生序號的公式具有重複機率近似為0的特性來產出序號

### UUID 版本
UUID版本會是以UUIDvxx來表示，其中xx為版本數，如下所示：
```
UUIDv1
UUIDv2
UUIDv3
UUIDv4
```

### 使用上來說，不需要檢測
由於UUID本身具有近似為0的重複機率，所以不太需要檢測重複UUID的程式。

## 複習
#🧠 UUID是什麼？->->-> `主旨為不依賴中央機構的註冊和分配來提供獨特且唯一的序號，具體則是依據著產生序號的公式具有重複機率近似為0的特性來產出序號`
<!--SR:!2022-06-05,3,250-->

#🧠 UUID一旦產出後，需不需要額外寫一個程式來檢測當前UUID是與過去的UUID重複？ ->->-> `由於UUID本身具有近似為0的重複機率，所以不太需要檢測重複UUID的程式。`
<!--SR:!2022-06-05,3,250-->

---
Status: #🌱 
Tags:
[[Database]] - [[ID]]
Links:
[[Sequelize 上的UUID 具體來說會在不同資料庫系統有著不同的資料型別]]
References:
[[@wikidataTongYongWeiYiShiBieMa2022]]