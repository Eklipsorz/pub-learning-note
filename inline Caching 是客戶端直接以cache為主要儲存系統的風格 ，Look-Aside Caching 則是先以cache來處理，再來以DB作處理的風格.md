## 描述
引用[[@jyt0532HuanCunDuXieJiZhiJyt0532Blog]]所描述的inline cache和look-Aside Cache：

> inline caching
> ![](https://www.jyt0532.com/public/inline-cache.png)

> look-Aside Cache
> ![](https://www.jyt0532.com/public/look-aside-cache.png)

重點：
- inline Caching 和 Look-Aside Caching 的 Caching 則是指緩存某些事物這項行為或者過程
- inline Caching 和 Look-Aside Caching 是設計緩存和資料庫的存取風格之一
-  inline Caching 是按照字面上的意思，資料庫、緩存、客戶端都擺在同一行為結構，並且存取模式都是一層面向最靠近的一層來直接處理：比如客戶端這層會先直接以緩存這層上的資料進行存取，並且由緩存負責與資料庫這層級進行資料上的同步
-  Look-Aside Caching 則是按照字面上的意思，客戶端與資料庫、緩存都各放一邊，並且存取模式是先從一邊開始處理，若無法就換另一邊來處理：是客戶端先對緩存做處理，若無法處理，就轉由另一邊的資料庫來處理。

## 複習
#🧠 inline Caching 和 Look-Aside Caching 的 Caching  是指->->-> `緩存某些事物這項行為或者過程`
#🧠 inline Caching是什麼？ ->->-> `是按照字面上的意思，資料庫、緩存、客戶端都擺在同一行為結構，並且存取模式都是一層面向最靠近的一層來直接處理：比如客戶端這層會先直接以緩存這層上的資料進行存取，並且由緩存負責與資料庫這層級進行資料上的同步`

#🧠  Look-Aside Caching 是什麼？ ->->-> ` 則是按照字面上的意思，客戶端與資料庫、緩存都各放一邊，並且存取模式是先從一邊開始處理，若無法就換另一邊來處理：是客戶端先對緩存做處理，若無法處理，就轉由另一邊的資料庫來處理`


---
Status: #🌱 
Tags:
[[客戶端對緩存發讀需求主要有cache hit為主和cache miss為主這兩種策略]] - [[Redis]] - [[Database]]
Links:
References:
[[@jyt0532HuanCunDuXieJiZhiJyt0532Blog]]