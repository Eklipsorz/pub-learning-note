
## 描述

[[@CodeSplittingReact]]
> The `React.lazy` function lets you render a dynamic import as a regular component.

> This will automatically load the bundle containing the `OtherComponent` when this component is first rendered.

> `React.lazy` takes a function that must call a dynamic `import()`. This must return a `Promise` which resolves to a module with a `default` export containing a React component.


React.lazy：
- 用途是替指定資源設定Lazy loading的功能
- 具體是將以dynamic import作為 callback 並根據指定資源是否要被渲染才執行對應callback來獲取對應的元件
    - dynamic import 具體會是以promise為主的import
- 語法：
    - callback 為函式物件，得是回傳Resolve為包含特定資源的模組的Promise 物件
    - 回傳會是標示為lazy-loading的React Component
	 ```
	React.lazy(callback)
	```
   -  當要載入對應其Component時，就會以非同步任務的形式來載入包含其資源的模組並獲取其中的對應Component。
- 細節：
   - 透過webpack編譯時就會進行code spliting來分割好幾份模組

#### 若要載入對應其Component時會遇到的問題
由於是以非同步任務形式來載入元件，所以在載入前可能會因為其元件


## 複習


---
Status: #🌱 
Tags:
[[React]]
Links:
References:
[[@CodeSplittingReact]]