


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
- 在React中，controlled component & uncontrolled component 是用來描述表單元素
- 狀態儲存和根據狀態更新畫面，主要分為：
	- 原生DOM元素原有的狀態儲存和根據狀態更新畫面
	- React 體系下的狀態儲存和根據狀態更新畫面
- 若React 上的表單元件是基於原生DOM元素原有的方法來儲存自己表單資料＆渲染表單，那麼React 就無法以狀態來控管該元件，因而使該表單元件為uncontrolled component
- 若React 上的表單元件是採用React自己體系的狀態來儲存表單資料 & 渲染表單，那麼React 本身就能以狀態來控管這元件，因而使該表單元件為controlled component



### uncontrolled component
 對於uncontrolled component，會有一些方法來獲取資訊和渲染：
 - 獲取狀態 & 儲存狀態：擷取對應的DOM節點，並從節點中取得資訊來儲存
 - 渲染：從React的開發角度觸發原生元件的渲染，讓其根據狀態去渲染自己元件

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


#### 原生DOM元素原有的狀態儲存和更新
[[@ithomeDay27JiShiTianQi]]

> 之所以在表單元素上會區分「受 React 控制的資料」和「不受 React 控制的資料」，主要是因為在瀏覽器中，像是 `<input />` 這類的表單元素本身就可以保有自己的資料狀態，這也就是爲什麼當我們在 `<input />` 中輸入文字後，可以直接透過 JavaScript 選到該 input 元素後，再取出該元素的值，因為使用者輸入的內容（資料）可以直接保存在 `<input />` 元素內。


重點：
- 原生DOM元素：\<input\>, \<textarea\>, and \<select\> 
- 當表格的原生DOM元素與使用者發生互動時
	- 會直接將互動資料(狀態)儲存起來，好讓JavaScript選到該元素就能直接從中取得資料
	```
	// 選取到該元件
	const component = document.getElementById('xxxx')
	// 直接從元件儲存的狀態取得過來
	const value = component.value
	```
	- 根據互動資訊(狀態)來更新&渲染元素的方法

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

---
Status: #🌱 
Tags:
[[React]] - [[JavaScript]]
Links:
References:
[[@reactUncontrolledComponentsReact]]
[[@ross-uAnswerWhatAre2021]]
[[@ithomeDay27JiShiTianQi]]
[[@chidumennamdiControlledVsUncontrolled]]
