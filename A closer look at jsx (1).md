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
#🧠 Question :: ->->-> ``

---
Status: #🌱 
Tags:
[[React]] - [[JavaScript]]
Links:
References:
[[@reactReactDingCengAPI]]