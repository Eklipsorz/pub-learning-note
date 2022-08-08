
> react is javascript library for building user interfaces
>  - it simplifies building those user interfaces
>

react ：
1. 本質上是一個JavaScript 函式庫，
2. react 程式碼具體為 JavaScript 程式碼
3. 主要用途為透過它來簡化使用者介面的建構流程



> react is all about components
> - all user interfaces in the end are made up of components



> what exactly is a component?
> reusable building blocks in user inteferaces
> components are in the end just a combination of HTML code 、 CSS code、JS code
> 	- HTML is DOM node
> 	- CSS is for styling DOM node
> 	- JS is for business logic and some logic


user interface
- 由多個元件(component)所組成
- 同頁會有多個user interfaces 



component 
- 由多個DOM節點和事件綁定來組成的基本元件
- 其元件會是UI介面上的主要基本建構單位
> individual building blocks
- 可重複使用在不同UI介面上
- 提出目的為：
	- 以模組形式來管理多個DOM節點構成的元件，讓元件可重複被使用、開發者更專注用途來開發元件

> you build these individual components and then you tell React how to compose them together into a final user interface
> And React embraces this concept of components becase
>   - Reusability： that reusability aspect (Don't repeat yourself )
>   - Separation of  Concerns： it allows us to separate our concerns (Don't do too many things in one and the same place (function))



component-driven user interfaces ?

> why it's all about components ? and what exactly a component is ? 


> React allows you to create re-usable and reactive components consisting of HTML and JavaScript (and CSS )

> what reactive means? 


> declarative approach 
> (x) imperative programming 
> you will always define the desired end state -> define the desired target state and let React figure out the actual JS DOM instructions


declarative rendering

> - Declarative rendering：開發者告訴電腦程式要渲染什麼樣的畫面，然後由電腦自己去生成對應的指令去實現畫面渲染：
	- 具體會是以特定語言架構來給予開發者定義怎麼樣的畫面，比如以語法來放置特定資料來告知系統以這些資料為目標來生成指令渲染
	- 內部則是解析目標並生成對應指令，其指令會是生成對應DOM節點、渲染指定樣式

在這裡目標畫面在react 稱作為desired end state 以及 特定情況下的 end state


> a bunch of configuration files 
> - that react app for production use

  

> node.js -> to execute **create react app tool**

 





1. index.js is the first file to execute

React 函式庫包含了react 和 react-dom 

react 則是 react 核心程式碼
react-dom 是用來指示react如何對dom操作和對瀏覽器操作





ReactDOM.createRoot => create the main entry point
the main hook of the overall user interface you are about to build with React
That's the idea behind createRoot


createRoot()
```
createRoot(container[, options]);
```
Create a React root for the supplied `container` and return the root. The root can be used to render a React element into the DOM with `render`:
```
const root = createRoot(container);
root.render(element);
```

- container ：會是指dom節點
- createRooot：主要指定哪個dom節點或者容器會是react層級的root節點，並回傳root
- 每個react層級的root節點可以呼叫render來將react element 指定放入在對應DOM節點 或者告訴系統 root節點對應的dom節點要如何被渲染




public 下的 index.html是最主要載入bundle.js的html，由index.html來搭配互動來讓bundle.js產生對應的畫面