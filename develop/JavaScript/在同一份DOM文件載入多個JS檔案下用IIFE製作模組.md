## 描述

### IIFE 模組下的背景
1. 同一份DOM Document 載入 多個JS檔案 即為在 DOM Document黏貼JS檔案對應的程式碼，並不會將各個檔案視為不同的全域環境
2. 同一份DOM Document 會經由瀏覽器分析成以window物件構成的BOM或者DOM，而所有在DOM Document 上的JS程式碼將會其文件對應的BOM window物件作為全域環境 
[[IIFE 是為了解決JavaScript 在同一份DOM Document載入多個JS檔案而產生出全域污染問題而提出的概念，具體實現是利用function、closure、grouping operator、圓括號來達成]]
	總結：
		- 同一份DOM文件載入多個JS檔案
		- 由於多個JS檔案在同份DOM Document 下會共享著window所構成的全域環境
		- 這些檔案能夠共享window


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
	- 依賴模組的順序：得清楚知道每個模組依賴哪些模組，依賴模組載入順序要正確，不正確的話，會無法正常使用載入，若依賴的越多就越複雜
	- 多個模組和主程式碼的依賴關係有可能會無法確定：模組上的任何一個函式都有機會從全域環境上存取對應全域變數，若存取的全域變數是額外模組提供的，這讓人無法確定哪一個模組才是真正被依賴的
- 請求太多，使得效能出現耗損：即使只有部分模組要載入依賴模組，但由於沒載入模組的管理(來按需載入)，還是得載入全部的依賴模組，這使得每次DOM Document的渲染 很有可能會讓所有對應依賴模組重新載入一次，進而使效能發生不必要的耗損
- 模組間會透過共同擁有的全域環境來更改對應全域變數


## 複習
#🧠 IIFE 模組化開始時的背景是什麼？ ->->-> `同一份DOM文件載入多個JS檔案、多個JS檔案在同份DOM Document 下會共享著window所構成的全域環境、 這些檔案能夠共享window`
<!--SR:!2022-07-29,3,250-->


#🧠 如何在同份DOM文件載入多個JS檔案的情況下來用IIFE建立模組？一檔案一模組？如何提供給其他JS檔案？  ->->-> `一開始會為了維護問題，一檔案為一個模組，而每個模組皆以IIFE所構成的功能函式和該功能函式所能共享的資料集合，提供模組的形式就是設定一個全域變數或者替window物件增加屬性就能`
<!--SR:!2022-07-29,3,250-->


#🧠 請試著用IIFE來構建一個模組，模組下的功能函式叫做increment和getCount，increment 必須能夠增加模組內的count資料，getCount則是取得對應count資料  ->->-> ``
<!--SR:!2022-07-29,3,250-->


#🧠 若IIFE模組下的功能函式需要載入其他模組的話，需要注意什麼->->-> `注意它是不是以IIFE來構成的模組且輸出會不會以全域變數來輸出模組`
<!--SR:!2022-07-29,3,250-->


#🧠 如何將被依賴模組載入至IIFE模組下的功能函式使用，假設被依賴模組jQuery是以IIFE所構成且以全域變數來輸出模組，請用程式碼來表示->->-> `(function (window, $) { function changeColor() { console.log(++_count);  $('body').css('background', 'red') } window.module1 = {  // ES6 增強語法 changeColor } })(window, jQuery)`
<!--SR:!2022-07-29,3,250-->

#🧠 如何在HTML載入以IIFE為主且以全域變數來輸出功能的模組 ->->-> ` <script  src="https://code.jquery.com/jquery-3.5.1.js"  integrity="sha256-=QWo7LDvxbWT2tbbQ97B53yJnYU3WhH/C8ycbRAkjPDc=" crossorigin="anonymous"></script>`
<!--SR:!2022-07-29,3,250-->

#🧠  IIFE模組化的缺點 ->->-> `- 檔案依賴：模組的檔案依賴關係會使載入非常繁瑣：一個檔案為一個模組，若要載入依賴模組必須**額外添加script和依賴的JS檔案才能實現**以及且要**按照載入順序來載入**、難以清楚知道模組之間的關係：本身無法單從HTML來看出IIFE模組還需要哪些模組，即使從JS檔案角度來看，參數名稱和引數名稱也只是使用關鍵字來識別源自於哪個模組 - 請求太多，使得效能出現耗損：即使只有部分模組要載入依賴模組，但由於沒載入模組的管理(來按需載入)，還是得載入全部的依賴模組，這使得每次DOM Document的渲染 很有可能會讓所有對應依賴模組重新載入一次，進而使效能發生不必要的耗損`
<!--SR:!2022-07-29,3,250-->

#🧠 IIFE模組化載入的模組越多，效能會發生什麼？ ->->-> `即使只有部分模組要載入依賴模組，但由於沒載入模組的管理(來按需載入)，還是得載入全部的依賴模組，這使得每次DOM Document的渲染 很有可能會讓所有對應依賴模組重新載入一次，進而使效能發生不必要的耗損`
<!--SR:!2022-07-29,3,250-->

#🧠 請舉例說明為什麼模組載入順序會是IIFE模組化的缺點？ ->->-> `假設moduleA被moduleB所依賴，而moduleB 被module C依賴 <script type="text/javascript" type="./moduleA.js"></script><script type="text/javascript" type="./moduleB.js"></script> <script type="text/javascript" type="./main.js"></script>，若考慮更多模組，那麼其順序會更為複雜，使開發者更難維護`
<!--SR:!2022-07-29,3,250-->


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