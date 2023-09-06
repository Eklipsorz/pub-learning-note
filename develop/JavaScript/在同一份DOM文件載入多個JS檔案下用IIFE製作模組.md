## 描述

### IIFE 模組下的背景

1. 同一份DOM文件載入多個JS檔案
2. 多個JS檔案在同份DOM Document 下會因為共享著GEC而處於相同的JS全域環境
3. 這些檔案能夠共享window

[[IIFE 是為了解決JavaScript 在同一份DOM Document載入多個JS檔案而產生出全域污染問題而提出的概念，具體實現是利用function、closure、grouping operator、圓括號來達成]]



### IIFE模組的構建
1.  勢必為了維護性，會以一個檔案作為一個模組：
	- 模組內容會是IIFE所構成的功能函式和該功能函式所能共享的資料集合
	- 提供模組的形式：以一個物件包含所有能夠提供的功能函式，並輸出至全域環境當全域變數，或者當window的變數
[[@ithomeDay25MoKuaiHua]] 所提供：
```js
// module1.js
(function (window) {
  let _count = 0
  function foo() {
    _count += 1
  }
  
  function getCount() {
    foo()
    console.log(_count);
  }
  // 暴露給全局
  window.module1 = {
    // ES6 增強語法
    getCount,
  }
})(window)
```

2. 若IIFE構成的模組依賴其他模組，比如jQuery：
```html
// body部分
<body>
  <script
    src="https://code.jquery.com/jquery-3.5.1.js"
    integrity="sha256-QWo7LDvxbWT2tbbQ97B53yJnYU3WhH/C8ycbRAkjPDc="
    crossorigin="anonymous"
  ></script>
  <script src="./module1.js"></script>
</body>
```

```js
// module1.js
(function (window, $) {
  let _count = 0
  function foo() {
    _count += 1
  }
  
  function getCount() {
    foo()
    console.log(_count);
  }
  function changeColor() {
    console.log(++_count);
    $('body').css('background', 'red')
  }
  window.module1 = {
    // ES6 增強語法
    getCount,
    changeColor
  }
})(window, jQuery)
```


### IIFE模組化的缺點：
[[@jzhishuQianDuanMoZuHuaIIFECommonjsAMD]] 所描述的缺點
> 上述例子展示瞭如何用IIFE來定義模組，這樣寫有幾個**缺點**：
> 
> -   定義了3個模組，那麼就引入了3個js指令碼，那如果有更多模組呢，那就意味著很頁面載入時會像伺服器發起多次http請求，這是不好的
> -   html中script的標籤順序是固定的，因為模組main依賴moduleB，moduleB依賴moduleA，所以moduleA必須先宣告，這樣在moduleB的IIFE執行時候才能正常，不然會拋處ReferenceError

[[@linclarkESModulesCartoon]] 所描述的缺點：
> First, all of your script tags need to be in the right order. Then you have to be careful to make sure that no one messes up that order.

> The dependencies between these different parts of your code are implicit. Any function can grab anything on the global, so you don’t know which functions depend on which scripts.

> A second problem is that because these variables are on the global scope, every part of the code that’s inside of that global scope can change the variable. Malicious code can change that variable on purpose to make your code do something you didn’t mean for it to, or non-malicious code could just accidentally clobber your variable.

造成問題：
- 檔案依賴：
	- 依賴模組的載入順序：得清楚知道每個模組依賴哪些模組，依賴模組載入順序要正確，不正確的話，會無法正常使用載入，若依賴的越多就越複雜
	- 多個模組和主程式碼的依賴關係有可能會無法確定：模組上的任何一個函式都有機會從全域環境上存取對應全域變數，若存取的全域變數是額外模組提供的，這讓人無法確定哪一個模組才是真正被依賴的
- 請求太多，使得效能出現耗損：
	- 模組越多，請求數越多
	- 模組不會按需求來載入：即使只有部分模組要載入依賴模組，但由於沒載入模組的管理(來按需載入)，還是得載入全部的依賴模組
	- webpage 若重複載入渲染會有重新發送索要模組之請求的疑慮：重複載入相同的webpage，可能會重新解析webpage內的程式碼而發送相同模組的索求請求
- 以IIFE作為基底的模組裡，模組間太容易能在全域環境下存取其全域變數：
	- 使得惡意程式模組可以透過更改全域變數來調用惡意程式下的功能模組
	- 合法程式模組可能會誤改到全域變數使得無法正常載入模組而報錯
	- 主程式可能會誤改到全域環境下的全域變數


## 複習
#🧠 IIFE 模組化開始時的背景是什麼？ ->->-> `同一份DOM文件載入多個JS檔案、多個JS檔案在同份DOM Document 下會共享著window所構成的全域環境、 這些檔案能夠共享window`
<!--SR:!2024-02-23,213,230-->


#🧠 如何在同份DOM文件載入多個JS檔案的情況下來用IIFE建立模組？一檔案一模組？如何提供給其他JS檔案？  ->->-> `一開始會為了維護問題，一檔案為一個模組，而每個模組皆以IIFE所構成的功能函式和該功能函式所能共享的資料集合，提供模組的形式就是設定一個全域變數或者替window物件增加屬性就能`
<!--SR:!2023-11-17,109,210-->


#🧠 請試著用IIFE來構建一個模組，模組下的功能函式叫做increment和getCount，increment 必須能夠增加模組內的count資料，getCount則是取得對應count資料  ->->-> ``
<!--SR:!2023-11-04,101,230-->


