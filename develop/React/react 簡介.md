
> react is javascript library for building user interfaces
>  - it simplifies building those user interfaces
>

react 本質上是一個JavaScript 函式庫，主要用途為透過它來簡化使用者介面的建構流程


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

 
