## 描述


### 存取context object的方式
1.  使用consumer component來獲取對應context object的內容
2. 使用元件類別下的contextType屬性 + this.context.xxx 來存取

第一個方法能夠用在functional component 和 class-based component；
第二個方法只能夠用在class-based component

#### 以官方提供的專用方法來看-context object的存取數多寡


使用元件類別下的contextType屬性 + this.context.xxx 來存取 這方法，由於只能透過contextType存取一個context object，所以這個方法最多就只能存取一個context object

functional component能使用的useContext 則是可以監聽並存取多個context object

### 以官方提供的專用方法來看-指定存取哪個context object
[[@reactContextReact]]
> The `contextType` property on a class can be assigned a Context object created by `React.createContext()`. Using this property lets you consume the nearest current value of that Context type using `this.context`.


```
class MyClass extends React.Component {
  componentDidMount() {
    let value = this.context;
    /* perform a side-effect at mount using the value of MyContext */
  }
  componentDidUpdate() {
    let value = this.context;
    /* ... */
  }
  componentWillUnmount() {
    let value = this.context;
    /* ... */
  }
  render() {
    let value = this.context;
    /* render something based on the value of MyContext */
  }
}
MyClass.contextType = MyContext;
```

重點：
- 官方提供的專用方法：設定元件class能夠存取的context object，讓對應元件類別下的物件只能夠存取對應的context object
	- 允許在元件class或者元件對應函式添加contextType屬性來指定context object
	```
	// syntax sugar
	class Component1 {}
	Component1.contextType = Context1
	// non syntax sugar
	const Component1 = (function () { })
	Component1.contextType = Context1
	```
	- 允許在class添加一個名為contextType 的 static member variable來指定
	```
	class Component1 {
		static contextType = Context1
	}
	```
- contextType 僅能填入context object
- 細節：
	- 針對class本身增加它所擁有的method、variable 或者 在對應class內添加static variable/method，都是相當於對著class本身增加它所擁有的method、variable
  

### 實際存取context object內容的方法

[[@reactContextReact]]
> The `contextType` property on a class can be assigned a Context object created by `React.createContext()`. Using this property lets you consume the nearest current value of that Context type using `this.context`.


若要存取contextType設定的context object，則是利用this.context.xxxx即可存取，而xxxx就是context object裡頭的屬性和方法

## 複習

#🧠  class-based component 存取context object的方法有哪兩種？ ->->-> `1.  使用consumer component來獲取對應context object的內容2. 使用元件類別下的contextType屬性 + this.context.xxx 來存取`

#🧠 React：使用consumer component來獲取對應context object的內容適用於哪些寫法 ->->-> `第一個方法能夠用在functional component 和 class-based component`

#🧠  React：使用元件類別下的contextType屬性 + this.context.xxx 來存取適用於哪些寫法->->-> `第二個方法只能夠用在class-based component`


#🧠 React：使用元件類別下的contextType屬性 + this.context.xxx 來存取，最多能存取多少個context object，為什麼？->->-> `只能存取一個context object，因為contextType只能填寫一種，所以就只能存取一個context object`

#🧠 React 官方提供的語法-contextType是做什麼？ (請說到類別和物件) ->->-> `設定元件class能夠存取的context object，讓對應元件類別下的物件只能夠存取對應的context object`

#🧠 React 官方提供的語法-contextType 語法是什麼？->->-> `元件class或者元件對應函式添加contextType屬性來指定對應context object`

#🧠 Question :: ->->-> ``

#🧠 Question :: ->->-> ``


#🧠 Question :: ->->-> ``


---
Status: #🌱 #📝 
Tags:
[[React]]
Links:
[[在JS中，class 內部定義static method 或者 static property，代表著已經在執行前分配好記憶體給method或者property，換言之，就是不透過執行物件的實例化過程來分配]]
References:
[[@reactContextReact]]