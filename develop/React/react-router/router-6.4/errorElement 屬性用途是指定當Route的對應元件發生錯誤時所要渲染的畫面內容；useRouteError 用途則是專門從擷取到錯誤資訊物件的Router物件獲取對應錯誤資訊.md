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
2. 用途： 專門從擷取到錯誤資訊物件的Router物件獲取對應錯誤資訊
3. 舉例：
```
1.  throw new Error('....')
```




## 複習


---
Status: #🌱 
Tags:
[[React]]
Links:
References:
[[@ErrorElementV6]]
[[@UseRouteErrorV6]]