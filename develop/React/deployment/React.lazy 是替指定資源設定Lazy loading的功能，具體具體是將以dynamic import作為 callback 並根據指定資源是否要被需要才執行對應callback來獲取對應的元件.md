
## 描述

[[@CodeSplittingReact]]
> The `React.lazy` function lets you render a dynamic import as a regular component.

> This will automatically load the bundle containing the `OtherComponent` when this component is first rendered.

> `React.lazy` takes a function that must call a dynamic `import()`. This must return a `Promise` which resolves to a module with a `default` export containing a React component.



React.lazy：
- 用途是替指定資源設定Lazy loading的功能
- 具體是將以dynamic import作為 callback 並根據指定資源是否要被需要才執行對應callback來獲取對應的元件
    - dynamic import 具體會是以promise為主的import
- 語法：
    - callback 為函式物件，得是回傳Resolve為包含特定資源/元件的模組的Promise 物件
    - 回傳會是標示為lazy-loading的React Component
	 ```
	React.lazy(callback)
	```
   -  當要載入對應其Component時，就會以非同步任務的形式來載入包含其資源的模組並獲取其中的對應Component。
- 細節：
   - 透過webpack編譯時就會進行code spliting來分割好幾份模組

#### 若要載入對應其Component時會遇到的問題
由於是以非同步任務形式來載入元件，所以在載入前可能會因為其元件本身不存在而無法渲染，最後報錯


##### 解法：
1. 使用Suspense元件來監測後裔元件是否能正常渲染並提供fallback畫面的元件：其中Component 為被標記使用lazy-loading的React Component

```
<Suspense fallback={JSX Element}>
	<Component />
</Suspense>
```


## 複習

#🧠 React.lazy的用途是什麼？ ->->-> `用途是替指定資源設定Lazy loading的功能`
<!--SR:!2023-02-01,28,250-->

#🧠 React.lazy的用途是替指定資源設定Lazy loading的功能，具體是什麼？？ ->->-> `具體是將以dynamic import作為 callback 並根據指定資源是否要被需要才執行對應callback來獲取對應的元件`
<!--SR:!2023-01-04,10,250-->

#🧠 React.lazy的用途是替指定資源設定Lazy loading的功能，具體是將以dynamic import作為 callback 並根據指定資源是否要被需要才執行對應callback來獲取對應的元件，其中的dynamic import 會是什麼？ ->->-> `dynamic import 具體會是以promise為主的import`
<!--SR:!2023-01-29,26,250-->

#🧠 React.lazy語法為何？ ->->-> `React.lazy(callback)`
<!--SR:!2023-01-23,21,250-->

#🧠 React.lazy語法為`React.lazy(callback)`，那麼callback會是指什麼？ ->->-> `callback 為函式物件，得是回傳Resolve為包含特定資源/元件的模組的Promise 物件`
<!--SR:!2023-02-01,28,250-->

#🧠 React.lazy語法為`React.lazy(callback)`，那麼callback該如何設定，舉例 ->->-> `React.lazy(() => import(....))`
<!--SR:!2023-01-23,21,250-->


#🧠 React.lazy語法為`React.lazy(callback)`會回傳什麼？->->-> `回傳會是標示為lazy-loading的React Component`
<!--SR:!2023-02-01,28,250-->


#🧠 React.lazy語法為`React.lazy(callback)`會回傳會是標示為lazy-loading的React Component，具體能像Component擺放嗎？執行到會如何？ ->->-> `可以， 當要載入對應其Component時，就會以非同步任務的形式來載入包含其資源的模組並獲取其中的對應Component。`
<!--SR:!2023-01-04,10,250-->

#🧠 當React.lazy時就會替主要bundle做什麼？ ->->-> `透過webpack編譯時就會進行code spliting來分割好幾份模組`
<!--SR:!2023-02-01,28,250-->

#🧠 若要載入對應其被標記為lazy-loading的Component時，通常會遇到的問題是什麼？->->-> `由於是以非同步任務形式來載入元件，所以在載入前可能會因為其元件本身不存在而無法渲染，最後報錯`


#🧠 若要載入對應其被標記為lazy-loading的Component時，通常會遇到的問題是由於是以非同步任務形式來載入元件，所以在載入前可能會因為其元件本身不存在而無法渲染，最後報錯，那麼解法會是什麼？ ->->-> `使用Suspense元件來監測後裔元件是否能正常渲染並提供fallback畫面的元件`


#🧠 若要載入對應其被標記為lazy-loading的Component時，通常會遇到的問題是由於是以非同步任務形式來載入元件，所以在載入前可能會因為其元件本身不存在而無法渲染，最後報錯，那麼解法會是什麼？ 用程式碼舉例->->-> `<Suspense fallback={JSX Element}><Component /> </Suspense> 其中Component 為被標記使用lazy-loading的React Component`
<!--SR:!2023-01-22,20,250-->

#💻 請在/githubRepo/react-builder/react-deployment-practice領取題目並切換lazy-loading-all-routes分支，請將App.js上的Route上元件設定成lazy-loading  ->->-> ``
<!--SR:!2023-01-28,25,250-->


---
Status: #🌱 
Tags:
[[React]]
Links:
[[optimize code 目標為效能提升，手段會是minify、refactor、memorized value、code spliting、lazy loading。lazy-loading為當代碼需要的時候，才會載入該代碼，否則不載入]]
[[react 部署步驟：test code -> optimize code -> build app for production -> upload -> configure server]]
References:
[[@CodeSplittingReact]]