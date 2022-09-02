## 描述

[[React：預設下，每個component 檔案所import的css並不會只限定於component才能使用，而是整個頁面上的元件都能存取]]

但這樣特性會在大型專案開發上出現：
- 難以維護、開發的問題


解決目標為：
- 讓每個component 都擁有自己的css樣式

### styled component
> style components is a package that helps you build
> - components which have certain styles attached to them where the styles really only affect the components to which they were attached and not any other components

[[@styled-componentsStyledcomponents]]
> import styled from 'styled-components';
> 
> const Button = styled.button``

> This Button variable here is now a React component that you can use like any other React component! This unusual backtick syntax is a new JavaScript feature called a tagged template literal.

> import styled from 'styled-components';
> const Button = styled.button``

使用styled物件下的button方法
- 回傳button 元件對應類別/建構式


styled-component 採用tagged template literal 來描述
- 形式：styled 為styled-component的套件名稱，element則是要渲染的元件是什麼
```
styled.<element>`<template-literal>`
```
- template-literal 則是以element為主會有的樣式屬性
	- 若element本身會有pseudo-class的selector設定，就以\&，比如說
	
	```
	styled.button`
		.button:focus {
		  outline: none;
		}
		
		.button:hover,
		.button:active {
		  background: #ac0e77;
		  border-color: #ac0e77;
		  box-shadow: 0 0 8px rgba(0, 0, 0, 0.26);
		}
		//
		&:focus {
		  outline: none;
		}
		
		&:hover,
		&:active {
		  background: #ac0e77;
		  border-color: #ac0e77;
		  box-shadow: 0 0 8px rgba(0, 0, 0, 0.26);
		}
	`
	```



## 複習


---
Status: #🌱 #📓
Tags:
[[React]] - [[CSS]]
Links:
[[React：預設下，每個component 檔案所import的css並不會只限定於component才能使用，而是整個頁面上的元件都能存取]]
[[tagged template literal 是標記特定字串作為特定函式A的參數來使用，特定字串是會用template literal來構成]]
[[styled-components 是一個專注將特定CSS樣式綁定在特定元件的第三方套件，其調用的方法會回傳具有特定樣式的元件]]
References:
[[@mdnTemplateLiteralsTemplate]]
[[@styled-componentsStyledcomponents]]
[[@styled-componentsStyledcomponentsBasics]]