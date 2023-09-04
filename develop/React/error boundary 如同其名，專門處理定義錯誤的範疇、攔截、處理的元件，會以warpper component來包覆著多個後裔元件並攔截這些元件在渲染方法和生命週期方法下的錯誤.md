## 描述


### 發送錯誤資訊物件的主要來源

主要來源為：
- 元件上的事件處理 
- 元件上發送出的非同步任務
- 元件本身的生命週期方法



### 錯誤資訊物件的傳遞


假如說在上述來源上出現錯誤的話，那麼勢必會以拋出搭載錯誤資訊之物件的形式來讓系統內部的錯誤處理程式模組能夠攔截
```
1.  if (this.props.users.length === 0) {
2.     throw new Error('No users provided!');
3.  }
```


當目前函式發出錯誤時的攔截流程：
- 會試著從目前函式下尋找可攔截錯誤資訊物件並處理的程式模組
- 若沒有就會往當初該執行環境下被呼叫的地方所在的函式A尋找可攔截錯誤資訊物件並處理的程式模組
- 在沒有就從函式A被呼叫的所在尋找可攔截錯誤資訊物件並處理的程式模組，直到找得到可攔截並處理為止
- 若都沒有的話，React 核心程式碼會在後頭接收錯誤來進行處理，其處理方式會是暫時停止執行渲染。


#### 兩難問題：

陷入最後一個流程的話，會因為無法正常呈現網頁畫面，並使使用者的使用體驗降低，若拔除React預設給定的錯誤處理，會無法保證網頁是否會按照預期執行以及安全性

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

componentDidCatch 生命週期函式：
- 每個元件都能定義
- 最主要負責攔截後裔節點在執行渲染函式或者生命週期函式時所拋出的錯誤進行處理
- 語法：
	- - error 會是被攔截到的錯誤資訊物件，會由react負責轉遞過來
```
componentDidCatch(error) {
	....
}
```
- 通常處理方式會是：依據錯誤種類來產生不同的狀態和觸發渲染
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

#🧠 boundary 命名緣由是什麼？ ->->-> `boundary 是一條線，標記著特定事物的邊緣或者特定情況下的上/下限`
<!--SR:!2024-04-01,245,229-->

#🧠 React：在一個元件中，發送錯誤資訊物件的主要來源是什麼？ ->->-> `- 元件上的事件處理 -  元件上發送出的非同步任務 - 元件本身的生命週期方法`
<!--SR:!2024-08-30,409,250-->

#🧠 React：在一個元件中，若發生預期外的錯誤，系統會如何發送錯誤？->->-> `那麼勢必會以拋出搭載錯誤資訊之物件的形式來讓系統內部的錯誤處理程式模組能夠攔截`
<!--SR:!2023-09-26,211,249-->

#🧠  React：在一個元件中，若發生預期外的錯誤，那麼勢必會以拋出搭載錯誤資訊之物件的形式來讓系統內部的錯誤處理程式模組能夠攔截，那麼攔截流程會是->->-> `- 會試著從目前函式下尋找可攔截錯誤資訊物件並處理的程式模組 - 若沒有就會往當初該執行環境下被呼叫的地方所在的函式A尋找可攔截錯誤資訊物件並處理的程式模組 - 在沒有就從函式A被呼叫的所在尋找可攔截錯誤資訊物件並處理的程式模組，直到找得到可攔截並處理為止 - 若都沒有的話，React 核心程式碼會在後頭接收錯誤來進行處理，其處理方式會是暫時停止執行渲染。`
<!--SR:!2023-08-22,34,189-->

#🧠  React：在一個元件中，若發生預期外的錯誤，那麼勢必會以拋出搭載錯誤資訊之物件的形式來讓系統內部的錯誤處理程式模組能夠攔截，若都沒有錯誤處理模組來攔截的話，React處理方式是如何？由誰處理？ ->->-> `React 核心程式碼會在後頭接收錯誤來進行處理，其處理方式會是暫時停止執行渲染`
<!--SR:!2023-12-12,254,249-->

#🧠 React：在一個元件中，若發生預期外的錯誤，即使沒有錯誤處理來攔截，React為何還要堅持攔截而採取預設錯誤處理？->->-> `會無法保證網頁是否會按照預期執行以及安全性`
<!--SR:!2023-09-11,202,249-->

#🧠 React：在一個元件中，若發生預期外的錯誤，即使沒有錯誤處理來攔截，React 為了保證網頁會按照預期執行以及安全性而堅持攔截而採取預設錯誤處理，但這樣的預設錯誤處理會給使用者帶來什麼潛在問題？ ->->-> `會因為無法正常呈現網頁畫面，並使使用者的使用體驗降低`
<!--SR:!2023-08-21,193,250-->


#🧠 React：在一個元件中，若錯誤資訊物件的來源是元件上的事件處理 和 元件上發送出的非同步任務，請問要用何種方式來攔截比較好？->->-> `使用JS語言體系的try...catch來解決`
<!--SR:!2023-09-08,203,249-->

#🧠 React：在一個元件中，若錯誤資訊物件的來源是元件上的事件處理 和 元件上發送出的非同步任務，為何不能採用error-boundary技術？->->-> `因為error-boundary技術只能攔截元件的渲染函式和生命週期方法所拋出的錯誤，這些來源都會在渲染之後就衍生，所以就無法正常攔截到`
<!--SR:!2024-09-30,434,250-->


