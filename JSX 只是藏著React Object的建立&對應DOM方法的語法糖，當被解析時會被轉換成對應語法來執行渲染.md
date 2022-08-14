## 描述


### 沒有JSX之前的時期

在還沒有使用JSX的時期，得必須載入以下函式庫，才能製作Virtual DOM
```
import React from 'react';
```

且若要渲染出以下預期結果的話
```
<div>
	<h2>Let's get started!</h2>
	<Expenses expenses={expenses}></Expenses>
</div>
```

就得React 函式庫裡頭的createElement來建立Virtual DOM來實現：
```
return React.createElement(
	'div',
	{},
	React.createElement('h2', {}, "Let's get started!"),
	React.createElement(Expenses, { items: expenses })
);
```

這樣問題會導致：
1. 載入方式很多餘：每個代表元件的檔案都必須要載入
```
import React from 'react';
```
2. 開發/維護難度提升，開發Virtual DOM會相當繁瑣、冗長

#### React.createElement 語法
[[@reactReactDingCengAPI]] 
該語法會建立Virtual DOM節點並回傳對應DOM節點物件，其中參數：
- type 指定建立的Virtual DOM種類
- props 則是賦予DOM的屬性
- children 則是DOM的子節點
```
React.createElement(
  type,
  [props],
  [...children]
)
```


### JSX 只是個語法糖


[[@reactReactDingCengAPI]] 
> 我們推薦使用 JSX 來描述你的 UI 應該長成什麼樣子。 每個 JSX element 都只是呼叫 `React.createElement()` 的語法糖。當你使用 JSX 的時候你將不需要直接呼叫以下的 method：
> -   `createElement()`
> -   `createFactory()`   

為了讓開發者更容易地去開發Virtual DOM來對應實際的DOM，所以才提出JSX這 **語法糖** 語言體系，最主要是將以下語法來簡化：
	- 建立Virtual DOM的方式


#### 當系統解析JSX語法時

當系統解析JSX語法時，會從JSX轉換成以下形式：

1. 自動載入react
`import React from 'react';`
2. 轉換成React object的建立&對應DOM方法來得到對應畫面，比如
`React.createElement(...)`

#### 案例：當系統解析JSX語法時
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



### 為什麼React Element 只能接受一個parent element

  
考慮以下React Element出現在兩個parent element，正常情況下會因為**React element 只能以一個parent element來建立**而報錯
```
return (
    <h2>Let's get started!</h2>
    <Expenses expenses={expenses}></Expenses>
)
```

或者

```
const element = (
	<h2>Let's get started!</h2>
    <Expenses expenses={expenses}></Expenses>
)
```

具體來說，每一個React Element 只能接受一個parent element的原因：
1. 每一個JSX語法都會是代表著React.createElement(...)回傳的節點，該節點會是一個包含多個子節點的parent節點
```
(
	<h2>Let's get started!</h2>
    <Expenses expenses={expenses}></Expenses>
)
```

轉換後
```
return React.createElement(...)
```


2. 然而實際上出現多個parent節點，而return 只能夠回傳單一物件/值，換言之，只能回傳一個parent節點
```
return React.createElement(...)
```

回傳選擇方式會有以下選擇：
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

其結果就是沒辦法如預期那樣回傳多個parent節點

#### 結論 
為了確保JSX語法能夠和對應的React.createElement保持著都能回傳同樣內容，所以會強制以下規則給JSX語法：
	- 每一個React Element 都只會有一個包含多個子節點的parent節點



## 複習

#🧠 React：在沒有使用JSX的時期，都是用什麼來建立/對應DOM？->->-> `載入React函式庫並從中調用建立Virtual DOM和對應DOM的語法`

#🧠 React：使用著React 函式庫來調用建立Virtual DOM和對應DOM的語法，會有什麼樣的問題？ ->->-> `載入方式很多餘：每個代表元件的檔案都必須要載入、開發/維護難度提升，開發Virtual DOM會相當繁瑣、冗長`


#🧠 React.createElement 語法是做什麼的？ 簡述一下用途？->->-> `該語法會建立Virtual DOM節點並回傳對應DOM節點物件`


---
Status: #🌱 
Tags:
[[React]] - [[JavaScript]]
Links:
[[JSX 是源自於React團隊額外從JavaScript衍生出來的語言，會搭配XML標籤語言來表示想要渲染出的畫面，JS則是處理畫面會有的處理]]
References:
[[@reactReactDingCengAPI]]