## 描述

### render 函式能夠回傳什麼形式的JSX Element

[[@reactReactComponentReact]]
```
render()
```

> The `render()` method is the only required method in a class component.

> When called, it should examine `this.props` and `this.state` and return one of the following types:
> 
> - React elements. Typically created via JSX. For example, <div /> and <MyComponent /> are React elements that instruct React to render a DOM node, or another user-defined component, respectively.
> 
>-  **Booleans or `null`**. Render nothing. (Mostly exists to support `return test && <Child />` pattern, where `test` is boolean.)
>
> - Arrays and fragments. Let you return multiple elements from render. See the documentation on fragments for more details. 



重點：
- render 函式能夠回傳的形式有：
	- 使用JSX語法的標籤元素
	```
	<div /> 
	<MyComponent /> 
	```
	- 使用Boolean expression && JSX Element 來表示 JSX 元素本身，其回傳內容會根據前者是否為true，若true，就以後者的JSX Element來呈現；若false，就忽略該Virtual DOM
	- 使用陣列包含多個React Element的形式
## 複習

#🧠 react：render函式還能夠回傳的JSX元素形式會有哪些？(搭配JS) ->->-> `單純JSX語法的元素、搭配JS Expression的JSX Element、使用陣列包含多個React Element的形式`
<!--SR:!2023-12-03,90,210-->

#🧠  react：render函式還能夠回傳的JSX元素形式會有哪些？ ->->-> `單純JSX語法的元素、搭配JS Expression的JSX Element、使用陣列包含多個React Element的形式`
<!--SR:!2023-12-21,171,190-->

---
Status: #🌱 #📓 
Tags:
[[React]]
Links:
[[渲染部分{expression}中的expression是指陣列的話，React 會直接將陣列上的每個元素當成react element 來並排當作渲染內容]]
[[React 解析boolean expression && JSX element  時，若前者為true，就以後者的JSX element為主，否則就忽略該Virtual DOM]]
References:
[[@reactReactComponentReact]]