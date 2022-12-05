


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

#### 使用前的注意事項
1. 確保有安裝styled-components這第三方套件
```
npm install --save styled-components
```

2. 使用前要載入其套件
```
import styled from 'styled-components';
```

#### 正式使用

當使用style.\<element\> 時，其實會建立對應元件的建構式，也就是React Element
```
const Element = styled.<element>`<template-literal>`
```

這個React Element 建構式預設會是回傳以下形式的內容：
	- 具體會是由\lelement\> \<\/element\> 所包裹著，裡頭內容會是props.children 
	- styled-components 的目標元件本身是原生HTML DOM元件的話，會把元件標籤上所設定的屬性(attributes)執行賦予至對應實際DOM節點上所擁有的屬性(attribute)

使用styled-component的元件為主的標籤，並賦予對應屬性(attribute)
```
<Element type={type1} onClick={onClick1}> </Element>
```

該屬性名和屬性值會接收到並轉換至styled-component的渲染內容裡：
```
  return (
    <element type={type1} onClick={onClick1}>
      {props.children}
    </element>
  );
```


#### 總結
使用styled-components 套件所建立的元件，預設下會有：
- 每個元件的對應渲染內容會包含props.children或者子節點
- 每個元件的對應渲染內容的元件屬性名稱(attribute)和屬性值(attribute)會依據元件標籤所用的屬性名稱(attribute)和屬性值(attribute)
```
<Element type={type1} onClick={onClick1}> </Element>
```
```
  return (
    <element type={type1} onClick={onClick1}>
      {props.children}
    </element>
  );
```

## 複習

#🧠 styled-components 是什麼樣技術概念的實現？ ->->-> `CSS-in-JS`
<!--SR:!2022-12-21,68,250-->

#🧠 Styled-components 如何防止CSS 全域污染問題->->-> `對綁定在特定元件A的樣式屬性區塊另外建立一個selector來包裝，其selector名稱會是獨特不重複，最後讓元件A的class連接至該selector`
<!--SR:!2023-02-16,78,247-->

#🧠 styled-components 是官方套件嗎？ 如何安裝->->-> `是第三方套件，安裝得用npm install styled-components`
<!--SR:!2023-03-19,113,247-->

#🧠 安裝styled-components好，若要使用其套件，要如何做？ ->->-> `先載入import styled from 'styled-components'; 然後該函式庫語法來將對應CSS內容和對應元件結合成syled-comoonents`
<!--SR:!2022-12-21,26,227-->

#🧠  styled-components 的出現背景是什麼？ ->->-> `預設下，專案下的所有css會是全域，無法讓特定css樣式屬性綁定在特定component。`
<!--SR:!2022-12-23,70,250-->


#🧠 styled-components 的出現背景是專案下的所有css會是全域，無法讓特定css樣式屬性綁定在特定component，這會衍生出什麼樣問題？ ->->-> `難以維護、開發的問題`
<!--SR:!2023-01-15,69,210-->

#🧠 styled-components 透過概念而實現的用途會是什麼？ ->->-> `主要是藉由實現CSS-in-JS的概念來讓特定樣式屬性綁定在特定元件下，不會產生CSS 相關的全域污染問題`
<!--SR:!2022-12-17,67,250-->

#🧠 styled-components 在實際DOM節點上，會綁定什麼樣class來當作class 屬性(attribute)值？ ->->-> `1. 自動替已經註冊在特定元件下的樣式內容生成一個獨特隨機名稱的className 2. 讓該元件的class屬性綁定於獨特隨機的className`
<!--SR:!2022-12-06,58,250-->

#🧠 styled-components 在實際DOM節點上，自動替已經註冊在特定元件下的樣式內容生成一個獨特隨機名稱的className 讓該元件的class屬性綁定於獨特隨機的className，請問目的為何？->->-> `在每個元件都能共享的CSSOM下，保證每個元件所使用的className 都對應著獨特且不重複的class selector `
<!--SR:!2023-01-31,88,230-->

#🧠 React：元件標籤上的style屬性和className屬性之間差別 ->->-> `前者是指定inline style，後者為設定對應元件所屬的類別。`
<!--SR:!2022-12-13,37,247-->

#🧠 在styled-components套件中，使用styled.\<element\>\`\<template-literal\>\`  後回傳的是什麼？->->-> `React Element 或者對應元件的建構式`
<!--SR:!2022-12-25,72,250-->

#🧠 在styled-components套件中，使用styled.\<element\>\`\<template-literal\>\`  後回傳的是React Element，其渲染內容為何？以程式碼來表示 ->->-> `return ( <element type={props.type} onClick={props.onClick}> {props.children}  </element> );`
<!--SR:!2022-12-19,68,250-->

#🧠 在styled-components套件中，使用styled.\<element\>\`\<template-literal\>\`  後回傳的是React Element，其渲染內容為  ![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1662214991/blog/react/style/css-in-js/styled-react-element_exjrbf.png) 中的type、onClick屬性如何定義的？->->-> `styled-components 的目標元件本身是原生HTML DOM元件的話，會把元件標籤上所設定的屬性(attributes)執行賦予至對應實際DOM節點上所擁有的屬性(attribute)`
<!--SR:!2022-12-23,70,250-->

#🧠 在styled-components套件中，使用styled.\<element\>\`\<template-literal\>\`  後回傳的是React Element，其渲染內容為  ![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1662214991/blog/react/style/css-in-js/styled-react-element_exjrbf.png) 中是如何定義該元件所包含的子節點？->->-> `預設下會有依照要產生的元件種類來產生對應子節點來被包含，如<element> </element> 所包裹的props.children`
<!--SR:!2022-12-27,73,250-->

#🧠 使用styled-components 套件所建立的元件，預設下會有什麼？ ->->-> `- 每個元件的對應渲染內容會包含props.children或者子節點 - 每個元件的對應渲染內容的元件屬性名稱(attribute)和屬性值(attribute)會依據元件標籤所用的屬性名稱(attribute)和屬性值(attribute)`
<!--SR:!2023-04-28,144,250-->

---
Status: #🌱 
Tags:
[[React]] - [[CSS]]
Links:
[[tagged template literal 是標記特定字串作為特定函式A的參數來使用，特定字串是會用template literal來構成]]
[[React：預設下，每個component 檔案所import的css並不會只限定於component才能使用，而是整個頁面上的元件都能存取]]
[[CSS-in-JS 是種技術，主要是將CSS樣式寫在JS內容，並運用JS程式語言的執行特色來根據執行情況來更改樣式中的內容]]
[[styled-components 的目標元件本身是原生HTML DOM元件的話，會把元件標籤上所設定的屬性(attributes)執行賦予至對應實際DOM節點上所擁有的屬性(attribute)]]
References: