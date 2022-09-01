## 描述

[[@mdnCombinatorsLearnWeb]]
> descendant selector
> The **descendant combinator** — typically represented by a single space (" ") character — combines two selectors such that elements matched by the second selector are selected if they have an ancestor (parent, parent's parent, parent's parent's parent, etc.) element matching the first selector. Selectors that utilize a descendant combinator are called _descendant selectors_.


重點：
- **descendant combinator** 會是利用DOM節點之間的parent-child關係來選擇對應節點
- 形式為：主要由多個基本selector和空格所構成，每個selector之間會用空格相連接
	- 例子1，會選擇符合selector1 的DOM 節點所擁有的子節點，且子節點是符合selector2
	```
	selector1 selector2 {
	
	}
	```
	- 例子2，會選擇符合selector1 和 selector 2 的DOM 節點所擁有的子節點，而子節點是符合selector3
	```
	selector1 selector2 selector3 {
	
	}
	```
## 複習

#🧠 descendant combinator 是什麼？ ->->-> `descendant combinator 會是利用DOM節點之間的parent-child關係來選擇對應節點`
<!--SR:!2022-09-04,3,250-->

#🧠 descendant combinator 的主要形式是什麼？ ->->-> `主要由多個基本selector和空格所構成，每個selector之間會用空格相連接`
<!--SR:!2022-09-04,3,250-->

#🧠 selector1 selector2 { }這類的selector會選擇什麼？ ->->-> `會選擇符合selector1 的DOM 節點所擁有的子節點，且子節點是符合selector2`
<!--SR:!2022-09-04,3,250-->

#🧠 selector1 selector2 selector3 { } 這類的selector會選擇什麼？ ->->-> `會選擇符合selector1 和 selector 2 的DOM 節點所擁有的子節點，而子節點是符合selector3`
<!--SR:!2022-09-04,3,250-->

---
Status: #🌱  
Tags:
[[CSS]]
Links:
[[CSS Combinator 使用特殊符號或者特定形式來將多種selector結合成另一種selector]]
References:
[[@mdnCombinatorsLearnWeb]]