## 描述

[[@RenderReact]]
> ### `render(reactNode, domNode, callback?)` [](https://beta.reactjs.org/reference/react-dom/render#render "Link for this heading")

> Call `render` to display a React component inside a browser DOM element.

```
import { render } from 'react-dom';const domNode = document.getElementById('root');render(<App />, domNode);
```

> React will display `<App />` in the `domNode`, and take over managing the DOM inside it.

> An app fully built with React will usually only have one `render` call with its root component. A page that uses “sprinkles” of React for parts of the page may have as many `render` calls as needed.

重點：
- render 是React 函式庫中的Virtual DOM物件所擁有的方法
	- 主要為定義對應個Virtual DOM 物件要有的渲染畫面為何
	- 每個Virtual DOM 物件都會對應到實際存在的Real DOM物件之內部

###  root 層級的Virtual DOM範例

```
const root = ReactDOM.createRoot(document.getElementById('root'));
root.render(
	<BrowserRouter>
		<App />
	</BrowserRouter>,
);
```

## 複習

#🧠 React：render 對於Virtual DOM物件來說是什麼？ 用途為何->->-> `render 是React 函式庫中的Virtual DOM物件所擁有的方法，主要為定義對應個Virtual DOM 物件要有的渲染畫面為何`
<!--SR:!2023-03-27,8,250-->

#🧠 React： 這是一段調用React函式庫的代碼，請問這做了什麼？`const root = ReactDOM.createRoot(document.getElementById('root')); root.render(...)`  ->->-> ``
<!--SR:!2023-03-27,8,250-->

#🧠 render 是React 函式庫中的Virtual DOM物件所擁有的方法，主要為定義對應個Virtual DOM 物件要有的渲染畫面為何，這樣指定渲染畫面又是為何？ ->->-> `每個Virtual DOM 物件都會對應到實際存在的Real DOM物件之內部`
<!--SR:!2023-04-14,19,250-->

#🧠 React 函式庫中的Virtual DOM物件 主要對應著Real DOM的什麼？ ->->-> `其本身和其內部`
<!--SR:!2023-03-29,10,250-->


---
Status: #🌱 
Tags:
[[React]] - [[JavaScript]]
Links:
References:
[[@RenderReact]]