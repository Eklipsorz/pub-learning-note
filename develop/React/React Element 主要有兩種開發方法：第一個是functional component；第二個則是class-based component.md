## 描述



### React Element 的開發方法：
1. class-based component 
2. functional component

#### functional component 
> components are regular javascript functions which return renderable result (typically JSX)

重點：
- functional component 會是一般函式宣告，其回傳內容為JSX Element
- 語法會是
```
function Component1() {
	....
	return (
		JSX Element
	)
}
```
#### class-based component 

> class-based component：
> components can also be defined as JS classes where a render() method defines the to-be-rendered output


重點：
- class-based component 是以JS class語法建立而成的元件類別，最主要會有render方法並且繼承react.Component 這個基本類別所擁有的方法和屬性
- 其類別下的constructor 本身藉由default constructor可以不必設定
- 其render 方法 具體定義該元件的渲染內容或者對應Virtual DOM結構，語法為：
```
class Component1 extends React.Component {
	render() {
		....
	}
}
```
- 當這類型元件以標籤來使用，會以Component1 這類別來建構對應實例，並呼叫該實例的render方法
```
<Component1 />
```


#### 歷史

> class-based component
> traditionally (React  < 16.8), you had to use class-based components to manage "state"

React 16.8 之前都使用class-based component 來建立元件
  
> 16.8 => react hooks & functional components
> hooks (useState and useEffect and so on.) =>

React 16.8 之後就改採用hooks 和 functional components 概念

> - these are functions for functional components, which bring features to functional components, which previously were reserved for class-based components




#### hooks 對於 class-based component來說
hooks 是：
- 本身是專屬於functional component開發方式
- functional component 的hook 和 class-based component 都是獨立功能，只是使用相同React核心程式碼來實現各自目的的功能




#### functional component 能否和class-based component 混搭使用？
> you can mix and match, but that will mostly matter if you are working on an existing application

   functional component 和 class-based component 兩者寫法可以混搭在整個專案上

## 複習

#🧠 建立React Element 有哪兩種開發方法？ ->->-> `class-based component、functional component`
<!--SR:!2023-08-23,199,250-->

#🧠 React：class-based component 是什麼？ ->->-> `class-based component 是以JS class語法建立而成的元件類別，最主要會有render方法並且繼承react.Component 這個基本類別所擁有的方法和屬性`
<!--SR:!2024-03-06,232,210-->

#🧠 React：functional component  是什麼？ ->->-> `會是一般函式宣告，其回傳內容為JSX Element`
<!--SR:!2024-11-03,461,250-->

#🧠 React：functional component  的語法是什麼？ ->->-> `function Component1() { ... return (JSX Element ) }`
<!--SR:!2024-07-22,370,230-->

#🧠 React：class-based component 搭配render 的基本語法是什麼？ ->->-> `class Component1 extends React.Component { render() { ... } }`
<!--SR:!2023-12-03,98,230-->


#🧠 class Component1 extends React.Component \{ render() \{ ... \} \}  中沒有Constructor，請問能夠正常執行嗎？為什麼->->-> `能夠正常執行，系統會根據目前類別是否繼承其他類別而給予預設的constructor來方便建立對應類別的實例`
<!--SR:!2023-09-02,205,250-->

#🧠 class Component1 extends React.Component \{ render() \{ ... \} \} 中的render 是做什麼？ ->->-> `具體定義該元件的渲染內容或者對應Virtual DOM結構`
<!--SR:!2024-09-21,431,250-->

#🧠 當元件類別Component1以標籤來使用，如\<Component1 \/\> React會如何處理該元件 ->->-> `會以Component1 這類別來建構對應實例，並呼叫該實例的render方法`
<!--SR:!2023-08-05,187,250-->

#🧠 實際上React Element會在什麼時候被建立成實例並被呼叫render ->->-> `當這類型元件以標籤來使用`
<!--SR:!2023-08-31,203,250-->


#🧠 React：hooks 對於 functional component 和 class-based component 來說，誰能夠使用，具體為什麼 ->->-> `hook 是專屬於functional component的寫法。functional component 的hook 和 class-based component 都是獨立功能，只是使用相同React核心程式碼來實現各自目的的功能`
<!--SR:!2024-05-17,330,249-->


#🧠 React：class-based component 和 functional component這兩種元件開發方式誰最先 ->->-> `class-based component`
<!--SR:!2023-08-14,194,250-->

#🧠  React：class-based component 和 functional component這兩種元件開發方式誰最為流行  ->->-> `functional component`
<!--SR:!2023-08-27,199,250-->


#🧠 React： class-based component 能夠使用hook嗎->->-> `class-based component 無法使用react hooks`
<!--SR:!2023-08-11,192,250-->


#🧠  React：functional component 的hook 和class-based-component的語法之間的關係來說是什麼？為什麼 ->->-> `毫無相關，functional component 的hook 和 class-based component 都是獨立功能，只是使用相同React核心程式碼來實現各自目的的功能`
<!--SR:!2024-02-05,270,249-->
<!--SR:!2022-12-21,38,249-->

#🧠  React：functional component 的hook 和class-based-component的語法之間的關係來說是什麼？為什麼 ->->-> `毫無相關，functional component 的hook 和 class-based component 都是獨立功能，只是使用相同React核心程式碼來實現各自目的的功能`
<!--SR:!2024-02-05,270,249-->



#🧠 functional component 能否和class-based component 混搭使用？->->-> `functional component 和 class-based component 兩者寫法可以混搭在整個專案上`
<!--SR:!2025-01-22,514,250-->






---
Status: #🌱 
Tags:
[[React]]
Links:
[[JS class 建構式是每個類別的特殊方法，用來根據資訊來建立對應類別下物件並初始化，若沒設定的話，系統會預設設定指定的constructor給開發者來執行]]
[[import { Component } from 'react'; 的用途為方便讓特定元件繼承React的通用元件類別和react element所會需要方法和屬性]]
References:

