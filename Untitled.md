


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
    this.input = React.createRef();  }

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

controlled component & uncontrolled component 是表單元素
在表單元素中，原生DOM元素如\<input\>, \<textarea\>, and \<select\> 等元素本身具有儲存使用者所輸入的內容(狀態)和根據內容(狀態)來更新&渲染元素的方法

React 本身也有自己的體系來儲存每個元件的狀態和藉由更新狀態而觸發更新&渲染對應元件的方法

若React 上的表單元件是採用原生DOM元素原有的方法來儲存自己表單資料＆渲染表單，那麼React 就無法以狀態來控管該元件，因而使該表單元件為uncontrolled component

若React 上的表單元件是採用React自己體系的狀態來儲存表單資料 & 渲染表單，那麼React 本身就能以狀態來控管這元件，因而使該表單元件為controlled component

方式1:
其parent 元件會透過props 和 它自己的狀態來傳遞給controlled component

方式2:
元件本身會有狀態來決定自身的渲染和業務邏輯


### 其他文獻

[[@ithomeDay27JiShiTianQi]]
> ## Controlled vs Uncontrolled Components

> 在 React 中表單元素的處理主要可以分成兩種 Controlled 和 Uncontrolled 這兩種，這裡**關於 Controlled 和 Uncontrolled 指的是「資料受不受到 React 所控制」，也就是「受 React 所控制的資料（Controlled）」或「不受 React 所控制的資料（Uncontrolled）」**。




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
