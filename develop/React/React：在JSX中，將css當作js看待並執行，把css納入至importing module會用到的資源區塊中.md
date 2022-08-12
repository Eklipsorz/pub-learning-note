## 描述
```
import './ExpenseItem.css'
```


重點：
- 在JSX中，將css當作js看待並執行，把css納入至importing module會用到的資源區塊中
- 預設情況下，webpack會將import css file視為該component 所要載入的css檔案，使用時就按照給定的樣式名稱來從importing module會用到的資源區塊中找到對應樣式名稱，最後webpack針對這component所生成的網頁會自動載入對應css檔案
- 具體要讓JSX渲染畫面使用對應CSS檔案

### import 'xxxx' 使用

> 僅作為副作用引入模塊
> 僅作為副作用（side effect）引入整個模塊，而不直接引入任何東西。這樣會在不引入實際數值的情況下，執行整個模塊的程式。

```
import '/modules/my-module.js';
```


[[Side Effect 是強調著特定操作、表達式、函式的處理過程，除了會影響自身所處於的執行環境以外，還會影響其他環境下本身或者其環境下的資料，如全域變數、共享用的資源]]

重點：
-  這類型import用途會是：import 到的模組會作為產生副作用或者修改主要importing module會用到的資源
- 利用執行該模組的top-level code來修改主要importing module會用到的資源
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

  

  

僅作為副作用（side effect）引入整個模塊，而不直接引入任何東西。這樣會在不引入實際數值的情況下，執行整個模塊的程式。


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
#🧠  import 'xxxx' 使用 是做什麼用的？ ->->-> `這類型import用途會是：import 到的模組會作為產生副作用或者修改主要importing module會用到的資源`
<!--SR:!2022-08-14,2,230-->

#🧠 import 'xxxx' 用途是修改主要importing module會用到的資源，具體如何做？ ->->-> `利用執行該模組的top-level code來修改主要importing module會用到的資源`
<!--SR:!2022-08-13,2,248-->

#🧠 在JSX中，執行import './ExpenseItem.css'會是？->->-> `把css納入至importing module會用到的資源區塊中`
<!--SR:!2022-08-13,2,248-->

#🧠 在JSX中，執行import './ExpenseItem.css'會是把css納入至importing module會用到的資源，那麼能夠讓XML使用樣式名稱嗎？為何 ->->-> `能，預設情況下，webpack會將import css file視為該component 所要載入的css檔案，使用時就按照給定的樣式名稱來從importing module會用到的資源區塊中找到對應樣式名稱`

#🧠 在JSX中，執行import './ExpenseItem.css'後，對應component的網頁會有這css嗎？ ->->-> `最後webpack針對這component所生成的網頁會自動載入對應css檔案`
<!--SR:!2022-08-13,2,248-->

#🧠 如何讓JSX中的XML表達元件增加樣式？ 以一個名為Component的元件來表達->->-> `添加className，<Component className='.....'></Component>`

#🧠 React：為何不讓JSX中的XML表達元件使用class？ ->->-> `由於XML是JSX語言的一部分，且class會跟JavaScript原生語法中的class起衝突，所以React會以className來替代指定每個元件的樣式`

---
Status: #🌱 
Tags:
[[React]] - [[JavaScript]]
Links:
[[Side Effect 是強調著特定操作、表達式、函式的處理過程，除了會影響自身所處於的執行環境以外，還會影響其他環境下本身或者其環境下的資料，如全域變數、共享用的資源]]
References:
[[@AddingStylesheetCreate]]