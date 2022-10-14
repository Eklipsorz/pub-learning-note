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
- 若都沒有的話，React 核心程式碼會在後頭接收錯誤來進行處理，其處理方式會是暫時停止執行渲染。

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
- 如同其名，專門處理定義錯誤的範疇、攔截、處理的元件，會以empty warpper component來包覆著多個元件，這些後裔元件只要在渲染方法或者所有生命週期函式執行時發生錯誤，即可被error-boundary 元件給攔截到
- 主要功能：攔截後裔元件所發送的錯誤資訊並進行處理，以避免後頭沒人處理錯誤資訊而讓React核心程式碼接收到並停止渲染。
- 本質上是一個標準的class-based component，但會夾雜著componentDidCatch 這生命週期方法（lifecycle method) 或者 static getDerivedStateFromError
- 目前functional component並沒有componentDidCatch的替代方案，故此要實現error boundary只能在class-based component

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

1. 先在建構式上定義hasError狀態，並設定初始值為false，表示一開始沒錯誤
2. 接著設定componentDidCatch 內增加setState，來讓hasError有機會轉換成true
3. 最後在render上設定能夠根據this.state.hasError是否為true來顯示錯誤訊息
4. 在UsersFinder中放置ErrorBoundary來包含想要攔截錯誤的後裔元件，在這裡會是Users元件

ErrorBoundary.js
```
import { Component } from 'react';

class ErrorBoundary extends Component {
  constructor() {
    super();
    this.state = { hasError: false };
  }

  componentDidCatch(error) {
    this.setState({ hasError: true });
  }

  render() {
    if (this.state.hasError) {
      return <p>Error</p>
    }
    return this.props.children;
  }
}

export default ErrorBoundary;

```

UsersFinder.js 
```
 render() {
    return (
      <Fragment>
        <div className={classes.finder}>
          <input type='search' onChange={this.searchChangeHandler.bind(this)} />
        </div>
        <ErrorBoundary>
          <Users users={this.state.filteredUsers} />
        </ErrorBoundary>
      </Fragment>
    );
  }
```

### boundary 命名緣由

> a real or imagined line that marks the edge or limit of something

重點：
- boundary 是一條線，標記著特定事物的邊緣或者特定情況下的上/下限

## 複習





#💻 請至/react-builder/question-review/class-based-component-question領取題目，並切換至error-boundary-to-class分支，實現ErrorBoundary元件來防止Users.js的錯誤拋錯衍生出的網頁崩潰問題->->-> `https://github.com/academind/react-complete-guide-code/blob/13-class-based-cmp/code/08-finished/src/components/ErrorBoundary.js`
<!--SR:!2022-10-18,3,250-->


---
Status: #🌱 
Tags:
[[React]]
Links:
References:
[[@reactReactComponentReact]]
[[@nachao2022NianQianDuanReactDe100DaoMianShiTiDeDi15TiCuoWuBianJieJueJin]]