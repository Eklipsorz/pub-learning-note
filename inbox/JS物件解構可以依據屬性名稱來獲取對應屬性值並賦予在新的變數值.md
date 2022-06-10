

## 描述

引用[[@mdnJieGouFuZhiJavaScriptMDN]]所描述的
> ### [指派到新的變數名稱](https://developer.mozilla.org/zh-TW/docs/Web/JavaScript/Reference/Operators/Destructuring_assignment#%E6%8C%87%E6%B4%BE%E5%88%B0%E6%96%B0%E7%9A%84%E8%AE%8A%E6%95%B8%E5%90%8D%E7%A8%B1 "Permalink to 指派到新的變數名稱")

> 物件中的屬性可以解構並擷取到名稱跟該屬性不一樣的變數。

```
const o = {p: 42, q: true};
const {p: foo, q: bar} = o;

console.log(foo); // 42
console.log(bar); // true
```

舉例來說， `const {p: foo} = o` 把物件 `o` 裡名為 `p` 的屬性解出並指派到一個名為 `foo` 的本地變數。

重點：
- 物件解構會依據屬性名稱來從指定物件o來取得對應的p屬性值和q屬性值，接著把p屬性值賦予至foo這個變數以及把q屬性值賦予至bar這個變數



```
const o = {p: 42, q: true};
const {p: foo, q: bar} = o;
```

## 複習
#🧠 請說明下面語法在做啥？![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1654493334/blog/javascript/destructure/js-destructure-example_y814dg.png)->->-> `物件解構會依據屬性名稱來從指定物件o來取得對應的p屬性值和q屬性值，接著把p屬性值賦予至foo這個變數以及把q屬性值賦予至bar這個變數`
<!--SR:!2022-06-20,10,250-->


---
Status: #🌱 
Tags:
Links:
References:
[[@mdnJieGouFuZhiJavaScriptMDN]]
