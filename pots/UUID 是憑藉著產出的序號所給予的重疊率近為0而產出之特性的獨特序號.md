## 描述

引用[[@wikidataTongYongWeiYiShiBieMa2022]]所描述
> 通用唯一辨識碼(UUID)是用於電腦體系中以辨識資訊的一個128位元識別碼。 根據標準方法生成，不依賴中央機構的註冊和分配，UUID具有唯一性，這與其他大多數編號方案不同。重複UUID碼概率接近零，可以忽略不計。

重點：
- UUID 全名為**U**niversally **U**nique **Id**entifier
- UUID 是一種用來識別全世界事物的識別ID，主旨為不依賴中央機構的註冊和分配來提供獨特且唯一的序號，具體則是依據著產生序號的公式具有重複機率近似為0的特性來產出序號

### UUID 版本
UUID版本會是以UUIDvxx來表示，其中xx為版本數，如下所示：

```
UUIDv1
UUIDv2
UUIDv3
UUIDv4
```

每個UUID版本的特性：
- 都依據特定實現目標來產生：
引用[[@wikidataTongYongWeiYiShiBieMa2022]]所描述
> 版本由 M 字串中指示。
> 版本1 - UUID 是根據時間和 節點ID（通常是MAC位址）生成； 
> 版本2 - UUID是根據識別碼（通常是組或使用者ID）、時間和節點ID生成； 
> 版本3、版本5 - 確定性UUID 通過雜湊（hashing）命名空間（namespace）識別碼和名稱生成； 
> 版本4 - UUID 使用[隨機性](https://zh.wikipedia.org/wiki/%E9%9A%8F%E6%9C%BA%E6%80%A7 "隨機性")或[偽隨機性](https://zh.wikipedia.org/wiki/%E4%BC%AA%E9%9A%8F%E6%9C%BA%E6%80%A7 "偽隨機性")生成。

- 使用者可選擇指定版本來達成目標，每個版本都是獨立的，且並不會繼承前一個版本的功能，如版本4的UUID就不會繼承版本1、版本2、版本3的功能
源自於[[@uuluUUIDBuTongBanBenDeQuBieJiXuanZeJianShu]]

### 使用上來說，不需要檢測
由於UUID本身具有近似為0的重複機率，所以不太需要檢測重複UUID的程式。

## 複習
#🧠 UUID是什麼？->->-> `一種用來識別全世界事物的識別ID，主旨為不依賴中央機構的註冊和分配來提供獨特且唯一的序號，具體則是依據著產生序號的公式具有重複機率近似為0的特性來產出序號`
<!--SR:!2022-07-16,27,250-->

#🧠 UUID一旦產出後，需不需要額外寫一個程式來檢測當前UUID是與過去的UUID重複？ ->->-> `由於UUID本身具有近似為0的重複機率，所以不太需要檢測重複UUID的程式。`
<!--SR:!2022-08-22,50,250-->

#🧠 UUID 的版本上的特性有哪些(提示：每個版本都有各自目標？每個版本是否繼承前一個版本？) ->->-> `UUID版本都依據特定實現目標來產生對應UUID、每個版本不會繼承前一個版本的功能`
<!--SR:!2022-09-02,55,250-->

#🧠 UUIDv4 是基於什麼而產生 ？ ->->-> `是為了讓UUID更像個隨機亂數而產出的版本`
<!--SR:!2022-08-30,53,250-->

#🧠  UUIDv5 和 UUIDv4 相比，誰的UUID更為隨機？->->-> `UUIDv4較為隨機，UUIDv5較為不隨機，因該版本的目標並不是為了讓UUID更像個隨機數，且每個版本都是獨立和不會繼承前一個版本的功能`
<!--SR:!2022-07-13,26,250-->

---
Status: #☀️ 
Tags:
[[Database]] - [[UUID]]
Links:
[[Sequelize 上的UUID 具體來說會在不同資料庫系統有著不同的資料型別]]
References:
[[@uuluUUIDBuTongBanBenDeQuBieJiXuanZeJianShu]]
[[@wikidataTongYongWeiYiShiBieMa2022]]