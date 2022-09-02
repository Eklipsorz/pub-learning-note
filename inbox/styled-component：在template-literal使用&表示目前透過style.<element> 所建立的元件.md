
## 描述

### 使用&來表示目前透過style.\<element\> 所建立的元件

[[@styled-componentsStyledcomponentsBasics]]
> 	& a single ampersand refers to **all instances** of the component; it is used for applying broad overrides:

```
const Thing = styled.div.attrs((/* props */) => ({ tabIndex: 0 }))`
  color: blue;

  &:hover {
    color: red; // <Thing> when hovered
  }

  & ~ & {
    background: tomato; // <Thing> as a sibling of <Thing>, but maybe not directly next to it
  }

  & + & {
    background: lime; // <Thing> next to <Thing>
  }

  &.something {
    background: orange; // <Thing> tagged with an additional CSS class ".something"
  }

  .something-else & {
    border: 1px solid; // <Thing> inside another element labeled ".something-else"
  }
`

render(
  <React.Fragment>
    <Thing>Hello world!</Thing>
    <Thing>How ya doing?</Thing>
    <Thing className="something">The sun is shining...</Thing>
    <div>Pretty nice day today.</div>
    <Thing>Don't you think?</Thing>
    <div className="something-else">
      <Thing>Splendid.</Thing>
    </div>
  </React.Fragment>
)
```

重點：
- 在styled-component 中，選擇器部分(或者template-literal部分)若使用&填入，就表示目前透過style.\<element\> 所建立的元件
```
const Element = styled.<element>`<template-literal>`
```
- 可運用& 的selector場景：
	- CSS Combinator
	- element.class selector
	- Pseudoelements, pseudoselectors

#### 使用案例1
```
	const Button = styled.<element>`
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


#### 使用案例2


```
.form-control input {
  display: block;
  width: 100%;
  border: 1px solid #ccc;
  font: inherit;
  line-height: 1.5rem;
  padding: 0 0.25rem;
}

.form-control input:focus {
  outline: none;
  background: #fad0ec;
  border-color: #8b005d;
}

.form-control.invalid label {
  color: red;
}

.form-control.invalid input {
  background: salmon;
  border-color: red;
}
```
  
更改成&來表示對應元件
```
const FormControl = styled.div`
  & input {
     display: block;
     width: 100%;
     border: 1px solid #ccc;
     font: inherit;
     line-height: 1.5rem;
     padding: 0 0.25rem;
  }

  & input:focus {
     outline: none;
     background: #fad0ec;
     border-color: #8b005d;
  }

  &.invalid label {
     color: red;
  }

  &.invalid input {
     background: salmon;
     border-color: red;
  }
```

`

## 複習


---
Status: #🌱  #📓
Tags:
[[React]] - [[CSS]]
Links:
[[styled-components 是一個專注將特定CSS樣式綁定在特定元件的第三方套件，其調用的方法會回傳具有特定樣式的元件]]
References: