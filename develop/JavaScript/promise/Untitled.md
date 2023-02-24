## 描述

當建立一個Promise object 時，會在heap記憶體區塊建立，並設定state和result這兩個屬性，其中被Promise object包含的任務可透過該Promise object所提供的resolve、reject方法來對該Promise object 寫入狀態和result

**其中被Promise object包含的任務可透過該Promise object所提供的resolve、reject方法** 中的Promise object會是對應先前建立的Promise object所在的記憶體位址

## 複習
#🧠 Question :: ->->-> ``

---
Status: #🌱 
Tags:
[[JavaScript]] - [[Promise]]
Links:
References: