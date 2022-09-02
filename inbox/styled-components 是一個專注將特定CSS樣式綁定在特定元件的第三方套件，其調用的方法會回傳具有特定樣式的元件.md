


## 描述


### styled-components 用途為

[[React：預設下，每個component 檔案所import的css並不會只限定於component才能使用，而是整個頁面上的元件都能存取]]

這樣特性會在大型專案開發上出現：
- 難以維護、開發的問題

styled-components 用途：
- 將特定樣式註冊在特定元件

### styled-components 為註冊在特定元件下的class生成一個獨特隨機的className

styled-component

1. 自動替已經註冊在特定元件下的class生成一個獨特隨機的className
2. 讓該元件綁定於獨特隨機的className

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

```
  return (
    <element type={props.type} onClick={props.onClick}>
      {props.children}
    </element>
  );
};
```







## 複習


---
Status: #🌱 #📓
Tags:
[[React]] - [[CSS]]
Links:
[[tagged template literal 是標記特定字串作為特定函式A的參數來使用，特定字串是會用template literal來構成]]
[[React：預設下，每個component 檔案所import的css並不會只限定於component才能使用，而是整個頁面上的元件都能存取]]
References: