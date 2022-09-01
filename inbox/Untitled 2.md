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
> const Button = styled.button``

> This Button variable here is now a React component that you can use like any other React component! This unusual backtick syntax is a new JavaScript feature called a tagged template literal.





## 複習


---
Status: #🌱 
Tags:
[[React]] - [[CSS]]
Links:
[[React：預設下，每個component 檔案所import的css並不會只限定於component才能使用，而是整個頁面上的元件都能存取]]
[[tagged template literal 是標記特定字串作為特定函式A的參數來使用，特定字串是會用template literal來構成]]
References:
[[@mdnTemplateLiteralsTemplate]]
[[@styled-componentsStyledcomponents]]