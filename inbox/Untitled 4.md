## 描述

we got two ways of using context.
1. 使用consumer component來獲取對應context object的內容

with use context, you can listen to multiple context in one of the same component by calling use context multiple times and pointing at different contexts.


class-based component

1. 僅能監聽並存取一個context object

  

functional component
1. 可以監聽並存取多個context object



React class component 可以接受名為 `contextType` 的屬性。此屬性的用處與 `Context.Consumer` 相同，都是用來接收上層 `Provider` 傳下來的值。

  

  

The `contextType` property on a class can be assigned a Context object created by `React.createContext()`. Using this property lets you consume the nearest current value of that Context type using `this.context`.

  

  

contextType 指定元件要存取的context object會是什麼

  

在這裡使用static property只是分配記憶體給特定property，且只能指定一個context object


so if there are two contexts which should be connected to one at the same component, this would simply not be an option, you would have to find some other work around like wrapping it in a number component

若要存取contextType設定的context object，則是利用
this.context.xxxx即可存取



## 複習


---
Status: #🌱 
Tags:
[[React]]
Links:
References: