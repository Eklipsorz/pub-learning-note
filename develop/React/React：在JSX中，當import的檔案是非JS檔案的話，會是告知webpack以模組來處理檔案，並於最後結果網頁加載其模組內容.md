## 描述
```
import './ExpenseItem.css'
```

重點：
- 在JSX中，當import的檔案是非JS檔案的話，會是告知webpack以模組來處理檔案，並於最後結果網頁加載其模組內容，好讓元件能夠使用其樣式
- 具體要讓JSX渲染畫面使用對應CSS檔案

### import 'xxxx' 使用

> 僅作為副作用引入模塊
> 僅作為副作用（side effect）引入整個模塊，而不直接引入任何東西。這樣會在不引入實際數值的情況下，執行整個模塊的程式。

```
import '/modules/my-module.js';
```


[[side effect 是指調用者執行特定操作或表達式或函式而得到除了回傳值給調用者這個主要效果以外的額外效果，side effect 通常會是影響主調用者所使用的共享資源之效果]]

重點：
- 若xxxx是JS檔案，這類型import用途會是：
	- import 到的模組會作為產生副作用或者修改主要importing module會用到的資源
- 若xxxx是非JS檔案且在React中，只是通知webpack哪些是要處理的模組
### 參考案例

[[@AddingStylesheetCreate]] 所描述
#### `Button.css`
```
1.  .Button {
2.       padding: 20px;
3.  }
```


#### `Button.js`
```
1.  import React, { Component } from 'react';

3.  import './Button.css'; // Tell webpack that Button.js uses these styles
4.  class Button extends Component {
5.       render() {
6.            // You can use them as regular CSS styles
7.           return <div className="Button" />;
8.       }
9.  }
```


https://create-react-app.dev/docs/adding-a-stylesheet/


### 讓JSX中的XML表達元件增加樣式
1. 理論上是得替每個元件以class來指定樣式：
```
<Component class='.....'></Component>
```
2. 由於XML是JSX語言的一部分，且class會跟JavaScript原生語法中的class起衝突，所以React會以className來替代指定每個元件的樣式
```
<Component className='.....'></Component>
```



## 複習
#🧠  import 'xxxx'且xxxx為JS檔案 使用 是做什麼用的？ ->->-> `這類型import用途會是：import 到的模組會作為產生副作用或者修改主要importing module會用到的資源`
<!--SR:!2023-10-01,212,230-->


#🧠  在React中， import 'xxxx' 使用且xxxx為非JS檔案 是做什麼用的？ ->->-> `告知webpack哪些模組要被處理`
<!--SR:!2025-01-21,525,250-->

#🧠 import 'xxxx'且xxxx為JS檔案， 用途是修改主要importing module會用到的資源，具體如何做？ ->->-> `利用執行該模組的top-level code來修改主要importing module會用到的資源`
<!--SR:!2023-12-28,107,230-->


#🧠 在JSX中，執行import './ExpenseItem.css'會是？->->-> `告知webpack將對應CSS檔案以模組來處理`
<!--SR:!2024-01-24,291,250-->


#🧠 在JSX中，執行import './ExpenseItem.css'會是把css納入至importing module會用到的資源，那麼能夠讓XML使用樣式名稱嗎？為何 ->->-> `能，告知webpack將對應CSS檔案以模組來處理，並於最後結果網頁加載對應CSS內容`
<!--SR:!2023-08-02,193,250-->


#🧠 在JSX中，執行import './ExpenseItem.css'後，對應component的網頁會有這css嗎？ ->->-> `最後webpack針對這component所生成的網頁會自動載入對應css檔案`
<!--SR:!2025-01-03,507,250-->


#🧠 如何讓JSX中的XML表達元件增加樣式？ 以一個HTML元件來表達->->-> `添加className，<div className='.....'></div>`
<!--SR:!2023-12-31,230,228-->


#🧠 React：為何不讓JSX中的XML表達元件使用class？ ->->-> `由於XML是JSX語言的一部分，且class會跟JavaScript原生語法中的class起衝突，所以React會以className來替代指定每個元件的樣式`
<!--SR:!2025-03-19,570,248-->

---
Status: #🌱 
Tags:
[[React]] - [[JavaScript]]
Links:
[[side effect 是指調用者執行特定操作或表達式或函式而得到除了回傳值給調用者這個主要效果以外的額外效果，side effect 通常會是影響主調用者所使用的共享資源之效果]]
References:
[[@AddingStylesheetCreate]]