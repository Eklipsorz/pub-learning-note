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


JSX 實際上來說是什麼？`是一個包裝建立&對應Virtual DOM原生方法的語法糖`


為了讓開發者更容易地去開發Virtual DOM來對應實際的DOM，所以才提出JSX這 **語法糖** 語言體系，最主要是將以下語法來簡化：
	- 建立&對應Virtual DOM的React原生方法


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
1. 每一個JSX元素都會是代表著React.createElement(...)回傳的節點，該節點會是一個包含多個子節點的parent節點
```
(
	<h2>Let's get started!</h2>
    <Expenses expenses={expenses}></Expenses>
)
```


```
(
	<XML code>
)
```

會分別轉換成：
```
(
	React.createElement('h2', {}, ...)
	React.createElement(Expenses, { expenses }, ....)
)
```
和
```
React.createElement(...)
```

2. 搭配最外圍的return 會形成：
```
return (
	React.createElement('h2', {}, ...)
	React.createElement(Expenses, { expenses }, ....)
)
```
和
```
return React.createElement(...)
```

3. 然而實際上JSX卻呈現著多個parent節點，而return 只能夠回傳單一物件/值，換言之，只能回傳一個parent節點
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
<!--SR:!2024-08-03,435,250-->

#🧠 React：使用著React 函式庫來調用建立Virtual DOM和對應DOM的語法，會有什麼樣的問題？ ->->-> `載入方式很多餘：每個代表元件的檔案都必須要載入、開發/維護難度提升，開發Virtual DOM會相當繁瑣、冗長`
<!--SR:!2023-09-02,204,230-->


#🧠 React.createElement 語法是做什麼的？ 簡述一下用途？->->-> `該語法會建立Virtual DOM節點並回傳對應DOM節點物件`
<!--SR:!2023-06-20,194,250-->

#🧠 React.createElement(A,B,C) 語法中的A、B和C各是做什麼的？ 簡述一下用途？ ->->-> `A指定建立後的DOM種類為何、B則是指定DOM節點會有什麼樣的attributes、C是指定DOM節點所包含的子節點`
<!--SR:!2023-12-29,108,230-->

#🧠 React：在沒有使用JSX的時期，如何使用React函式庫來轉換以下對應DOM結構？![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1660485103/blog/react/react-element/react-expected-result_cpazde.png)->->-> `![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1660485104/blog/react/react-element/react-actual-result_ajx4rn.png)`
<!--SR:!2023-09-29,99,230-->


#🧠 JSX 實際上來說是什麼？->->-> `是一個包裝建立&對應Virtual DOM原生方法的語法糖`
<!--SR:!2024-01-06,240,230-->

#🧠 JSX 實際上包裝了什麼來做成語法糖？ ->->-> `建立&對應Virtual DOM的React原生方法`
<!--SR:!2024-07-30,350,230-->

#🧠 當系統解析JSX語法，會做什麼樣的轉換？->->-> `自動載入react import React from 'react'; 2. 轉換成React object的建立&對應DOM方法來得到對應畫面，比如
<!--SR:!2023-06-28,180,230-->
`React.createElement(...)`


#🧠 為什麼使用JSX語法糖的React Element 只能接受一個parent element，講個大概就好 ->->-> `每一個JSX語法都會是代表著React.createElement(...)回傳的節點，該節點會是一個包含多個子節點的parent節點、然而實際上JSX卻呈現著多個parent節點，而return 只能夠回傳單一物件/值，換言之，只能回傳一個parent節點，在這樣情況下，只能選擇一個或者都不選，哪一個都無法按照JSX代表意思來使原生方法實現。`
<!--SR:!2024-11-18,503,250-->

#🧠 每個JSX元素語法-\<Element1\>.... \<\/Element1\>被React看作是？以程式碼來表示 ->->-> `React.createElement(Element1, {...}, ....)`
<!--SR:!2023-11-17,261,249-->

#🧠 每個JSX元素語法-\<Element1\>.... \<\/Element1\>被React看作是？以文字來描述 ->->-> `被看作以React函式庫的createElement語法來建立對應元件。`
<!--SR:!2024-01-01,293,249-->

#🧠 以下是JSX語法，系統會自動解析成什麼？請用程式碼表示 ![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1660485660/blog/react/react-element/JSX-React-Element_xk0slt.png) ->->-> `( React.createElement('h2', {}, ...) React.createElement(Expenses, { expenses }, ....) )`
<!--SR:!2023-11-25,266,249-->


#🧠 系統會如何看待這段JSX代碼？請用程式碼表示![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1660485752/blog/react/react-element/JSX-React-Element-Example_qkhdoe.png)->->-> `React.createElement(...)`
<!--SR:!2023-10-23,244,249-->



---
Status: #🌱 
Tags:
[[React]] - [[JavaScript]]
Links:
[[JSX 是源自於React團隊額外從JavaScript衍生出來的語言，會搭配XML標籤語言來表示想要渲染出的畫面，JS則是處理畫面會有的處理]]
References:
[[@reactReactDingCengAPI]]