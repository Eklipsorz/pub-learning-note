

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

> ## **费解**

> 用了 this 之后，完整代码如下：

```text
var person = {
    name: 'Frank',
    age: 18,
    phone: '13812345678',
    sayHi: function(){
      console.log('你好，我是 ${this.name}，今年 ${this.age} 岁')
    },
    sayBye: function(){
      console.log('再见，记得我叫 ${this.name} 哦，想约我的话打电话给我，我的电话是 ${this.phone}')
    }
}

```

> 现在轮到新手疑惑了，这个 this 到底是个啥玩意儿？从哪来的呀？
实际上 this 是隐藏的第一个形参。在你调用 person.sayHi() 时，这个 person 会「变成」 this。

## 複習
#🧠 Question :: ->->-> ``

---
Status: #🌱 
Tags:
[[JavaScript]]
Links:
References:
[[@fangyinghangJSLiWeiShiMeHuiYouThis]]