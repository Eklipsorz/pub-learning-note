## 描述

當建立一個Promise object 時，會在heap記憶體建立其區塊，並設定state、result這兩個屬性，其中被Promise object包含的任務可透過該Promise object所提供的resolve、reject方法來對該Promise object 所在的記憶體內來寫入狀態和result

**其中被Promise object包含的任務可透過該Promise object所提供的resolve、reject方法** 中的Promise object會是對應先前建立的Promise object所在的記憶體位址



## 複習

#🧠 JavaScript：由Promise 物件所包覆的任務是如何在記憶體層面下回報自己狀態和結果告知程式模組來進行合適的事件處理？->->-> `當建立一個Promise object 時，會在heap記憶體建立其區塊，並設定state、result這兩個屬性，其中被Promise object包含的任務可透過該Promise object所提供的resolve、reject方法來對該Promise object 所在的記憶體內來寫入狀態和result`
<!--SR:!2023-04-02,11,230-->



---
Status: #🌱 
Tags:
[[JavaScript]] - [[Promise]]
Links:
References: