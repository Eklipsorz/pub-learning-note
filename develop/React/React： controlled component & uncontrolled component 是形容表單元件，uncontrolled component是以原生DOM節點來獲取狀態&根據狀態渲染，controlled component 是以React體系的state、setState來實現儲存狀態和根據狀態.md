


## 描述

[[@reactFormsReact]]
> In HTML, form elements such as \<input\>, \<textarea\>, and \<select\> typically maintain their own state and update it based on user input. In React, mutable state is typically kept in the state property of components, and only updated with setState().

> We can combine the two by making the React state be the “single source of truth”. Then the React component that renders a form also controls what happens in that form on subsequent user input. An input form element whose value is controlled by React in this way is called a “controlled component”.


```
class NameForm extends React.Component {
  constructor(props) {
    super(props);
    this.state = {value: ''};
    this.handleChange = this.handleChange.bind(this);
    this.handleSubmit = this.handleSubmit.bind(this);
  }

  handleChange(event) {    this.setState({value: event.target.value});  }
  handleSubmit(event) {
    alert('A name was submitted: ' + this.state.value);
    event.preventDefault();
  }

  render() {
    return (
      <form onSubmit={this.handleSubmit}>        
	      <label>
          Name:
          <input type="text" value={this.state.value} onChange={this.handleChange} />        </label>
        <input type="submit" value="Submit" />
      </form>
    );
  }
}
```

[[@reactUncontrolledComponentsReact]]
> uncontrolled components, where form data is handled by the DOM itself.

```
class NameForm extends React.Component {
  constructor(props) {
    super(props);
    this.handleSubmit = this.handleSubmit.bind(this);
    this.input = React.createRef();  
  }

  handleSubmit(event) {
    alert('A name was submitted: ' + this.input.current.value);    event.preventDefault();
  }

  render() {
    return (
      <form onSubmit={this.handleSubmit}>
        <label>
          Name:
          <input type="text" ref={this.input} />        </label>
        <input type="submit" value="Submit" />
      </form>
    );
  }
}
```

重點：
- 無論使用哪個框架來開發元件，都會在意著**其元件的狀態如何儲存&獲取**和**其元件如何根據狀態來重新被渲染**，而狀態即為特定時間下的特定元件經由互動而得到互動資訊
- 在React中，controlled component & uncontrolled component 是用來描述表單元素
- 狀態儲存和根據狀態更新畫面，主要分為：
	- 原生DOM元素原有的狀態儲存和根據狀態更新畫面
	- React 體系下的狀態儲存和根據狀態更新畫面
- 若React 上的表單元件是基於原生DOM元素原有的方法來儲存自己表單資料＆渲染表單，那麼React 就無法以狀態來控管該元件，因而使該表單元件為uncontrolled component
- 若React 上的表單元件是採用React自己體系的狀態來儲存表單資料 & 渲染表單，那麼React 本身就能以狀態來控管這元件，因而使該表單元件為controlled component

### 為什麼原生DOM表單元素的原生狀態儲存和根據狀態而渲染畫面會影響到React ？

1. ~~因為React 在元件上的開發上可以用原生DOM元素的層級來開發，但問題是原生DOM元素本身就因為規範和瀏覽器實現而擁有自己的方式來儲存狀態和根據狀態渲染畫面，關於儲存狀態和根據狀態渲染畫面，React 本身也有自己的概念去實現和替代。~~
2. ~~這時會面臨到二選一的問題：第一個是使用React的體系去管理元件的狀態和根據狀態渲染畫面、第二個是使用原生DOM元素本身擁有的方式，但這很難從React去控管它的狀態、根據狀態來渲染~~


由於React在元件上的開發上可以用DOM 元素開發概念和他們原生就有實現來進行，而關於狀態儲存和根據狀態而渲染，本身上React和原生DOM都有實現，但DOM元件開發概念由於跟著被帶入至開發，以至於可以在React使用原生概念做，這時就會冒出兩選一的問題，使用React? 還是使用原生DOM原本方法

### uncontrolled component
 對於uncontrolled component，會有一些方法來獲取資訊和渲染：
 - 獲取狀態 & 儲存狀態：擷取對應實際DOM節點，並從節點中取得資訊來儲存
 - 渲染：
	 - 透過擷取對應實際DOM節點，並從DOM節點上直接修改屬性來觸發更新狀態、渲染
	 - 從React的開發角度觸發原生元件的預設渲染，讓其根據狀態去渲染自己元件

產生來源：
	- 使用ref技術而衍生的元件

### controlled component
 對於controlled component，會有一些方法來獲取資訊和渲染：
- 獲取狀態 & 儲存狀態：替元件註冊狀態、更新狀態用函式，並用他們來擷取每一次的互動結果進而替代原生DOM語法
- 渲染：使用對應狀態的更新狀態用函式，來以指定狀態來重新渲染一次

實際方式為：
- 方式1: 由parent 元件的狀態和更新狀態(兼渲染)用的函式來透過props和callback來控管controlled component，即元件上的儲存狀態和根據狀態而渲染全由parent元間來控管
```
// Expenses.js
function Expenses(props) {

	const { expenses } = props;
	const [year, setYear] = useState('2018');

	const filterChangeHandler = (year) => {
		setYear(year);
	};

  

	return (
		<div>
			<ExpensesFilter
			   selectedYear={year}
			   onChangeHandler={filterChangeHandler}
			 />
		</div>
	);
}
```


```
function ExpensesFilter(props) {

	const yearChangeHandler = (event) => {
		const year = event.target.value;
		props.onChangeHandler(year);
	};
	
	return (
		<div className='expenses-filter'>
			<select value={props.selectedYear} onChange={yearChangeHandler}>
			.
			.
			</select>
		</div>
	);
}
```

- 方式2: 元件本身會有狀態來決定元件自己的狀態儲存、根據狀態而渲染

```
class NameForm extends React.Component {
  constructor(props) {
    super(props);
    this.state = {value: ''};
    this.handleChange = this.handleChange.bind(this);
    this.handleSubmit = this.handleSubmit.bind(this);
  }

  handleChange(event) {    this.setState({value: event.target.value});  }
  handleSubmit(event) {
    alert('A name was submitted: ' + this.state.value);
    event.preventDefault();
  }

  render() {
    return (
      <form onSubmit={this.handleSubmit}>        
	      <label>
          Name:
          <input type="text" value={this.state.value} onChange={this.handleChange} />        </label>
        <input type="submit" value="Submit" />
      </form>
    );
  }
}
```

### 狀態儲存和根據狀態更新畫面


#### 原生表單DOM元素原有的狀態儲存和根據狀態更新&畫面
[[@ithomeDay27JiShiTianQi]]

> 之所以在表單元素上會區分「受 React 控制的資料」和「不受 React 控制的資料」，主要是因為在瀏覽器中，像是 `<input />` 這類的表單元素本身就可以保有自己的資料狀態，這也就是爲什麼當我們在 `<input />` 中輸入文字後，可以直接透過 JavaScript 選到該 input 元素後，再取出該元素的值，因為使用者輸入的內容（資料）可以直接保存在 `<input />` 元素內。


重點：
- 具體是由瀏覽器預設處理來負責處理狀態儲存和根據狀態更新&畫面
- 原生表單DOM元素：\<input\>, \<textarea\>, and \<select\> 
- 當表格的原生DOM元素與使用者發生互動時
	- 狀態儲存：瀏覽器預設下會直接將互動資料(狀態)以JS物件形式儲存起來
	```
	// 選取到該元件
	const component = document.getElementById('xxxx')
	// 直接從元件儲存的狀態取得過來
	const value = component.value
	```
	- 根據狀態渲染：瀏覽器會設定每個元件的預設事件處理來根據互動資訊(狀態)來更新&渲染元素的方法，

#### React 體系下的狀態儲存和根據狀態更新畫面
React 本身也有自己的體系來儲存每個元件的狀態和藉由更新狀態而觸發更新&渲染對應元件的方法，分別為：
```
this.state
setState
```



### 其他文獻

