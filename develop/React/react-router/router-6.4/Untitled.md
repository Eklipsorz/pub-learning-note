## 描述

###
當Route的對應元件發生錯誤時，可以使用以錯誤訊息來渲染：
- Route 元件的errorElement屬性來作為錯誤訊息出現時所要的渲染
- 能夠攔截到的錯誤種類會是Route執行對應loader時的錯誤、Route執行渲染對應元件時的錯誤
`<Route .... errorElement={JSX Element} />`


其errorElement的Route元件若擺在parent route元件的話，其後裔元件發生錯誤時，會以parent route元件的errorElement為主。


###

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