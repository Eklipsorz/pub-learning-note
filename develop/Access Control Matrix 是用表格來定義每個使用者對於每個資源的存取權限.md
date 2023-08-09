

## 描述
ACM 是 Access Control Matrix 的縮寫，定義在特定系統上，某些特定物件A對於特定資源B上所擁有的權限，會是以矩陣的形式或者以表格形式來表示，如下圖的表格：
- 表格代表著特定系統
- 表格上的橫列(row)皆代表著不同特定物件A
- 直欄(column)則是代表著特定資源B
- 欄位值就是代表著特定物件A對於該欄位所代表的特定資源B之所擁有的權限

舉例來說，下圖是列舉三個特定物件A：s1、s2、s3，特定資源B則是指f1、f2、f3、f4、f5、f6，在這裡以(a,b)來表示欄位值，a為第a列，b為第b欄，若(1,2)的話就表示特定物件s1 對於f2的存取是擁有權限、讀寫權限，若(1,1)的話，就代表著特定物件s1對於f1的存取是毫無權限的。

後面權限定義依此類推。
![](https://www.researchgate.net/profile/James-Joshi/publication/27233516/figure/fig1/AS:638408414220289@1529219835691/An-access-control-matrix-and-its-access-control-list-and-capability-list.png)

## 優點
1. 可透過索引容易了解特定物件對於特定資源的權限是什麼

## 缺點
1. 相較於ACL[[Access Control List 是使用串列來定義每個物件所擁有的權限]]而言，會佔取更多空間，因為會ACM不論如何存取需求為何，都會算到表格本身這個固定空間成本，而ACL會根據需求來增加或者減少空間成本


## Note
引用劍橋字典所描述的Matrix會是指：
> a group of numbers or other symbols arranged in a rectangle that can be used together as a single unit to solve particular mathematical problems

一組數字或者一組符號組成一個正方形狀來合併成一個基本單位來處理，其形狀會是
```
1 2 3
4 5 6
7 8 9
```


## 複習

#🧠 Access Control Matrix 是用來做什麼？->->-> `定義在特定系統上，某些特定物件A對於特定資源B上所擁有的權限，會是以矩陣的形式或者以表格形式來表示`
<!--SR:!2025-09-12,764,270-->

#🧠  能試著說明第一列第二欄是指什麼意思？第一列第一欄是指什麼意思？ ![](https://www.researchgate.net/profile/James-Joshi/publication/27233516/figure/fig1/AS:638408414220289@1529219835691/An-access-control-matrix-and-its-access-control-list-and-capability-list.png) ->->-> `若(1,2)的話就表示特定物件s1 對於f2的存取是擁有權限、讀寫權限，若(1,1)的話，就代表著特定物件s1對於f1的存取是毫無權限的。`
<!--SR:!2023-09-03,300,270-->

#🧠  Access Control Matrix 的優點是什麼？ ->->-> `透過索引容易了解特定物件對於特定資源的權限是什麼`
<!--SR:!2023-09-24,313,270-->

#🧠  Access Control Matrix 的缺點是什麼? ->->-> `相較於ACL而言，會佔取更多空間，因為會ACM不論如何存取需求為何，都會算到表格本身這個固定空間成本，而ACL會根據需求來增加或者減少空間成本`
<!--SR:!2024-02-01,375,250-->

---
Status: #☀️  
Tags:
[[Operating System]]  - [[Array]] - [[LinkedList]]
Links:
[[Access Control List 是使用串列來定義每個物件所擁有的權限]]
References:
[[@jamesb.d.joshiAccessControlMatrix]]