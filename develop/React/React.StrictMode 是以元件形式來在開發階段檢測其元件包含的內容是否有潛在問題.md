## 描述


### React.StrictMode 檢測每個元件的生命週期(包含有沒有副作用)是否正確執行

[[@tanglie1993YiWoDeReact]]
> 如上所述，原因是 `React.StrictMode`。如果我们在应用中检查我们之前使用 `CRA` 运行的文件，我们会发现，我们的 `<App />` 组件被它包裹：

```jsx
ReactDOM.render(
  <React.StrictMode>
    <App />
  </React.StrictMode>,
  document.getElementById('root')
);
复制代码
```

> 显然，重新渲染并不是一个 bug，或者和库的渲染机制有关的东西。正相反，它是 `React` 提供的一种调试机制 🤗。

[[@reactYanGeMoShiReact]]
> ### 偵測意想不到的副作用

> 概念上，React 在兩種面相上能夠運作：
> -   **render** 面相決定了必須做出什麼改變到例如 DOM 的地方。在這個面相上，React 呼叫 `render` 然後比較了它與上一次 render 的結果。


開發階段會由React.StrictMode所包裹著，它會多執行1~N次生命週期會遇到的階段函式來檢測渲染期間的生命週期是否出現預期以外的副作用，基本上會藉由重複執行來比對結果來判斷

这些生命周期有：

-   `constructor`
-   `componentWillMount` (或者 UNSAFE_componentWillMount)
-   `componentWillReceiveProps` (或者 UNSAFE_componentWillReceiveProps)
-   `componentWillUpdate` (或者 UNSAFE_componentWillUpdate)
-   `getDerivedStateFromProps`
-   `shouldComponentUpdate`
-   `render`
-   `setState` 更新函数 (第一个参数)
    
### React.StrictMode 會檢測什麼？
[[@reactYanGeMoShiReact]]
> StrictMode 目前可以幫助：
- 發現擁有不安全生命週期的 component
-  警告使用了 legacy string ref API
- 警告使用到了被棄用的 findDOMNode
- 偵測意想不到的副作用
- 偵測 legacy context API
- 確保可重用的 state


重點：
- StrictMode 主要會檢測以下事物：
	- 每個元件的生命週期(包含有沒有副作用)是否正確執行
	- 是否使用舊有API和舊語法
	- 是否出現意想不到的副作用
	- 檢查每個元件的狀態是否正確
	- 檢測每個元件對應的DOM是否有問題

### React.StrictMode 會不會發生在部署階段
這只會發生在開發階段，部署階段並不會將React.StrictMode加入至部署時的內容，所以可以在部署階段避免這樣子的試錯

### React.StrictMode
[[@reactYanGeMoShiReact]]
> `嚴格模式`是一個用來突顯應用程式裡潛在問題的工具。

> 注意：
> 嚴格模式檢查只會在開發模式中執行；_它們不應該影響正式環境_。

```
import React from 'react';

function ExampleApplication() {
  return (
    <div>
      <Header />
      <React.StrictMode>        
	    <div>
          <ComponentOne />
          <ComponentTwo />
        </div>
      </React.StrictMode>      
      <Footer />
    </div>
  );
}
```

> 在上面的範例裡，嚴格模式檢查將_不會_跑在 `Header` 和 `Footer` 元件上。然而 `ComponentOne` 和 `ComponentTwo`，以及它們底下的所有子依賴，都會被檢查。

重點：
- React.StrictMode 是一個檢測開發時期是否有潛在問題的元件
- 具體來說，React.StrictMode會是以元件來表示，並只針對它所包含的內容來進行檢測，舉例來說：
	- React.StrictMode 包含的div元件會被檢查
	- 沒被React.StrictMode包含的元件不會被檢查，如Header元件、Footer元件

```
import React from 'react';

function ExampleApplication() {
  return (
    <div>
      <Header />
      <React.StrictMode>        
        <div>
          <ComponentOne />
          <ComponentTwo />
        </div>
      </React.StrictMode>      
      <Footer />
    </div>
  );
}
```

## 複習
#🧠  React.StrictMode 是用來作什麼？ ->->-> `是一個檢測開發時期是否有潛在問題的元件`
<!--SR:!2023-06-07,179,250-->



#🧠 請問React.StrictMode 對於以下元件會如何挑選並做檢測？![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1660817785/blog/react/strictmode/strictmode-example_nb6aio.png)->->-> `React.StrictMode會直接以它包含的元件來做檢測，比如div元件。以外的元件則不會被檢測，比如Header、Footer`
<!--SR:!2023-06-06,180,250-->

#🧠 React.StrictMode 具體會做什麼檢測？->->-> `檢測每個元件的生命週期是否正確執行、檢測每個元件的狀態、檢測是否有使用老舊語法&API、檢測每個元件對應的DOM節點是否有問題、檢測是否有其他副作用`
<!--SR:!2023-10-02,36,170-->




#🧠 React.StrictMode 會不會發生在部署階段？為什麼？->->-> `這只會發生在開發階段，部署階段並不會將React.StrictMode加入至部署時的內容，所以可以在部署階段避免這樣子的試錯`
<!--SR:!2024-02-08,325,250-->

---
Status: #🌱 
Tags:
[[React]] - [[JavaScript]]
Links:
References:
[[@fakiolasMyReactComponents]]
[[@tanglie1993YiWoDeReact]]
[[@reactYanGeMoShiReact]]
