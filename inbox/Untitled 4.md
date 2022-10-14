## 描述

there are errors which you can't prevent or which are simply being used transport information that something went wrong from on part of the application to another part

consider an http request which is being sent.

if the server is temporarily not responding, the request can't complete and you will likely end up with an error being generated


```
1.  if (this.props.users.length === 0) {
2.     throw new Error('No users provided!');
3.  }
```



當特定元件發出錯誤時，會試著從目前函式下尋找可攔截錯誤資訊物件並處理的程式模組，若沒有就會往當初該執行環境下被呼叫的地方所在的函式A尋找可攔截錯誤資訊物件並處理的程式模組，在沒有就從函式A被呼叫的所在尋找可攔截錯誤資訊物件並處理的程式模組，直到找得到可攔截並處理為止，若沒有的話，React 會報錯

  

and i let his error bubble up the call stack. So I pass it through all these components, and if it's not handled anywhere, this will crash my application

  

可能的替代方案：

- 不拋出錯誤，但取而代之是以其他方式來處理

```
1.  try {
2.       someCodeWhichMightFail()
3.  } catch(err) {
4.    // handle error
5. }
```



nonetheless, if an error is generated inside of a component and we can't handle it in that component though

  

如果元件對應的JSX code本身出現錯誤的話，就不能夠直接以try...catch

  

error boundary：

- 本質上是一個標準的class-based component，但會夾雜著componentDidCatch 這生命週期方法（lifecycle method)
- 目前functional component並沒辦法支援componentDidCatch，故此要實現error boundary只能在class-based component


componentDidCatch 這生命週期方法可以添加任一一個class-based component，只要元件A添加了該方法，元件A就會是error boundary


> well, this lifecycle method will be triggered whenever one of the child components throws an error or generates an error

componentDidCatch 生命週期函式

- 語法：
  error 會是被攔截到的錯誤資訊物件，會由react負責轉遞過來
  設定hasError為true來表達有錯誤

```
1.  componentDidCatch(error) {
2.    // 根據error種類來訂製各個錯誤處理
3.    this.setState({ hasError: true});
4.  }
```


error boundary
1. 設定成wrapper component 來包含多個component，以此讓這些component發生錯誤時，可以先被error boundary攔截到
2. 註冊hasError這狀態來好讓後頭渲染內容根據狀態來變動，比如發生錯誤就印出代表錯誤訊息的頁面；沒發生錯誤就正常渲染
3. 在開發模式，會因為錯誤資訊來特意顯示，實際上，對應的error-boundary有呈現對應畫面；在production階段並不會呈現錯誤資訊

## 複習


---
Status: #🌱 
Tags:
[[React]]
Links:
References: