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
	- 允許在class添加一個名為contextType 的 static member variable來指定context object
	```
	class Component1 {
		static contextType = Context1
	}
	```
- contextType 僅能填入context object
- 細節：
	- 針對class本身增加它所擁有的method、variable 或者 在對應class內添加static variable/method，都是相當於對著class本身增加它所擁有的method、variable

#### 對著class本身增加屬性 vs. 在class使用static 變數

對著class本身增加屬性 vs. 在class使用static 變數：
- 兩者皆為是對class本身增加屬性
- class的對應物件並不會獲取到這些屬性或者變數

對於第一個描述的案例：
```
class Class1 {
	static variable = 1;
};

class Class2 {}
Class2.variable = 1;

console.log(Class1, Class2);
```

```
[class Class1] { variable: 1 } [class Class2] { variable: 1 }
```

對於第二個描述的案例
```
class Class1 {
	static variable = 1;
	constructor() {
		this.name = 'hi'
	}
}

class Class2 {}
Class2.variable = 1;

const obj1 = new Class1();
const obj2 = new Class2();

console.log(Class1, Class2);
console.log(obj1, obj2);
```

```
[class Class1] { variable: 1 } [class Class2] { variable: 1 }
Class1 { name: 'hi' } Class2 {}
```

### 實際存取context object內容的方法

[[@reactContextReact]]
> The `contextType` property on a class can be assigned a Context object created by `React.createContext()`. Using this property lets you consume the nearest current value of that Context type using `this.context`.


若要存取contextType設定的context object，則是利用this.context.xxxx即可存取，而xxxx就是context object裡頭的屬性和方法

## 複習

#🧠  class-based component 存取context object的方法有哪兩種？ ->->-> `1.  使用consumer component來獲取對應context object的內容2. 使用元件類別下的contextType屬性 + this.context.xxx 來存取`
<!--SR:!2022-10-18,3,250-->

#🧠 React：使用consumer component來獲取對應context object的內容適用於哪些寫法 ->->-> `第一個方法能夠用在functional component 和 class-based component`
<!--SR:!2022-10-17,3,250-->

#🧠  React：使用元件類別下的contextType屬性 + this.context.xxx 來存取適用於哪些寫法->->-> `第二個方法只能夠用在class-based component`
<!--SR:!2022-10-18,3,250-->


#🧠 React：使用元件類別下的contextType屬性 + this.context.xxx 來存取，最多能存取多少個context object，為什麼？->->-> `只能存取一個context object，因為contextType只能填寫一種，所以就只能存取一個context object`
<!--SR:!2022-10-17,3,250-->

#🧠 React 官方提供的語法-contextType是做什麼？ (請說到類別和物件) ->->-> `設定元件class能夠存取的context object，讓對應元件類別下的物件只能夠存取對應的context object`
<!--SR:!2022-10-17,3,250-->

#🧠 React 官方提供的語法-contextType 語法是什麼？->->-> `元件class或者元件對應函式添加contextType屬性來指定對應context object；在class添加一個名為contextType 的 static member variable來指定context object`
<!--SR:!2022-10-17,3,250-->

#🧠 React 官方提供的語法-contextType 語法中，請用程式碼表示**在元件class或者元件對應函式添加contextType屬性來指定context object**這方法->->-> `class Component1 {} Component1.contextType = Context1`
<!--SR:!2022-10-17,3,250-->

#🧠 JS ：class Component1 \{\} Component1.contextType = Context1等同於是什麼？程式碼會是什麼？ ->->-> `對著名為Component1的函式物件添加contextType屬性，程式碼會是const Component1 = (function () { } Component1.contextType = Context1`
<!--SR:!2022-10-17,3,250-->


#🧠 React 官方提供的語法-contextType 語法中，請用程式碼表示**允許在class添加一個名為contextType 的 static member variable來指定context object**這方法 ->->-> `class Component1 { static contextType = Context1 }`
<!--SR:!2022-10-17,3,250-->

#🧠 請問class Component1 \{ static contextType = Context1 \} 等同於什麼語法->->-> `class Component1 {} Component1.contextType = Context1`
<!--SR:!2022-10-17,3,250-->

#🧠 JS ：對著class本身增加屬性 vs. 在class使用static 變數之間差別是什麼？共同點是什麼 ->->-> `首先他們兩者皆是對class本身增加屬性，所以是一樣的，只是表現方式不同、class的對應物件並不會獲取到這些屬性或者變數`
<!--SR:!2022-10-17,3,250-->


#🧠 JS ：對著class本身增加屬性 vs. 在class使用static 變數之間差別是什麼？class的對應物件會有該屬性或者static變數嗎？->->-> `class的對應物件並不會獲取到這些屬性或者變數`
<!--SR:!2022-10-17,3,250-->

#🧠 React 官方提供的語法要如何實際存取context object內容，假使已經設定contextType屬性->->-> `直接在class內使用this.context.xxxx，其中xxxx就是context object所能提供的屬性和方法。`
<!--SR:!2022-10-17,3,250-->

#🧠 functional component 下的useContext 可以使用多少個context object ->->-> `N個`
<!--SR:!2022-10-27,10,250-->





---
Status: #🌱 
Tags:
[[React]]
Links:
[[在JS中，class 內部定義static method 或者 static property，代表著已經在執行前分配好記憶體給method或者property，換言之，就是不透過執行物件的實例化過程來分配]]
References:
[[@reactContextReact]]