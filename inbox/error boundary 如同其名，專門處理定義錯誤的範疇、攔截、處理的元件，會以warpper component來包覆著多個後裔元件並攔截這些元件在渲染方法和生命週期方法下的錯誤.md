## 描述


### 發送錯誤資訊物件的主要來源

主要來源為：
- 元件上的事件處理 
- 元件上發送出的非同步任務
- 元件本身的生命週期方法



### 錯誤資訊物件的傳遞


假如說在上述來源上出現錯誤的話，那麼勢必會以拋出錯誤的形式來讓系統內部的錯誤處理程式模組能夠攔截
```
1.  if (this.props.users.length === 0) {
2.     throw new Error('No users provided!');
3.  }
```


當目前函式發出錯誤時：
- 會試著從目前函式下尋找可攔截錯誤資訊物件並處理的程式模組
- 若沒有就會往當初該執行環境下被呼叫的地方所在的函式A尋找可攔截錯誤資訊物件並處理的程式模組
- 在沒有就從函式A被呼叫的所在尋找可攔截錯誤資訊物件並處理的程式模組，直到找得到可攔截並處理為止
- 若沒有的話，React 會報錯，最後並阻止其渲染


#### 錯誤資訊物件的處理

[[@nachao2022NianQianDuanReactDe100DaoMianShiTiDeDi15TiCuoWuBianJieJueJin]]
> ### 问题
    React17 中错误边界（Error Boundaries）能正常捕获错误的场景有哪些？
> ### 选项

> A. 绑定DOM的事件方法中的错误。
> B. 异步代码中的错误。
> C. 任意子组件树的渲染方法 `render()` 和所有生命周期方法中的错误。
> D. 错误边界组件自身的错误。


若是處於以下狀況的錯誤
-  元件上的事件處理
-  元件上發送出的非同步任務 (setTimeout、Promise)

就以JS語言體系的try...catch來解決，但無法使用error-boundary元件來解決，原因在於其元件只能攔截元件的渲染方法和所有生命週期方法中的錯誤，這兩種情況很有可能會是渲染方法或者生命週期方法之後才出現


### error boundary

error boundary：
- 如同其名，專門處理定義錯誤的範疇、攔截、處理的元件，會以warpper component來包覆著多個元件，這些後裔元件只要在渲染方法或者所有生命週期函式執行時發生錯誤，即可被error-boundary 元件給攔截到
- 本質上是一個標準的class-based component，但會夾雜著componentDidCatch 這生命週期方法（lifecycle method) 或者 static getDerivedStateFromError
- 目前functional component並沒辦法支援componentDidCatch，故此要實現error boundary只能在class-based component

#### error boundary 侷限性
> A. 绑定DOM的事件处理方法中的错误无法被捕获到。（因为在触发交互前，组件的生命周期和渲染都已经被执行。如果需要捕获事件的方法中的错误，需要使用 JS 的 `try / catch` 方法。）
>
> B. 异步代码中的错误无法被捕获到。（包括 setTimeout、Promise 等，原因与A同理。）
>
> D. 错误边界组件自身错误无法被捕获，而是会被上层的错误边界组件给获取。

它無法處理：
- 元件上的事件處理所產生的錯誤
- 元件上的非同步任務所產生的錯誤
- error-boundary 元件本身並不能夠被自己攔截到，只能被上層的error-boundary元件攔截到

#### error boundary 定義
[[@nachao2022NianQianDuanReactDe100DaoMianShiTiDeDi15TiCuoWuBianJieJueJin]]

> 在 class 组件中定义了 static getDerivedStateFromError() 或 componentDidCatch() 这两个生命周期方法中的任意一个（或两个）时，那么它就变成一个错误边界。

成立error-boundary的條件：
- 必須是class-based component
- 定義componentDidCatch 這生命週期方法（lifecycle method) 或者 static getDerivedStateFromError


#### componentDidCatch 語法

> well, this lifecycle method will be triggered whenever one of the child components throws an error or generates an error

componentDidCatch 生命週期函式
- 語法：
	- - error 會是被攔截到的錯誤資訊物件，會由react負責轉遞過來
```
componentDidCatch(error) {
	....
}
```
- 通常處理方式會是：搭配狀態註冊，來在componentDidCatch切換狀態以及觸發渲染
```
1.  componentDidCatch(error) {
2.    // 根據error種類來訂製各個錯誤處理
3.    this.setState({ hasError: true});
4.  }
```

##### componentDidCatch  & getDerivedStateFromError 觸發時間點
[[@reactReactComponentReact]]
> This lifecycle is invoked after an error has been thrown by a descendant component.

重點：
- 只要其後裔元件的渲染方法和任一生命週期方法拋出錯誤，就會執行error-boundary下的componentDidCatch


### error-boundary 常見實作方式

1. 製作一個

error boundary
1. 設定成wrapper component 來包含多個component，以此讓這些component發生錯誤時，可以先被error boundary攔截到
2. 註冊hasError這狀態來好讓後頭渲染內容根據狀態來變動，比如發生錯誤就印出代表錯誤訊息的頁面；沒發生錯誤就正常渲染
3. 在開發模式，會因為錯誤資訊來特意顯示，實際上，對應的error-boundary有呈現對應畫面；在production階段並不會呈現錯誤資訊

### boundary


> a real or imagined line that marks the edge or limit of something

重點：
- boundary 是一條線，標記著特定事物的邊緣或者特定情況下的上/下限

## 複習


---
Status: #🌱 
Tags:
[[React]]
Links:
References:
[[@reactReactComponentReact]]
[[@nachao2022NianQianDuanReactDe100DaoMianShiTiDeDi15TiCuoWuBianJieJueJin]]