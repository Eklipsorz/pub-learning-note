


## 描述

styled-components 本身是CSS-in-JS的實現案例之一

### styled-components 用途為

[[React：預設下，每個component 檔案所import的css並不會只限定於component才能使用，而是整個頁面上的元件都能存取]]

這樣特性會在大型專案開發上出現：
- 難以維護、開發的問題

styled-components 用途：
- 將特定樣式綁定在特定元件，不會產生CSS 相關的全域污染問題

### styled-components 為註冊在特定元件下的class生成一個獨特隨機的className

styled-component

1. 自動替已經註冊在特定元件下的樣式內容生成一個獨特隨機名稱的className
2. 讓該元件的class屬性綁定於獨特隨機的className

目的於：
- 在每個元件都能共享的CSSOM下，保證每個元件所使用的className 都對應著獨特且不重複的class selector 

#### 案例：使用styled-component來建立的元件而加載的class

在實際DOM樹狀結構下，button 會獲取到由styled-component所建立的className並加載 `<button type="submit" class="sc-AxjAm hHFnXX"> Add Goal </button>`

其中sc-AxjAm 和 hHFnXX是styled-component 另外產生出來的className

### styled-components 回傳的內容

當使用style.\<element\> 時，其實會建立對應元件的建構式，也就是React Element
```
const Element = styled.<element>`<template-literal>`
```

這個React Element 建構式預設會是回傳以下形式的內容：
	- 具體會是由\lelement\> \<\/element\> 所包裹著，裡頭內容會是props.children 
	- element 屬性(attribute)名稱和屬性值會是對應著該元件所擁有的props的屬性名稱(property)、屬性值來定義，比如props有type和onClick這兩個屬性(property)，這兩個會直接添加至對應element標籤下的屬性(attribute)
- styled-components 的目標元件本身是原生HTML DOM元件的話，會把元件標籤上所設定的屬性(attributes)執行賦予至對應實際DOM節點上所擁有的屬性(attribute)

```
  return (
    <element type={props.type} onClick={props.onClick}>
      {props.children}
    </element>
  );
```


## 複習

#🧠 styled-components 是什麼樣技術概念的實現？ ->->-> `CSS-in-JS`


#🧠  styled-components 的出現背景是什麼？ ->->-> `預設下，專案下的所有css會是全域，無法讓特定css樣式屬性綁定在特定component。`


#🧠 styled-components 的出現背景是專案下的所有css會是全域，無法讓特定css樣式屬性綁定在特定component，這會衍生出什麼樣問題？ ->->-> `難以維護、開發的問題`

#🧠 styled-components 透過概念而實現的用途會是什麼？ ->->-> `主要是藉由實現CSS-in-JS的概念來讓特定樣式屬性綁定在特定元件下，不會產生CSS 相關的全域污染問題`

#🧠 styled-components 在實際DOM節點上，會綁定什麼樣class來當作class 屬性(attribute)值？ ->->-> `1. 自動替已經註冊在特定元件下的樣式內容生成一個獨特隨機名稱的className 2. 讓該元件的class屬性綁定於獨特隨機的className`

#🧠 styled-components 在實際DOM節點上，自動替已經註冊在特定元件下的樣式內容生成一個獨特隨機名稱的className 讓該元件的class屬性綁定於獨特隨機的className，請問目的為何？->->-> `在每個元件都能共享的CSSOM下，保證每個元件所使用的className 都對應著獨特且不重複的class selector `

#🧠 在styled-components套件中，使用styled.\<element\>\`\<template-literal\>\`  後回傳的是什麼？->->-> `React Element 或者對應元件的建構式`

#🧠 在styled-components套件中，使用styled.\<element\>\`\<template-literal\>\`  後回傳的是React Element，其渲染內容為何？以程式碼來表示 ->->-> `return ( <element type={props.type} onClick={props.onClick}> {props.children}  </element> );`

#🧠 在styled-components套件中，使用styled.\<element\>\`\<template-literal\>\`  後回傳的是React Element，其渲染內容為  ![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1662214433/blog/react/style/css-in-js/styled-react-element_nksxq5.png) 中的type、onClick屬性如何定義的？->->-> `styled-components 的目標元件本身是原生HTML DOM元件的話，會把元件標籤上所設定的屬性(attributes)執行賦予至對應實際DOM節點上所擁有的屬性(attribute)`

#🧠 在styled-components套件中，使用styled.\<element\>\`\<template-literal\>\`  後回傳的是React Element，其渲染內容為  ![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1662214433/blog/react/style/css-in-js/styled-react-element_nksxq5.png) 中是如何定義該元件所包含的子節點？->->-> `具體會是由\lelement\> \<\/element\> 所包裹著，裡頭內容會是props.childre`

---
Status: #🌱 #📓
Tags:
[[React]] - [[CSS]]
Links:
[[tagged template literal 是標記特定字串作為特定函式A的參數來使用，特定字串是會用template literal來構成]]
[[React：預設下，每個component 檔案所import的css並不會只限定於component才能使用，而是整個頁面上的元件都能存取]]
[[CSS-in-JS 是種技術，主要是將CSS樣式寫在JS內容，並運用JS程式語言的執行特色來根據執行情況來更改樣式中的內容]]
[[styled-components 的目標元件本身是原生HTML DOM元件的話，會把元件標籤上所設定的屬性(attributes)執行賦予至對應實際DOM節點上所擁有的屬性(attribute)]]
References: