## 描述
[[@harryWeiShiMereactWuGuoDuShiYongRefs]]
> 因为 React 推崇 **数据不可变（immutable）**的编程思想，即不会直接修改对象的属性，而是深拷贝一份新对象，再对新的对象进行修改。  
> 
> 在 React 中每次 `setState` 传递的都是一个新的对象（新的引用），在更新渲染时 React 获取的也是新的对象，而 `refs` 在组件的每一个生命周期都保持唯一引用，修改 `ref.current` 的值使得其违背了 immutable 原则。

[[@reactRefsHeDOM]]
> 在很少的情況下，你可能會想要在 parent component 取得 child 的 DOM 節點。在一般的情形下，並不建議這麼做，因為這會破壞 component 的封裝




> now, it's recommended that you don't manipulate it.
> Your DOM should really only be manipulated by React



> 什麼時候該使用 Ref

> 有幾種適合使用 ref 的情況：

> - 管理 focus、選擇文字、或影音播放。
> - 觸發即時的動畫。
> - 與第三方 DOM 函式庫整合。


rarely use refs to manipulate the DOM.

Here we're not really manipulating the DOM, we're not adding a new element.




You will sometimes have use cases where you just want to quickly read a value

and if you only want to read a value and you never plan on changing anything, well, then you don't really need state. because just to state as a keylogger is not that great. It's a lot of unnecessary code and work. 

so if you just want to read a value, refs are probably better.

refs, which are a little bit less code but you have this edge case of manipulating the DOM, or a state, which definitely cleaner but is a bit more code.


## 複習
---
Status: #🌱 #📓 
Tags:
Links:
References:
[[@harryWeiShiMereactWuGuoDuShiYongRefs]]
[[@reactRefsHeDOM]]