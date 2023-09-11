

## 描述
[[@fangyinghangJSLiWeiShiMeHuiYouThis]] 所描述：
> 这篇文章是从语言创造者（JS 之父的角度）来思考 this

> ## **需求**
> 假设我们有一个对象

```js
var person = {
    name: 'Frank',
    age: 18,
    phone: '13812345678',
    sayHi: function(){
      // 待补充
    },
    sayBye: function(){
      // 待补充
    }
}
```

> 这个 person 对象有 name 和 age 属性，还有一个 sayHi 方法，现在的需求是：

> 调用 person.sayHi(...)，打印出「你好，我是 Frank，今年 18 岁」。  
> 调用 person.sayBuy(...)，打印出「再见，记得我叫 Frank 哦，想约我的话打电话给我，我的电话是 13812345678」

> 需求就是这么简单，通过达成这个需求，我们就能理解 this 的本质。

重點：
- 問題描述如何使用一個person物件下的sayHi和sayBye來根據其物件下的資訊來印出指定內容，這些方法主要要印出其物件下的name、age、phone


### 方法1

> ## **最傻的方案**

```js
var person = {
    ...
    sayHi: function(name, age){
      console.log('你好，我是 ${name}，今年 ${age} 岁')
    },
    sayBye: function(name, phone){
      console.log('再见，记得我叫 ${name} 哦，想约我的话打电话给我，我的电话是 ${phone}')
    }
}
```
> 调用方式是

```text
person.sayHi(person.name, person.age)
person.sayBye(person.name, person.phone)
```

> 别急，我知道这代码很傻，接下来改进。

方法1重點：
- 將person物件下的sayHi和sayBye打造成如下：函式宣告依照所需屬性來宣告
```
function sayHi(name, age) {
	// code
}
	
function sayBye(name, phone) {
	// code
}
```
- 調用person物件下的方法： 呼叫時就直接事先拿要處理的person物件，來按照屬性分派參數
```
const person1 = getPerson(...)
person.sayHi(person1.name, person1.age)
person.sayBye(person1.name, person.phone)
```
- 缺點是：
	- 對於人類開發而言，這種呼叫形式是很累贅的，因為.前面就有person，參數卻還要填入person物件
	- 需要的參數是person物件下的特定屬性，卻要跟著實際屬性來填入，這樣若要N個屬性，那麼呼叫的參數就要載入N個

### 方法2

> ## **第一次改进**

> 上面方法中，每次都要在调用的时候自行选择 person.name 作为参数，真的很傻，不如直接传入一个 person，代码如下：

```js
var person = {
    ...
    sayHi: function(self){
      console.log('你好，我是 ${self.name}，今年 ${self.age} 岁')
    },
    sayBye: function(self){
      console.log('再见，记得我叫 ${self.name} 哦，想约我的话打电话给我，我的电话是 ${self.phone}')
    }
}
```

> 调用方式是

```text
person.sayHi(person)
person.sayBye(person)
```

> 稍微好一点了，但是这代码依然很傻。  
为什么不能把参数里的 person 省掉，变成 person.sayHi() 就好了。


方法2重點：
- 將person物件下的sayHi和sayBye打造成如下：填入指定的person物件，來讓函式自己從物件中取得想要的屬性，在這裡會將參數取名為self，是由於本身是拿同樣是person物件的實體來印出對應結果，以物件導向語言的邏輯上來說的話，就是實體在呼叫自己所屬的方法，方法所用的屬性就是從實體中取出，如同狗在吠叫，叫聲(參數)本身內建的汪汪，而不是喵喵
```
function sayHi(self) {
	//....
}

function sayBye(self) {
	//....
}
```
- 調用person物件下的方法：事先獲取想要的person物件，然後將該物件當作參數入至這兩個方法
```
const person1 = getPerson(...)
person.sayHi(person1)
person.sayBye(person1)
```
- 與方法1改進：
	- 函式所需的參數再也不會依據物件上的屬性數量來決定，比如說物件上的屬性數量是N個，那麼函式所需的參數最多會是N個(考量實際運用)。
	- 依據想要的person物件來填入，所以參數量只會是一個
- 缺點：
	- 對於人類開發而言，這種呼叫形式是很累贅的，因為.前面就有person，參數卻還要填入person物件


### 方法3


> ## **加糖**

> 开发者最想要的调用方式是 person.sayHi()，那么问题来了，如果 person.sayHi() 没有实参，person.sayHi 函数是如何接收到 person 的呢？

> 1.  方法1：依然把第一个参数 self 当做 person，这样形参就会永远比实参多出一个 self
> 2.  方法2：隐藏 self，然后用关键字 this 来访问 self。

> JS 之父选择了方法2，用 this 访问 self。Python 之父选择了方法1，留下 self 作为第一个参数。

> 过程如下：

```text
// 用 this 之前：
sayHi: function(self){
    console.log('你好，我是 ${self.name}，今年 ${self.age} 岁')
}
// 用 this 之后：
sayHi: function(){
    // this 就是 self
    console.log('你好，我是 ${this.name}，今年 ${this.age} 岁')
}
```

方法3重點：
- 主要解決下述缺點
	- 對於人類開發而言，這種呼叫形式是很累贅的，因為.前面就有person，參數卻還要填入person物件
- 能解決方案如下所示：是否透過語法改造成人類可以接受的形式
	- 方法1： 依然採用將想要存取的物件當作參數來載入並且顯示，這樣每次呼叫物件下的方法都會多出一個物件參數
	- 方法2： 依然採用將想要存取的物件當作參數來載入但不顯示，這樣每次呼叫下的方法都不會呈現出需要多一個物件參數，但在執行函式時會以一個隱藏變數this來表示對應被隱藏的參數物件，換言之，this等同於呼叫該方法的物件，或者說要存取的物件被載入特定物件的方法來處理
