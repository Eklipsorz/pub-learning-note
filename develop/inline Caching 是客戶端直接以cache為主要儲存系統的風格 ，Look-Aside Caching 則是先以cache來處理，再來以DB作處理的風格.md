## 描述
引用[[@jyt0532HuanCunDuXieJiZhiJyt0532Blog]]所描述的inline cache和look-Aside Cache：

> inline caching
> ![](https://www.jyt0532.com/public/inline-cache.png)

> look-Aside Cache
> ![](https://www.jyt0532.com/public/look-aside-cache.png)

重點：
- inline Caching 和 Look-Aside Caching 的 Caching 則是緩存某些事物這項行為、過程、架構
- inline Caching 和 Look-Aside Caching 是設計緩存和資料庫的存取風格之一
-  inline Caching 是按照字面上的意思，資料庫、緩存、客戶端都擺在同一行為結構，並且存取模式都是一層面向最靠近的一層來直接處理：比如客戶端這層會先直接以緩存這層上的資料進行存取，並且由緩存負責與資料庫這層級進行資料上的同步
-  Look-Aside Caching 則是按照字面上的意思，客戶端與資料庫、緩存都各放一邊，並且存取模式是先從一邊開始處理，若無法就換另一邊來處理：是客戶端先對緩存做處理，若無法處理，就轉由另一邊的資料庫來處理。

## 複習
#🧠 inline Caching 和 Look-Aside Caching 的 Caching  是指->->-> `緩存某些事物這項行為、過程、架構`
<!--SR:!2022-07-08,27,250-->
#🧠 inline Caching是什麼？ ->->-> `是按照字面上的意思，資料庫、緩存、客戶端都擺在同一行為結構，並且存取模式都是一層面向最靠近的一層來直接處理：比如客戶端這層會先直接以緩存這層上的資料進行存取，並且由緩存負責與資料庫這層級進行資料上的同步`
<!--SR:!2022-07-05,25,250-->

#🧠  Look-Aside Caching 是什麼？ ->->-> ` 則是按照字面上的意思，客戶端與資料庫、緩存都各放一邊，並且存取模式是先從一邊開始處理，若無法就換另一邊來處理：是客戶端先對緩存做處理，若無法處理，就轉由另一邊的資料庫來處理`
<!--SR:!2022-08-30,58,250-->


---
Status: #🌱 
Tags:
[[Caching]] - [[Redis]] - [[Database]]
Links:
[[cache hit為主的方法是從緩存存取資料但很容易被人忽略同步問題，cache miss為主的方法是從資料庫讀取資料但能選擇同步]]
References:
[[@jyt0532HuanCunDuXieJiZhiJyt0532Blog]]