[[@ithomeDay27JiShiTianQi]]
> ## Controlled vs Uncontrolled Components

> 在 React 中表單元素的處理主要可以分成兩種 Controlled 和 Uncontrolled 這兩種，這裡**關於 Controlled 和 Uncontrolled 指的是「資料受不受到 React 所控制」，也就是「受 React 所控制的資料（Controlled）」或「不受 React 所控制的資料（Uncontrolled）」**。

> 之所以在表單元素上會區分「受 React 控制的資料」和「不受 React 控制的資料」，主要是因為在瀏覽器中，像是 `<input />` 這類的表單元素本身就可以保有自己的資料狀態，這也就是爲什麼當我們在 `<input />` 中輸入文字後，可以直接透過 JavaScript 選到該 input 元素後，再取出該元素的值，因為使用者輸入的內容（資料）可以直接保存在 `<input />` 元素內。


[[@chidumennamdiControlledVsUncontrolled]]
> Controlled components in React are those in which form data is handled by the component’s state.

> Uncontrolled components are those for which the form data is handled by the DOM itself. “Uncontrolled” refers to the fact that these components are not controlled by React state.


> changes through callbacks like onChange. A parent component "controls" it by handling the callback and managing its own state and passing the new values as props to the controlled component. You could also call this a "dumb component".

> A Uncontrolled Component is one that stores its own state internally, and you query the DOM using a ref to find its current value when you need it. This is a bit more like traditional HTML.


## 複習

#🧠 React：setState 是做什麼用？(提示有兩個)->->-> `更新狀態、根據狀態來觸發渲染`
<!--SR:!2023-07-19,194,250-->

#🧠 無論使用哪個框架來開發網頁元件，都會在意元件狀態的什麼？其狀態又會是什麼？ ->->-> `都會在意著**其元件的狀態如何儲存&獲取**和**其元件如何根據狀態來重新被渲染**，而狀態即為特定時間下的特定元件經由互動而得到互動資訊`
<!--SR:!2023-08-06,112,210-->

#🧠 在React中，controlled component & uncontrolled component 是用來描述著什麼元素？ ->->-> `前者是指狀態會被React體系的狀態管理給管理的元件、後者是指狀態不會被React體系的狀態管理給管理的元件`
<!--SR:!2024-06-02,264,229-->


#🧠 在實際的網頁開發中，表單元素上的狀態儲存和狀態更新畫面有哪兩種主要方式？ ->->-> `原生DOM元素原有的狀態儲存和根據狀態更新畫面、網頁框架(如React )體系下的狀態儲存和根據狀態更新畫面`
<!--SR:!2023-07-18,116,246-->
<!--SR:!2023-06-06,147,230-->

#🧠 在實際的網頁開發中，表單元素上的狀態儲存和狀態更新畫面有哪兩種主要方式？ ->->-> `原生DOM元素原有的狀態儲存和根據狀態更新畫面、網頁框架(如React )體系下的狀態儲存和根據狀態更新畫面`
<!--SR:!2023-07-18,116,246-->


#🧠 在React中，controlled component 是什麼？ ->->-> `若React 上的表單元件是採用React自己體系的狀態來儲存表單資料 & 渲染表單，那麼React 本身就能以狀態來控管這元件，因而使該表單元件為controlled component`
<!--SR:!2024-03-15,342,250-->

#🧠 在React中，uncontrolled component 是什麼？ ->->-> `若React 上的表單元件是基於原生DOM元素原有的方法來儲存自己表單資料＆渲染表單，那麼React 就無法以狀態來控管該元件，因而使該表單元件為uncontrolled component`
<!--SR:!2025-02-10,543,250-->

#🧠 原生DOM元素原有的狀態儲存和根據狀態更新&畫面下，原生DOM元素會是哪些？ ->->-> `\<input\>, \<textarea\>, and \<select\>`
<!--SR:!2024-10-10,468,250-->

