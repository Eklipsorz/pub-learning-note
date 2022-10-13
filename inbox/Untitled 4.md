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
- 官方提供的專用方法：
	- 允許在元件class或者元件對應函式添加contextType屬性來指定該元件class能夠存取的context object是什麼
	```
	// syntax sugar
	class Component1 {}
	Component1.contextType = Context1
	// non syntax sugar
	const Component1 = (function () { })
	Component1.contextType = Context1
	```
	- 允許在class添加一個名為contextType 的 static member variable來指定該元件class能夠存取到
- contextType 僅能填入context object


React class component 可以接受名為 `contextType` 的屬性。此屬性的用處與 `Context.Consumer` 相同，都是用來接收上層 `Provider` 傳下來的值。

  

  



  

  

contextType 指定元件要存取的context object會是什麼

  

在這裡使用static property只是分配記憶體給特定property，且只能指定一個context object


### 實際存取context object內容的方法

so if there are two contexts which should be connected to one at the same component, this would simply not be an option, you would have to find some other work around like wrapping it in a number component

若要存取contextType設定的context object，則是利用
this.context.xxxx即可存取



## 複習


---
Status: #🌱 
Tags:
[[React]]
Links:
[[在JS中，class 內部定義static method 或者 static property，代表著已經在執行前分配好記憶體給method或者property，換言之，就是不透過執行物件的實例化過程來分配]]
References:
[[@reactContextReact]]