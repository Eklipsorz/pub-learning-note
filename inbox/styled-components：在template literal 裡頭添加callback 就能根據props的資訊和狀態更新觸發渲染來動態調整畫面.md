## 描述


[[@styled-componentsStyledcomponentsBasics]]

### 在styled-components的literal 添加callback

```
// Create an Input component that'll render an <input> tag with some styles
const Input = styled.input`
  padding: 0.5em;
  margin: 0.5em;
  color: ${props => props.inputColor || "palevioletred"};
  background: papayawhip;
  border: none;
  border-radius: 3px;
`;

// Render a styled text input with the standard input color, and one with a custom input color
render(
  <div>
    <Input defaultValue="@probablyup" type="text" />
    <Input defaultValue="@geelen" type="text" inputColor="rebeccapurple" />
  </div>
);
```


> Note how the inputColor prop is not passed to the DOM, but type and defaultValue are. That is styled-components being smart enough to filter non-standard attributes automatically for you.


重點：
- 在styled-components的template-literal中，使用callback的話，會先執行callback得到對應的結果並替代callback所在的地方，最後以替代後的結果來當styled-components的方法之參數
- callback 的參數是對應元件的props物件
- 之所以可以使用callback，是使用了：
	- template literal ＋ \$\{\} 對於expression 優先執行


#### 案例1

使用 styled.div 方法建立以原生HTML DOM 元件為主的FormControl Component
```
const FormControl = styled.div`
  margin: 0.5rem 0;

  & label {
    font-weight: bold;
    display: block;
    margin-bottom: 0.5rem;
    color: ${(props) => (props.invalid ? 'red' : 'black')};
  }

  & input {
    display: block;
    width: 100%;
    border: 1px solid #ccc;
    font: inherit;
    line-height: 1.5rem;
    padding: 0 0.25rem;
    background: ${(props) => (props.invalid ? 'salmon' : ' transparent')};
    border-color: ${(props) => (props.invalid ? 'red' : '#ccc')};
  }

  & input:focus {
    outline: none;
    background: #fad0ec;
    border-color: #8b005d;
  }
`;
```

接著根據invalid 屬性和isValid狀態來動態呼叫對應的FormControl建構式來根據現有資訊和callback來產生對應內容和外表的FormControl元件

```
<FormControl invalid={!isValid}>
        <label>Course Goal</label>
        <input type='text' onChange={goalInputChangeHandler} />
</FormControl>
```

現有資訊和callback來產生對應內容和外表的FormControl元件：
```
  & label {
    font-weight: bold;
    display: block;
    margin-bottom: 0.5rem;
    color: ${(props) => (props.invalid ? 'red' : 'black')};
  }

  & input {
    display: block;
    width: 100%;
    border: 1px solid #ccc;
    font: inherit;
    line-height: 1.5rem;
    padding: 0 0.25rem;
    background: ${(props) => (props.invalid ? 'salmon' : ' transparent')};
    border-color: ${(props) => (props.invalid ? 'red' : '#ccc')};
  }
```

```
import React, { useState } from 'react';
import styled from 'styled-components';
import Button from '../../UI/Button/Button';
import './CourseInput.css';

const FormControl = styled.div`
  margin: 0.5rem 0;

  & label {
    font-weight: bold;
    display: block;
    margin-bottom: 0.5rem;
    color: ${(props) => (props.invalid ? 'red' : 'black')};
  }

  & input {
    display: block;
    width: 100%;
    border: 1px solid #ccc;
    font: inherit;
    line-height: 1.5rem;
    padding: 0 0.25rem;
    background: ${(props) => (props.invalid ? 'salmon' : ' transparent')};
    border-color: ${(props) => (props.invalid ? 'red' : '#ccc')};
  }

  & input:focus {
    outline: none;
    background: #fad0ec;
    border-color: #8b005d;
  }
`;

const CourseInput = (props) => {
  const [enteredValue, setEnteredValue] = useState('');
  const [isValid, setIsValid] = useState(true);

  const goalInputChangeHandler = (event) => {
    const value = event.target.value;

    if (value.trim().length) setIsValid(true);
    setEnteredValue(value);
  };

  const formSubmitHandler = (event) => {
    event.preventDefault();
    event.stopPropagation();

    if (!enteredValue.trim().length) {
      setIsValid(false);
      return;
    }
    props.onAddGoal(enteredValue);
  };

  return (
    <form onSubmit={formSubmitHandler}>
      <FormControl invalid={!isValid}>
        <label>Course Goal</label>
        <input type='text' onChange={goalInputChangeHandler} />
      </FormControl>
      <Button type='submit'>Add Goal</Button>
    </form>
  );
};

export default CourseInput;
```




### styled-components 的目標元件本身是原生HTML DOM元件的話

> ## Passed props
> If the styled target is a simple element (e.g. styled.div), styled-components passes through any known HTML attribute to the DOM. If it is a custom React component (e.g. styled(MyComponent)), styled-components passes through all props.

> This example shows how all props of the Input component are passed on to the DOM node that is mounted, as with React elements.
- 如果styled-component的目標元件本身是原生HTML DOM元件的話，會把元件所設定的屬性(attributes)直接賦予至對應實際DOM節點上所擁有的屬性(attribute)
- 案例如下：假若Element 為原生HTML DOM元件的話，那麼當解析讀取到Element標籤時就會呼叫定義的地方來獲取對應元件的Virtual DOM，其中把attribute1、attribute2最後設定給對應元件的實際DOM屬性上來當該DOM節點的屬性，屬性分別是attribute1=value1 和 attribute2=value2
```
// 定義
const Element = styled.<element>`<template-literal>`
// 定義後使用
<Element attribute1=value1 attribute2=value2> </Element>
```


## 複習


---
Status: #🌱 #📓
Tags:
[[React]] - [[CSS]]
Links:
References:
[[@styled-componentsStyledcomponentsBasics]]