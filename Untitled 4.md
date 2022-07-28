## 描述

> Blocking the main thread like this would make an app that uses modules too slow to use. This is one of the reasons that the ES module spec splits the algorithm into multiple phases. 
> 
> Splitting out construction into its own phase allows browsers to fetch files and build up their understanding of the module graph before getting down to the synchronous work of instantiating.


瀏覽器的模組源自於以下兩個地方，且效率會侷限於網路和存取設備，一般來說，網路速率會比存取設備還慢：

1.  第三方模組：網路上下載至本地端速率＋從本地端載入檔案至專案的速率
    
2.  本地端模組：從本地端載入檔案至專案的速率
    

大部分情況下，由於客戶端所需的模組都是源自第三方，且網路速率會比存取設備還慢，所以會非常依賴於網路速率

所以ES module spec才將模組載入分成三個階段：建構、實例化、確定/決定來試著以非同步形式來執行

其中建構步驟會是向第三方索要對應模組檔案並建立module graph來表示每個模組之間的依賴關係。

> build up their understanding of the module graph before getting down to the synchronous work of instantiating.

實例化對於同個模組的載入任務來說，會是依賴著建構任務完成才會做的任務，但是對於不同模組來說，卻可以是以非同步來完成


> CommonJS can do things differently because loading files from the filesystem takes much less time than downloading across the Internet. This means Node can block the main thread while it loads the file. 
> 
> And since the file is already loaded, it makes sense to just instantiate and evaluate (which aren’t separate phases in CommonJS). 
> 
> This also means that you’re walking down the whole tree, loading, instantiating, and evaluating any dependencies before you return the module instance.

CommonJS 本身是源自於伺服器端的模組化標準，其模組皆源自於伺服器本機端，只考量如從硬碟獲取對應模組內容並載入至特定區塊，所以並沒有考量網路上的傳輸延遲問題，網路上的傳輸延遲會比從本機端獲取模組來得慢。

因此CommonJS設計上會是：

1.  以模組在本機端儲存設備上為前提
    
2.  獲取模組以及載入模組的方式是同步(以建構、實例化、確定值這些階段來說)：在儲存設備找到模組→ 將模組轉化成實例 → 評估模組還有沒有依賴其他模組 → 執行模組所要執行的程式碼 → 回傳模組實例至需要載入的那一方
    
3.  沒特意將模組載入細分成建構、實例化、確定值這幾個階段
    
4.  模組的依賴關係遍歷會是DFS



![](https://hacks.mozilla.org/files/2018/03/12_cjs_require-768x457.png)
## 複習
#🧠 Question :: ->->-> ``

---
Status: 
Tags:
Links:
References: