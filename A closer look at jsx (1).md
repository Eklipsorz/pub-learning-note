## 描述

在還沒有使用JSX的時期，得必須載入以下函式庫，才能製作Virtual DOM
```
import React from 'react';
```

這導致：
1. 每個代表元件的檔案都必須要載入
2. 開發Virtual DOM會相當繁瑣、冗長


in the past , import React from 'react';

其中JSX 是個語法糖  
JSX -> syntactic sugar

  

當系統解析syntactic sugar 會從那轉換成以下形式：

1. 自動載入react
`import React from 'react';`

2. 並以React 這object來渲染對應畫面，比如
`React.createElement(...)`

  
舉例：以下是JSX 的 syntactic sugar
```
return (
    <div>
      <h2>Let's get started!</h2>
      <Expenses expenses={expenses}></Expenses>
    </div>
  );
```

  

接著會轉換成以下程式碼來執行
```
import React from 'react';
import Expenses from './components/Expenses';

const h2Element = React.createElement('h2', {}, 'Let\'s get started!');
const expenseElement = React.createElement(Expenses, { items: expenses });
return React.createElement('div', {}, h2Element, expenseElement);
```


  
1. it should also be clear why you need some wrapping element as a root JSX element

2. why you can't have just these two side-by-side elements. e.g.,




  

每一個React Element 只能接受一個parent element的原因:

```
return (
    <h2>Let's get started!</h2>
    <Expenses expenses={expenses}></Expenses>
)
```

1. 轉換後的形式會是如下，其結果會是兩個語句，各會回傳對應DOM節點，但return 只能接收一個單一值/單一物件


```
// 方式1：什麼也沒回傳
return 
React.createElement('h2', {}, 'Let\'s get started!');
React.createElement(Expenses, { items: expenses });
```

```
// 方式2：回傳h2
return React.createElement('h2', {}, 'Let\'s get started!');
React.createElement(Expenses, { items: expenses });
```

```
// 方式3：回傳Expenses
React.createElement('h2', {}, 'Let\'s get started!');
return React.createElement(Expenses, { items: expenses });
```







  

參考資料
[[@reactReactDingCengAPI]] 
> 我們推薦使用 JSX 來描述你的 UI 應該長成什麼樣子。 每個 JSX element 都只是呼叫 `React.createElement()` 的語法糖。當你使用 JSX 的時候你將不需要直接呼叫以下的 method：
-   `createElement()`
-   `createFactory()`   

type 指定建立的Virtual DOM種類，props則是賦予DOM的屬性，children 則是DOM的子節點
```
React.createElement(
  type,
  [props],
  [...children]
)
```




## 複習


---
Status: #🌱 
Tags:
[[React]] - [[JavaScript]]
Links:
References:
[[@reactReactDingCengAPI]]