```
// 方法1
function sayHi(self) {
	// code....
}

function sayBye(self) {
	// code....
}
// 方法2

function sayHi() {
	variable = getData(this)
	// code...with variable
}

function sayBye() {
	variable = getData(this)
	// code...with variable
}
```

 - 實際選擇上：
	 - python 語言使用方案1
	 - javascript 語言使用方案2

## 複習
#🧠 假如在person物件下定義兩個方法sayHi和sayBye，那麼若想透過person所擁有的name、age、phone來處理和印出的話，請問該如何做，請先用最傻的方案 (提示：要什麼屬性就用什麼屬性)![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1655534693/blog/javascript/object/object-self-example1_bcjr5l.png) ->->-> `person的sayHi和sayBye函式宣告會是要name、age、phone這三種person會有屬性，實際呼叫的話，就直接先獲取指定person物件，然後按照person.name、person.age、person.phone來呼叫`
<!--SR:!2024-06-30,449,250-->


#🧠 假如在person物件下定義兩個方法sayHi和sayBye，並且定義兩個函式宣告是以函式所需要的物件屬性來宣告的話，會有什麼樣的缺點？(提示：所需的屬性數越多和呼叫形式很累贅) ![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1655535068/blog/javascript/object/object-self-method1_lgbab7.png)->->-> `-   需要的參數是person物件下的特定屬性，卻要跟著實際屬性來填入，這樣若要N個屬性，那麼呼叫的參數就要載入N個 -   對於人類開發而言，這種呼叫形式是很累贅的，因為.前面就有person，參數卻還要填入person物件 `
<!--SR:!2023-11-27,125,210-->


#🧠 假如在person物件下定義兩個方法sayHi和sayBye，那麼若想透過person所擁有的name、age、phone來處理和印出的話，請問該如何做，能否縮減至一個參數的函式，而不是要N個屬性就給N個參數 (提示：object.name object.age)  ![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1655534693/blog/javascript/object/object-self-example1_bcjr5l.png) ->->-> `person的sayHi和sayBye函式宣告為一個物件，稱作為self參數名稱，當要呼叫person.sayHi和person.sayBye時就載入指定要存取的物件，比如person.sayHi(person1)，然後由函式本身自己向物件索要屬性來要，而不是從參數那邊指定要哪個屬性。`
<!--SR:!2024-06-11,438,250-->


#🧠 假如在person物件下定義兩個方法sayHi和sayBye，並且定義兩個函式宣告是以函式所需要的物件來宣告，並由函式本身自己向物件索要想要的屬性，這和單純要N個屬性就載入N個參數的形式相比，有什麼樣改善？(提示：所需的屬性數) ![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1655535068/blog/javascript/object/object-self-method2_q19eld.png) ->->-> `-   函式所需的參數再也不會依據物件上的屬性數量來決定，比如說物件上的屬性數量是N個，那麼函式所需的參數最多會是N個(考量實際運用)。-   依據想要的person物件來填入，所以參數量只會是一個`
<!--SR:!2024-08-18,483,250-->

#🧠 假如在person物件下定義兩個方法sayHi和sayBye，並且定義兩個函式宣告是以函式所需要的物件來宣告，還存在著什麼樣的缺點 （提示：呼叫形式好像很多餘) ![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1655535068/blog/javascript/object/object-self-method2_q19eld.png) ->->-> `-   對於人類開發而言，這種呼叫形式是很累贅的，因為.前面就有person，參數卻還要填入person物件`
<!--SR:!2024-05-20,425,250-->


#🧠 假如在person物件下定義兩個方法sayHi和sayBye，那麼若想透過person所擁有的name、age、phone來處理和印出的話，請問該如何做，能否不用參數就能索要？ (提示：this)  ![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1655534693/blog/javascript/object/object-self-example1_bcjr5l.png)  ->->-> `將原本語法形式改造成不需要參數的語法形式，使其讓人類變得很容易理解和使用，比如依然採用將想要存取的物件當作參數來載入但不顯示，這樣每次呼叫下的方法都不會呈現出需要多一個物件參數，但在執行函式時會以一個隱藏變數this來表示對應被隱藏的參數物件，換言之，this等同於呼叫該方法的物件，或者說要存取的物件被載入特定物件的方法來處理`
<!--SR:!2024-07-30,470,250-->

#🧠 假如在person物件下定義兩個方法sayHi和sayBye，那麼若想透過person所擁有的name、age、phone來處理和印出的話，請問該如何做，最佳實踐有哪兩個 (提示：不用參數和用一個參數)？python 會用哪個？ js會用哪個  ![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1655534693/blog/javascript/object/object-self-example1_bcjr5l.png)  ->->-> `-   方法1： 依然採用將想要存取的物件當作參數來載入並且顯示，這樣每次呼叫物件下的方法都會多出一個物件參數-   方法2： 依然採用將想要存取的物件當作參數來載入但不顯示，這樣每次呼叫下的方法都不會呈現出需要多一個物件參數，但在執行函式時會以一個隱藏變數this來表示對應被隱藏的參數物件，換言之，this等同於呼叫該方法的物件，或者說要存取的物件被載入特定物件的方法來處理，python 會用前者；js會用後者`
<!--SR:!2023-10-07,25,190-->



---
Status: #🌱 
Tags:
[[JavaScript]]
Links:
[[this、self、me等關鍵字在電腦語言中是指目前執行的代碼屬於哪一個實體物件]]
References:
[[@fangyinghangJSLiWeiShiMeHuiYouThis]]