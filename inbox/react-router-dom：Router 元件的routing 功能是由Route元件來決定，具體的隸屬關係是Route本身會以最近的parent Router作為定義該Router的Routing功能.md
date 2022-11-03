## 描述


> The Route component is perhaps the most important component in React Router to understand and learn to use well. Its most basic responsibility is to render some UI when its path matches the current URL.


重點：
- Router 元件的routing 功能主要是由Route 元件來決定
- Router和Route的隸屬關係是如何決定的：Route本身會以最近的parent Router作為定義該Router的Routing功能
- 基於前者，所以具體來說每一個Router 元件都會以parent 元件形式來包含Route 元件 或者 只要是在Router的任意後裔節點下定義Route元件，兩者都會是以最近的parent Router作為定義該Router的Routing功能
```
// 方式1：以清單形式來擺放各個Route
<Router>
	<Route path=path1>
		<Component1 />
	</Route>
	
	<Route path=path2>
		<Component2 />
	</Route>
	.
	.
<Router />
```

```
// 方式2：擺放
<Router>
	<Route path=path1>
		<Component1 />
	</Route>
	
	<Route path=path2>
		<Component2 />
	</Route>
	.
	.
<Router />
```

```
function Component1() {

	return (
		<Route />
	)
}
```
## 複習

#🧠 react-router-dom：Router 元件的routing 功能主要由誰來決定？ ->->-> `Router 元件的routing 功能主要是由Route 元件來決定`

#🧠 react-router-dom：請問Router和Route的隸屬關係是如何決定的？ ->->-> `Route本身會以最近的parent Router作為定義該Router的Routing功能`

#🧠 react-router-dom：請問Router 和 Route 擺放方式有哪些？ ->->-> ``

#🧠 Question :: ->->-> ``


---
Status: #🌱 
Tags:
[[React]]
Links:
References: