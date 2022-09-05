## 描述
### styled-components 的目標元件本身是原生HTML DOM元件的話

> ## Passed props
> If the styled target is a simple element (e.g. styled.div), styled-components passes through any known HTML attribute to the DOM. If it is a custom React component (e.g. styled(MyComponent)), styled-components passes through all props.

> This example shows how all props of the Input component are passed on to the DOM node that is mounted, as with React elements.
- 如果styled-component的目標元件本身是原生HTML DOM元件的話，會把元件標籤上所設定的屬性(attributes)直接賦予至對應實際DOM節點上所擁有的屬性(attribute)
- 案例如下：假若Element 為原生HTML DOM元件的話，那麼當解析讀取到Element標籤時就會呼叫定義的地方來獲取對應元件的Virtual DOM，其中把attribute1、attribute2最後設定給對應元件的實際DOM屬性上來當該DOM節點的屬性，屬性分別是attribute1=value1 和 attribute2=value2
```
// 定義
const Element = styled.<element>`<template-literal>`
// 定義後使用
<Element attribute1=value1 attribute2=value2> </Element>
```

## 複習


---
Status: #🌱 
Tags:
[[React]] - [[CSS]]
Links:
References: