## 描述


> The Route component is perhaps the most important component in React Router to understand and learn to use well. Its most basic responsibility is to render some UI when its path matches the current URL.


重點：
- Router 元件的routing 功能主要是由Route 元件來決定
- Router和Route的隸屬關係是如何決定的：Route本身會以最近的parent Router作為定義該Router的Routing功能
- 基於前者，會有以下兩種方式
	- 以清單形式來擺放各個Route：每一個Router 元件都會以parent 元件形式來包含Route 元件
	- 於Router所包含的任意後裔元件內定義Route：只要是在Router的任意後裔元件內定義Route元件
	- 前兩者為何可以實現：兩者都會Route是以最近的parent Router作為定義該Router的Routing功能
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
// 方式2：於Router所包含的任意後裔元件內定義Route
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
<!--SR:!2022-12-15,28,250-->

#🧠 react-router-dom：請問Router和Route的隸屬關係是如何決定的？ ->->-> `Route本身會以最近的parent Router作為定義該Router的Routing功能`
<!--SR:!2023-02-18,68,250-->

#🧠 react-router-dom：請問Router 和 Route 擺放方式有哪些？ ->->-> `方式1：以清單形式來擺放各個Route、方式2：擺放Router所包含的任意後裔元件內定義Route`
<!--SR:!2022-12-14,27,250-->

#🧠 react-router-dom：請問Router 和 Route 擺放方式有哪些？方式1：以清單形式來擺放各個Route，如何做？->->-> ``
<!--SR:!2023-02-19,69,250-->


#🧠 react-router-dom：請問Router 和 Route 擺放方式有哪些？方式2：於Router所包含的任意後裔元件內定義Route，如何做？ ->->-> ``
<!--SR:!2022-12-15,28,250-->

#🧠 react-router-dom：請問Router 和 Route 擺放方式有哪些？方式1：以清單形式來擺放各個Route、方式2：於Router所包含的任意後裔元件內定義Route，這兩者為何可以實現Router和Route的隸屬關係是如何決定的？->->-> `兩者都會Route是以最近的parent Router作為定義該Router的Routing功能`
<!--SR:!2022-12-14,27,250-->



---
Status: #🌱 
Tags:
[[React]]
Links:
[[React-router-dom：BrowserRouter 是主要提供client-side routing服務的component。 Route 是一個component，主要負責定義router 能夠合法使用的path以及對應path能夠渲染的component]]
References: