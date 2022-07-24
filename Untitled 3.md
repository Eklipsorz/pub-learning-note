## 描述

以IIFE作為模組：
1.  會以一個檔案作為一個模組，而模組內容會是IIFE所構成的功能函式和該功能函式所能共享的資料集合
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

2. 若IIFE構成的模組依賴其他模組，比如jQuery，那麼由IIFE必須要以jQuery模組提供的全域變數來載入至IIFE函式當參數呼叫
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


造成問題：
- 檔案依賴：
	- 難以清楚知道模組之間的關係：本身無法單從HTML來看出IIFE模組還需要哪些模組，即使從JS檔案角度來看，參數名稱和引數名稱也只是使用關鍵字來識別源自於哪個模組，
	- 模組的檔案依賴關係會使載入非常繁瑣：一個檔案為一個模組，若要載入依賴模組必須額外添加script和依賴的JS檔案才能實現
- 請求太多，使得效能出現耗損：即使只有部分模組要載入依賴模組，但由於沒載入模組的管理(來按需載入)，還是得載入全部的依賴模組，這使得每次DOM Document的渲染 很有可能會讓所有對應依賴模組重新載入一次，進而使效能發生不必要的耗損


## 複習
#🧠 Question :: ->->-> ``

---
Status: #🌱 
Tags:
[[JavaScript]]
Links:
References:
[[@ithomeDay25MoKuaiHua]]
[[@axinQianTanJSQianDuanMoZuHuaDeJiZhongGuiFanChengShiSheJiChengShiRenSheng]]