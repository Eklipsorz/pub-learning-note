## 描述


### 模組載入方式分為三階段

Common JS ：

-   將每個模組的載入分成construction、instantiation、evaluation三個階段(在這裡CommonJS並不會特意分割這三個階段)



### CommonJS源自於伺服器端

CommonJS 本身是源自於伺服器端的模組化標準，其模組皆源自於伺服器本機端，只考量如從硬碟獲取對應模組內容並載入至特定區塊，所以並沒有考量網路上的傳輸延遲問題，網路上的傳輸延遲會比從本機端獲取模組來得慢。



### 單個CommonJS模組的載入
> The CommonJS approach has a few implications, and I will explain more about those later. But one thing that it means is that in Node with CommonJS modules, you can use variables in your module specifier. You are executing all of the code in this module (up to the `require` statement) before you look for the next module. That means the variable will have a value when you go to do module resolution.


[![A require statement which uses a variable is fine. An import statement that uses a variable is not.](https://2r4s9p1yi1fa2jd7j43zph8r-wpengine.netdna-ssl.com/files/2018/03/13_static_import-500x146.png)](https://2r4s9p1yi1fa2jd7j43zph8r-wpengine.netdna-ssl.com/files/2018/03/13_static_import.png)

當需求方以Require來指定特定JS檔案，就會將JS檔案視為CommonJS模組檔案，這時JS引擎會先於編譯期間替module 建立模組實例來存放要輸出給內容，接著執行該模組的top-level code 來產生模組要輸出的內容以及執行輸出模組內容的語句，如：

```
exports = module.exports = ....
```

實際上會將模組實例複製一份讓發送require的那一份獲取副本，所以實際上是透過執行模組來獲取模組所要輸出的內容。

> This is different from CommonJS modules. In CommonJS, the entire export object is copied on export. This means that any values (like numbers) that are exported are copies.

> This means that if the exporting module changes that value later, the importing module doesn’t see that change.


![](https://hacks.mozilla.org/files/2018/03/31_cjs_variable-768x174.png)



### CommonJS 特點

因此CommonJS設計上會是：

1.  以模組在本機端儲存設備上為前提而設計
2.  每個模組的載入皆是同步處理：目前模組的載入必須等待前面模組的載入階段都完成才能做
3.  載入形式：執行模組來載入模組實例至需求方
4.  沒特意將模組載入細分成建構、實例化、確定值這幾個階段，而是會透過DFS遍歷模組依賴關係的底部
5.  模組的依賴關係遍歷會是DFS




> The CommonJS approach has a few implications, and I will explain more about those later. But one thing that it means is that in Node with CommonJS modules, you can use variables in your module specifier. You are executing all of the code in this module (up to the `require` statement) before you look for the next module. That means the variable will have a value when you go to do module resolution.

> But with ES modules, you’re building up this whole module graph beforehand… before you do any evaluation. This means you can’t have variables in your module specifiers, because those variables don’t have values yet.

CommonJS 模組是指需求方只要以JS檔案來執行其模組，其模組本身是透過執行模組期間輸出模組內容至需求方，所以由於透過執行來獲取模組內容，所以本身可以透過執行狀況來變更其他要被載入的模組



## 複習
#🧠 Question :: ->->-> ``

---
Status: #🌱 
Tags:
[[JavaScript]]
Links:

References: