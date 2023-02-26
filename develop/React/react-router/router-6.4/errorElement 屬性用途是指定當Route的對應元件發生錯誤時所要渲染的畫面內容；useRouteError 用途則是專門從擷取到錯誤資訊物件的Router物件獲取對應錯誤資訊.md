## 描述



### errorElement 屬性作用
[[@ErrorElementV6]]
> When exceptions are thrown in loaders, actions, or component rendering, instead of the normal render path for your Routes (\<Route element\>), the error path will be rendered (\<Route errorElement\>) and the error made available with useRouteError.


errorElement 重點：
- 用途為指定當Route的對應元件發生錯誤時所要渲染的畫面內容
	- 能夠攔截到的錯誤種類：Route執行對應loader時的錯誤、Route執行渲染對應元件時的錯誤、Route執行對應action時的錯誤
- errorElement會存在每個Route元件上的屬性，其語法為：
	- errorElement為 JSX Element語法
`<Route .... errorElement={JSX Element} />`
- 其errorElement的Route元件若擺在parent route元件的話，其後裔Route 元件發生錯誤時，會以parent route元件的errorElement為主。


### useRouteError 用途
[[@UseRouteErrorV6]]
> Inside of an errorElement, this hook returns anything thrown during an action, loader, or rendering. 

useRouteError：
1. 形式：本身為hook
2. 用途： 專門從Route執行對應loader時的錯誤、Route執行渲染對應元件時的錯誤、Route執行對應action時的錯誤來獲取對應的錯誤資訊物件
3. 舉例：
```
1.  throw new Error('....')
```
4. 語法：回傳錯誤資訊物件
```
const error = useRouteError()
```

## 複習

#🧠 react-router-dom v6.4 ：errorElement 在Route元件上是做什麼？ ->->-> `指定當Route的對應元件發生錯誤時所要渲染的畫面內容`
<!--SR:!2023-03-19,61,250-->

#🧠  react-router-dom v6.4 ：errorElement 在Route元件上是指定當Route的對應元件發生錯誤時所要渲染的畫面內容，那麼它能夠攔截到哪種錯誤？？->->-> `Route執行對應loader時的錯誤、Route執行渲染對應元件時的錯誤、Route執行對應action時的錯誤`
<!--SR:!2023-03-18,61,250-->

#🧠  react-router-dom v6.4 ：errorElement 會是哪一種元件的屬性？ ->->-> `Route`
<!--SR:!2023-04-05,72,250-->

#🧠  react-router-dom v6.4 ：errorElement 會是Route元件的屬性，請問其語法會是什麼？ ->->-> `<Route .... errorElement={JSX Element} />`
<!--SR:!2023-03-15,59,250-->

#🧠  react-router-dom v6.4 ：errorElement 在Route元件上是指定當Route的對應元件發生錯誤時所要渲染的畫面內容，其中它能夠攔截渲染對應元件時的錯誤，請問元件的範疇會是什麼？ ->->-> `元件本身、元件所包含的後裔元件`
<!--SR:!2023-06-24,120,250-->

#🧠 react-router-dom v6.4 ：useRouteError 用途為何？->->-> ` 專門從Route執行對應loader時的錯誤、Route執行渲染對應元件時的錯誤、Route執行對應action時的錯誤來獲取對應的錯誤資訊物件`
<!--SR:!2023-04-04,71,250-->

#🧠  react-router-dom v6.4 ：useRouteError 語法為何？ ->->-> `const error = useRouteError()`
<!--SR:!2023-02-26,47,250-->

#🧠 react-router-dom v6.4 ：useRouteError 語法會回傳什麼？ ->->-> `回傳錯誤資訊物件`
<!--SR:!2023-03-23,42,230-->

#🧠 react-router-dom v6.4 ：useRouteError 是專門回傳錯誤資訊物件，請問從哪裡獲取到的錯誤資訊物件？ ->->-> `從Route執行對應loader時的錯誤、Route執行渲染對應元件時的錯誤、Route執行對應action時的錯誤資訊來獲取和轉換`
<!--SR:!2023-06-07,108,250-->

#🧠 react-router-dom v6.4 ：useRouteError和 Route元件上的errorElement 屬性都取自於哪些錯誤資訊？->->-> `從Route執行對應loader時的錯誤、Route執行渲染對應元件時的錯誤、Route執行對應action時的錯誤資訊來獲取和轉換`
<!--SR:!2023-03-29,43,249-->

---
Status: #🌱 
Tags:
[[React]]
Links:
References:
[[@ErrorElementV6]]
[[@UseRouteErrorV6]]