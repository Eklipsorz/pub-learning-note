## 描述

[[@reactpatternsJSXSpreadAttributes]]
> ## What is JSX Spread Attributes?[#](https://reactpatterns.js.org/docs/jsx-spread-attributes#what-is-jsx-spread-attributes "Direct link to heading")
>
> Spread attributes is a JSX feature, it's a syntax for passing all of an object's properties as JSX attributes.

> ## For examples[#](https://reactpatterns.js.org/docs/jsx-spread-attributes#for-examples "Direct link to heading")

>If you know all the properties that you want to place on a component ahead of time, it is easy to use JSX.

```
const component = <Component foo={x} bar={y} />
```

> If you don't know which properties you want to set, you might be tempted to add them onto the object later.

```
var component = <Component />;

component.props.foo = x // bad
component.props.bar = y // also bad
```

> Now you can use a new feature of JSX called spread attributes.

```
let props = {}
props.foo = x
props.bar = y
const component = <Component {...props} />
```


[[@reactJSXDepthReact]]
> ### Spread Attributes
>
> If you already have `props` as an object, and you want to pass it in JSX, you can use `...` as a “spread” syntax to pass the whole props object. These two components are equivalent:

```
function App1() {
  return <Greeting firstName="Ben" lastName="Hector" />;
}

function App2() {
  const props = {firstName: 'Ben', lastName: 'Hector'};
  return <Greeting {...props} />;}
```

重點：
- React spread attributes 
	- 具體是利用JS原生的spread operator對於物件操作的效果為基礎來 針對 component所擁有的屬性(attribute)進行擴張
	- 用法：
		- property 會是物件
		- ...property 會是JS原生的spread operator正對著物件的屬性進行擴張

	```
	const property = { propert1: value1, property2: value2 }
	<Component {...property} />
	// 等同於
	// <Component property1=value1 property2=value2 />
	```
	- ...property 會是JS原生的spread operator正對著物件的屬性進行擴張
	```
	property1:value1, property2:value2, ....
	```


## 複習

#🧠 React spread attributes  是什麼技術？ ->->-> `具體是利用JS原生的spread operator對於物件操作的效果為基礎來 針對 component所擁有的屬性(attribute)進行擴張`
<!--SR:!2023-07-07,174,250-->

#🧠 原生JS：...object 執行起來會有什麼效果 ->->-> `property1:value1, property2:value2, ....`
<!--SR:!2023-09-11,185,230-->


#🧠 React spread attributes  用法為何？ ->->-> `const property = { propert1: value1, property2: value2 } <Component {...property} />`
<!--SR:!2023-07-19,181,250-->

#🧠 React spread attributes ： const property = \{ propert1: value1, property2: value2 \} \<Component {...property} \/\> 相對於什麼樣的component ->->-> `<Component property1=value1 property2=value2 />`
<!--SR:!2023-07-18,180,250-->


#🧠 React spread attributes  用法概念為何？ ->->-> `以一個物件的屬性來對元件的屬性(attribute)進行spread 操作`
<!--SR:!2023-08-03,193,250-->



---
Status: #🌱 
Tags:
[[React]]
Links:
References:
[[@reactpatternsJSXSpreadAttributes]]
[[@reactJSXDepthReact]]