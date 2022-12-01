## 描述

> A \<Route\> is only ever to be used as the child of \<Routes\> element, never rendered directly. Please wrap your \<Route\> in a \<Routes\>.

[[@react-routerReactRouterDeclarativea]]
> Upgrade all \<Switch\> elements to \<Routes\>
> React Router v6 introduces a Routes component that is kind of like Switch, but a lot more powerful.


Route 元件只能被包裹在Routes元件
Routes元件會替代Switch



Switch 元件 在挑選路徑時會以誰先滿足目前URL來挑選，流程為
- 遍歷每個Route元件並比對目前它的path和URL是否滿足，
	- 若滿足就挑它並停止遍歷
	- 若不滿足就繼續遍歷


Routes 元件 在挑選路徑時會以具體程度為優先來挑選，流程為：
- 遍歷每個Route元件並評估目前Route元件所對應的path 對於目前URL的具體程度為何
- 遍歷完就以具體程度最高的Route元件為主


specifically, the internal logic for evaluating these paths and then picking a route to load changed

3. 每個Route元件都會是exact matching來比對path，若要使用fuzzy matching，可以使用*這字原來表示，比如若要表示welcome開頭的頁面都是渲染element1元件，就設定如下

```
1.  <Route path='/welcome/* element={element1} />
```


in v6 ,

1. switch 元件由Routes來替代

> switch doesn't exist anymore

2. Route元件用法改變，若要指定對應Route元件要渲染的元件，就要
```
1.  <Route path='/welcome element={element1} />
```



## 複習


---
Status: #🌱 
Tags:
[[React]]
Links:
References:
[[@react-routerReactRouterDeclarativea]]