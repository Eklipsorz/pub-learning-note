## 描述

[[@mdnCombinatorsLearnWeb]]
> descendant selector
> The **descendant combinator** — typically represented by a single space (" ") character — combines two selectors such that elements matched by the second selector are selected if they have an ancestor (parent, parent's parent, parent's parent's parent, etc.) element matching the first selector. Selectors that utilize a descendant combinator are called _descendant selectors_.


重點：
- **descendant combinator** 會是利用DOM節點之間的parent-child關係來選擇選擇child dom節點或者後裔dom 節點
- 形式為：主要由多個基本selector和空格所構成，每個selector之間會用空格相連接
	- 例子1：挑選滿足selector2的DOM節點，且會是DOM節點A的後裔節點，該節點A會滿足selector1
	```
	selector1 selector2 {
	
	}
	```
	- 例子2：挑選滿足selector2的DOM節點，且會是DOM節點A的後裔節點，該節點A會滿足selector1和selector2
	```
	selector1 selector2 selector3 {
	
	}
	```

### 後裔節點為特定節點所擁有的子節點或者源自於特定節點的後裔節點

> Someone's descendants are the people in later generations who are related to them.

重點：
- 某事物A的後裔會是從某事物A衍生的事物
## 複習

#🧠 descendent 命名緣由為何？ ->->-> `某事物A的後裔會是從某事物A衍生的下一代事物`

#🧠 descendant combinator 是什麼？ ->->-> `descendant combinator 會是利用DOM節點之間的parent-child關係來選擇child dom節點或者子孫dom 節點`

#🧠 descendant combinator 所選擇的後裔節點會是指什麼？ ->->-> `特定節點的子節點，特定節點的孫子節點`

#🧠 descendant combinator 所選擇的後裔節點就一定是特定節點的子節點嗎 ->->-> `不一定，還有可能會是特定節點的子孫節點`

#🧠 descendant combinator 的主要形式是什麼？ ->->-> `主要由多個基本selector和空格所構成，每個selector之間會用空格相連接`

#🧠 舉例來說明何謂後裔節點？->->-> `節點A擁有節點B，而節點B擁有節點C，那麼節點B和節點C就是源自於節點A的後裔節點`

#🧠 selector1 selector2 { }這類的selector會選擇什麼？ ->->-> `挑選滿足selector2的DOM節點，且會是DOM節點A的後裔節點，該節點A會滿足selector1`


#🧠 selector1 selector2 selector3 { } 這類的selector會選擇什麼？ ->->-> `挑選滿足selector2的DOM節點，且會是DOM節點A的後裔節點，該節點A會滿足selector1和selector2`


---
Status: #🌱  
Tags:
[[CSS]]
Links:
[[CSS Combinator 使用特殊符號或者特定形式來將多種selector結合成另一種selector]]
References:
[[@mdnCombinatorsLearnWeb]]