#🧠 React：error boundary是什麼？ （請說到為何包覆)->->-> `如同其名，專門處理定義錯誤的範疇、攔截、處理的元件，會以empty warpper component來包覆著多個元件，這些後裔元件只要在渲染方法或者所有生命週期函式執行時發生錯誤，即可被error-boundary 元件給攔截到`
<!--SR:!2024-01-21,281,249-->

#🧠 React：error boundary是如同其名，專門處理定義錯誤的範疇、攔截、處理的元件，會以empty warpper component來包覆著多個元件，請問被包覆的後裔元件會有什麼好處？->->-> `這些後裔元件只要在渲染方法或者所有生命週期函式執行時發生錯誤，即可被error-boundary 元件給攔截到`
<!--SR:!2024-03-03,235,230-->

#🧠 React：error boundary 功能是什麼？ ->->-> `攔截後裔元件所發送的錯誤資訊並進行處理，以避免後頭沒人處理錯誤資訊而讓React核心程式碼接收到並停止渲染。`
<!--SR:!2023-11-01,219,230-->

#🧠 React：error boundary 功能是攔截後裔元件所發送的錯誤資訊並進行處理，為何需要攔截處理？ ->->-> `以避免後頭沒人處理錯誤資訊而讓React核心程式碼接收到並停止渲染。`
<!--SR:!2023-11-09,235,249-->

#🧠 React：通常error boundary會是用什麼寫法來開發 ？為什麼？->->-> `class-based component，目前functional component並沒有componentDidCatch的替代方案，故此要實現error boundary只能在class-based component`
<!--SR:!2024-09-08,418,250-->

#🧠 React：error boundary 元件 是如同其名，專門處理定義錯誤的範疇、攔截、處理的元件，該元件如何被建立出來？ ->->-> `- 必須是class-based component - 定義componentDidCatch 這生命週期方法（lifecycle method) 或者 static getDerivedStateFromError`
<!--SR:!2023-11-14,118,209-->


#🧠 React：error boundary 元件的局限性是什麼？->->-> `它無法處理：- 元件上的事件處理所產生的錯誤- 元件上的非同步任務所產生的錯誤 - error-boundary 元件本身並不能夠被自己攔截到，只能被上層的error-boundary元件攔截到`
<!--SR:!2023-08-24,181,230-->

#🧠  React：componentDidCatch 生命週期函式的用途是什麼？ ->->-> `最主要負責攔截後裔節點在執行渲染函式或者生命週期函式時所拋出的錯誤進行處理`
<!--SR:!2023-09-10,202,249-->

#🧠 React：componentDidCatch 生命週期函式的語法 ->->-> `componentDidCatch(error) {}`
<!--SR:!2023-12-17,104,230-->


#🧠 React：componentDidCatch 生命週期函式的語法為componentDidCatch(error) \{\}，其中的error是從何而來的？ ->->-> `後裔節點在執行渲染函式或者生命週期函式時所拋出的錯誤`
<!--SR:!2023-09-13,200,249-->


#🧠 React：componentDidCatch 生命週期函式的通常開發方式是？->->-> `依據錯誤種類來產生不同的狀態和觸發渲染`
<!--SR:!2023-12-01,96,230-->

#🧠 React： componentDidCatch  觸發時間點 ->->-> `只要其後裔元件的渲染方法和任一生命週期方法拋出錯誤，就會執行error-boundary下的componentDidCatch`
<!--SR:!2024-01-05,271,249-->

#🧠 React： getDerivedStateFromError 觸發時間點 ->->-> `只要其後裔元件的渲染方法和任一生命週期方法拋出錯誤，就會執行error-boundary下的componentDidCatch`
<!--SR:!2024-01-15,276,249-->

#🧠 React：error-boundary 常見實作方式，請以Users元件作為錯誤物件的來源來說明 ->->-> `1. 先在建構式上定義hasError狀態，並設定初始值為false，表示一開始沒錯誤 2. 接著設定componentDidCatch 內增加setState，來讓hasError有機會轉換成true 3. 最後在render上設定能夠根據this.state.hasError是否為true來顯示錯誤訊息 4. 在UsersFinder中放置ErrorBoundary來包含想要攔截錯誤的後裔元件，在這裡會是Users元件`
<!--SR:!2024-05-16,303,229-->

#🧠 React：Error-boundary 元件 可以處理自己元件下的生命週期函式和渲染函式所拋出來的錯誤嗎？->->-> `並不能`
<!--SR:!2023-12-11,217,229-->

#🧠 React：Error-boundary 元件 不可以處理自己元件下的生命週期函式和渲染函式所拋出來的錯誤，那怎麼樣才能處理Error-boundary 元件下的生命週期函式和渲染函式所拋出來的錯誤？->->-> `讓包含Error-boundary元件的Error-boundary元件來處理`
<!--SR:!2023-10-16,218,249-->

#🧠 React：error boundary 元件功能避免了什麼？ ->->-> `避免後頭沒人處理錯誤資訊而讓React核心程式碼接收到並停止渲染。`
<!--SR:!2024-01-08,269,248-->


#🧠 React：預設錯誤處理若沒攔截到錯誤並處理的話，會有什麼事情發生？ ->->-> `錯誤很有可能危害到系統的穩定和安全`
<!--SR:!2023-10-04,209,248-->


#🧠 componentDidUpdate 參數 vs componentDidCatch參數之間差別是什麼？ ->->-> `前者是(prevProps, prevState)；後者是(error)`
<!--SR:!2024-05-02,283,228-->

---
Status: #🌱 
Tags:
[[React]]
Links:
References:
[[@reactReactComponentReact]]
[[@nachao2022NianQianDuanReactDe100DaoMianShiTiDeDi15TiCuoWuBianJieJueJin]]