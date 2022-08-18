## 描述

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


開發階段會由React.StrictMode所包裹著，它會多執行1~N次生命週期會遇到的階段函式來檢測渲染期間的生命週期是否出現預期以外的副作用。

这些生命周期有：

-   `constructor`
-   `componentWillMount` (或者 UNSAFE_componentWillMount)
-   `componentWillReceiveProps` (或者 UNSAFE_componentWillReceiveProps)
-   `componentWillUpdate` (或者 UNSAFE_componentWillUpdate)
-   `getDerivedStateFromProps`
-   `shouldComponentUpdate`
-   `render`
-   `setState` 更新函数 (第一个参数)
    


基本上會藉由重複執行來比對結果來判斷
這只會發生在開發階段，部署階段並不會有React.StrictMode，所以可以避免這樣子的試錯


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
      <React.StrictMode>        <div>
          <ComponentOne />
          <ComponentTwo />
        </div>
      </React.StrictMode>      <Footer />
    </div>
  );
}
```

> 在上面的範例裡，嚴格模式檢查將_不會_跑在 `Header` 和 `Footer` 元件上。然而 `ComponentOne` 和 `ComponentTwo`，以及它們底下的所有子依賴，都會被檢查。

## 複習
#🧠 Question :: ->->-> ``

---
Status: #🌱 
Tags:
[[React]] - [[JavaScript]]
Links:
References:
[[@fakiolasMyReactComponents]]
[[@tanglie1993YiWoDeReact]]
[[@reactYanGeMoShiReact]]