#🧠 請描述原生DOM元素原有的狀態儲存和根據狀態更新&畫面下的手段是什麼？ ->->-> `狀態儲存：瀏覽器預設下會直接將互動資料(狀態)以JS物件形式儲存起來、根據狀態渲染：瀏覽器會設定每個元件的預設事件處理來根據互動資訊(狀態)來更新&渲染元素的方法`
<!--SR:!2024-04-05,353,250-->


#🧠 在React 開發上，原生DOM元素的狀態儲存和根據狀態而渲染畫面這兩種原生方法為何還能存在於React框架 ？->->-> `由於React在元件上的開發上可以用DOM 元素開發概念和他們原生就有實現來進行，而關於狀態儲存和根據狀態而渲染，本身上React和原生DOM都有實現，但DOM元件開發概念由於跟著被帶入至開發，以至於可以在React使用原生概念做，這時就會冒出兩選一的問題，使用React? 還是使用原生DOM原本方法?`
<!--SR:!2023-06-27,150,228-->



#🧠 React ：React 和 controlled component 的控管關係會是如何？ ->->-> `使用React的體系去管理元件的狀態和根據狀態渲染畫面`
<!--SR:!2025-01-18,522,250-->

#🧠 React ：React 和 uncontrolled component的控管關係會是如何？ ->->-> `使用原生DOM元素本身擁有的方式，但這很難從React去控管它的狀態、根據狀態來渲染`
<!--SR:!2024-07-20,421,250-->

#🧠  React ：請問React能方便控管uncontrolled component 的儲存狀態＆根據狀態來渲染畫面嗎？為什麼->->-> `不行，因為最主要會由原生元件來控制其狀態儲存和畫面選染`
<!--SR:!2023-05-31,170,250-->

#🧠 React ：請問React能方便控管controlled component 的儲存狀態＆根據狀態來渲染畫面嗎？為什麼 ->->-> `可以，因為正是使用著React體系來掌握`
<!--SR:!2024-03-12,339,250-->

#🧠 請描述React 體系下的狀態儲存和根據狀態更新畫面是什麼？ ->->-> `React 本身也有自己的體系，分別為：state、setState`
<!--SR:!2025-02-06,539,250-->

#🧠 React ：對於uncontrolled component，會有一些方法來獲取資訊和渲染，具體能夠對該component本身做什麼來實現狀態資料的獲取和渲染？->->-> ` - 獲取狀態 & 儲存狀態：擷取對應實際DOM節點，並從節點中取得資訊來儲存 - 渲染： - 透過擷取對應實際DOM節點，並從DOM節點上直接修改屬性來觸發更新狀態、渲染 - 從React的開發角度觸發原生元件的預設渲染，讓其根據狀態去渲染自己元件`
<!--SR:!2023-06-03,160,250-->

#🧠 React：uncontrolled component 如何產生->->-> `基於ref技術來實現component的狀態管理。`
<!--SR:!2024-09-27,448,250-->


#🧠 React ：對於controlled component，會有一些方法來獲取資訊和渲染，具體能夠對該component本身做什麼來實現狀態資料的獲取和渲染？->->-> `替元件註冊狀態、更新狀態用函式來實現`
<!--SR:!2023-06-05,150,230-->


#🧠 React ：對於controlled component的儲存狀態、根據狀態來更新畫面，會有什麼實際方式來實現(parent 和自己) ->->-> `1. 由parent 元件的狀態和更新狀態(兼渲染)用的函式來透過props和callback來控管controlled component，即元件上的儲存狀態和根據狀態而渲染全由parent元間來控管、2. 元件本身會有狀態來決定元件自己的狀態儲存、根據狀態而渲染`
<!--SR:!2024-07-04,320,230-->



---
Status: #🌱 
Tags:
[[React]] - [[JavaScript]]
Links:
[[原生HTML DOM元件都會有瀏覽器根據標準而開發出來的原生狀態管理實現，分別是將元件轉換成DOM物件來儲存狀態以及設定預設事件處理來變更狀態和渲染內容]]
References:
[[@reactUncontrolledComponentsReact]]
[[@ross-uAnswerWhatAre2021]]
[[@ithomeDay27JiShiTianQi]]
[[@chidumennamdiControlledVsUncontrolled]]
