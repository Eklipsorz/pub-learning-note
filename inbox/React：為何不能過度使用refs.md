## 描述
[[@harryWeiShiMereactWuGuoDuShiYongRefs]]
> 因为 React 推崇 **数据不可变（immutable）**的编程思想，即不会直接修改对象的属性，而是深拷贝一份新对象，再对新的对象进行修改。  
> 
> 在 React 中每次 `setState` 传递的都是一个新的对象（新的引用），在更新渲染时 React 获取的也是新的对象，而 `refs` 在组件的每一个生命周期都保持唯一引用，修改 `ref.current` 的值使得其违背了 immutable 原则。

[[@reactRefsHeDOM]]
> 在很少的情況下，你可能會想要在 parent component 取得 child 的 DOM 節點。在一般的情形下，並不建議這麼做，因為這會破壞 component 的封裝





## 複習
---
Status: #🌱 #📓 
Tags:
Links:
References:
[[@harryWeiShiMereactWuGuoDuShiYongRefs]]
[[@reactRefsHeDOM]]