## 描述

[[@mdnConstructorJavaScriptMDN]]

> The constructor method is a special method of a class for creating and initializing an object instance of that class.

> A constructor enables you to provide any custom initialization that must be done before any other methods can be called on an instantiated object.


> If you don't provide your own constructor, then a default constructor will be supplied for you. If your class is a base class, the default constructor is empty:

```
constructor() {}
```

> If your class is a derived class, the default constructor calls the parent constructor, passing along any arguments that were provided:

```
constructor(...args) {
  super(...args);
}
```


重點：
- constructor 是每個類別的特殊方法，用來根據資訊來建立對應類別下物件並初始化
- 語法會是：
	- Class1 所要定義的類別
	- constructor 根據資訊來建立對應Class1類別下的實例，它的執行時機會是當使用者以new來建立實例時，必定執行且最先執行的方法
```
class Class1 {
	constructor() {
		....
	}
}
```

- 若使用者沒定義constructor，系統會根據目前類別是否繼承其他類別來提供預設的建構式：
	- 若沒繼承，則提供如下：
	```
	constructor() {}
	```
	- 若有繼承的話，則提供如下：會呼叫被繼承類別B的建構式，並傳遞由使用者傳遞過來的引數至類別B的建構式來建立對應類別B的實例，並以該類別B實例作為延伸來當作目前類別下的實例
	```
	consturctor(...args) {
		super(...args);
	}
	```


## 複習

#🧠 JS 中的class 建構式是什麼？ ->->-> `是每個類別的特殊方法，用來根據資訊來建立對應類別下物件並初始化`
<!--SR:!2024-11-04,461,250-->

#🧠 JS 中的class 搭配建構式的語法是什麼？ ->->-> `class Class1 { constructor() {....} }`
<!--SR:!2023-09-06,55,210-->


#🧠 JS中的class 建構式若沒開發者定義的話，並且使用new來呼叫建構式，系統會怎麼做？ ->->-> `系統會根據目前類別是否繼承其他類別來賦予預設的建構式`
<!--SR:!2025-01-14,509,250-->

#🧠 JS中的class 建構式若沒開發者定義的話，並且使用new來呼叫建構式，系統會根據目前類別是否繼承其他類別來賦予預設的建構式？若是沒繼承的話，會是建構式？ ->->-> `系統設定的建構式會是constructor() {}`
<!--SR:!2023-09-03,205,250-->


#🧠 JS中的class 建構式若沒開發者定義的話，並且使用new來呼叫建構式，系統會根據目前類別是否繼承其他類別來賦予預設的建構式？若是繼承的話，會是什麼建構式？ ->->-> `consturctor(...args) { super(...args) }`
<!--SR:!2023-12-13,105,230-->


#🧠 JS中的class 建構式若沒開發者定義的話，並且使用new來呼叫建構式，系統會根據目前類別是否繼承其他類別來賦予預設的建構式？若是繼承的話，會是什麼建構式？ (用文字說明) ->->-> `若有繼承的話，則提供如下：會呼叫被繼承類別B的建構式，並傳遞由使用者傳遞過來的引數至類別B的建構式來建立對應類別B的實例，並以該類別B實例作為延伸來當作目前類別下的實例
<!--SR:!2024-11-02,460,250-->
`


---
Status: #🌱 
Tags:
[[JavaScript]]
Links:
References:
[[@mdnConstructorJavaScriptMDN]]