#🧠 若IIFE模組下的功能函式需要載入其他模組的話，需要注意什麼->->-> `注意它是不是以IIFE來構成的模組且輸出會不會以全域變數來輸出模組`
<!--SR:!2024-02-26,210,230-->


#🧠 如何在將由IIFE結構所構成的特定模組A來載入jQuery之情況下，來將特定模組A輸出至全域環境下，請用程式碼來表示->->-> `(function (window, $) { function changeColor() { console.log(++_count);  $('body').css('background', 'red') } window.module1 = {  // ES6 增強語法 changeColor } })(window, jQuery)`
<!--SR:!2023-09-16,34,170-->



#🧠 (重複)如何在將由IIFE結構所構成的特定模組A來載入jQuery之情況下，來將特定模組A輸出至全域環境下，請用程式碼來表示->->-> `(function (window, $) { function changeColor() { console.log(++_count);  $('body').css('background', 'red') } window.module1 = {  // ES6 增強語法 changeColor } })(window, jQuery)`
<!--SR:!2023-10-21,48,237-->



#🧠 如何在HTML載入以IIFE為主且以全域變數來輸出功能的模組 ->->-> ` <script  src="https://code.jquery.com/jquery-3.5.1.js"  integrity="sha256-=QWo7LDvxbWT2tbbQ97B53yJnYU3WhH/C8ycbRAkjPDc=" crossorigin="anonymous"></script>`
<!--SR:!2025-02-05,561,250-->

#🧠  IIFE模組化的缺點有哪些？ ->->-> `- 檔案依賴：依賴模組的載入順序、多個模組和主程式碼的依賴關係有可能會無法確定 - 請求太多，使得效能出現耗損 - 以IIFE作為基底的模組裡，模組間太容易能在全域環境下存取其全域變數 `
<!--SR:!2023-09-28,198,248-->


#🧠 檔案依賴為IIFE模組化的缺點之一，請說明為什麼？(提示有兩個)->->-> `檔案依賴上主要有依賴模組的順序、多個模組和主程式碼之間的依賴關係有可能會無法確定。前者是強迫開發者得清楚了解依賴模組的載入順序，不正確會無法正常執行，且依賴的越多，就越複雜。後者是因爲模組們由於共享同一個全域環境上的全域變數，模組的任一函式都有可能因為存取到的全域變數是其他模組，而使模組間的依賴關係產生，而這份關係又不是正常開發手段要出現的。`
<!--SR:!2023-09-20,197,248-->



#🧠 請求太多為IIFE模組化的缺點之一，請說明為什麼？(請說明真正造成浪費的點) ->->-> `	- 模組越多，請求數越多 - 模組不會按需求來載入：即使只有部分模組要載入依賴模組，但由於沒載入模組的管理(來按需載入)，還是得載入全部的依賴模組 - webpage 若重複載入渲染會有重新發送索要模組之請求的疑慮：重複載入相同的webpage，可能會重新解析webpage內的程式碼而發送相同模組的索求請求`
<!--SR:!2023-09-24,60,227-->
<!--SR:!2023-02-02,24,228-->

#🧠 請求太多為IIFE模組化的缺點之一，請說明為什麼？(請說明真正造成浪費的點) ->->-> `	- 模組越多，請求數越多 - 模組不會按需求來載入：即使只有部分模組要載入依賴模組，但由於沒載入模組的管理(來按需載入)，還是得載入全部的依賴模組 - webpage 若重複載入渲染會有重新發送索要模組之請求的疑慮：重複載入相同的webpage，可能會重新解析webpage內的程式碼而發送相同模組的索求請求`
<!--SR:!2023-09-24,60,227-->


#🧠 模組間太容易能在全域環境下存取其全域變數為IIFE模組化的缺點之一，請說明為什麼？  ->->-> `	- 使得惡意程式模組可以透過更改全域變數來調用惡意程式下的功能模組 - 合法程式模組可能會誤改到全域變數使得無法正常載入模組而報錯 - 主程式可能會誤改到全域環境下的全域變數`
<!--SR:!2023-10-04,65,228-->




#🧠 IIFE模組化載入的模組越多，效能會發生什麼？ ->->-> `即使只有部分模組要載入依賴模組，但由於沒載入模組的管理(來按需載入)，還是得載入全部的依賴模組，這使得每次DOM Document的渲染 很有可能會讓所有對應依賴模組重新載入一次，進而使效能發生不必要的耗損`
<!--SR:!2023-11-06,60,208-->



#🧠 請舉例說明為什麼模組載入順序會是IIFE模組化的缺點？ ->->-> `假設moduleA被moduleB所依賴，而moduleB 被module C依賴 <script type="text/javascript" type="./moduleA.js"></script><script type="text/javascript" type="./moduleB.js"></script> <script type="text/javascript" type="./main.js"></script>，若考慮更多模組，那麼其順序會更為複雜，使開發者更難維護`
<!--SR:!2023-09-25,197,248-->




---
Status: #🌱 
Tags:
[[JavaScript]] 
Links:
[[當在DOM Document上的script寫上語法時，實際上是以DOM Document下的BOM Tree之window物件所構築的全域環境執行]]
References:
[[@linclarkESModulesCartoon]]
[[@ithomeDay25MoKuaiHua]]
[[@jzhishuQianDuanMoZuHuaIIFECommonjsAMD]][[@axinQianTanJSQianDuanMoZuHuaDeJiZhongGuiFanChengShiSheJiChengShiRenSheng]]