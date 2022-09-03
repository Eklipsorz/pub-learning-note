## 描述




### 在styled-components的literal 添加callback
[[@styled-componentsStyledcomponentsBasics]]
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
- 在styled-components的template-literal中，使用callback的話，由於本身是template-literal，所以會先執行callback得到對應的結果並替代callback所在的地方，最後以替代後的結果來當styled-components的方法之參數
- styled-components + callback  => 讓component的渲染樣式屬性會根據執行情況而更改
- callback 的參數是對應元件的props物件
- 之所以可以使用callback，是使用了：
	- template literal ＋ \$\{\} 對於expression 優先執行 + styled-components 對於expression 為callback的處理方式
	- styled-components 對於expression 為callback的處理方式：當styled-components讀取到後，會先執行callback，並以其callback結果來替代\$\{callback\} 所在的位置



#### 預設下，在template literal 使用callback
預設下，在template literal 中添加\$\{expression\}，其中expression並不支援執行callback並拿其結果來替代\$\{callback\} 所在的位置


若在template literal 添加\$\{expression\}，
```
const variable = 'hiii'

const string = `this is test: ${(variable) => {
	console.log('hi')
}}`;

console.log(string);
```

會讓JS引擎無法識別，而直接當作字串來處理，其結果會是：

```
this is test: (variable) => {
  console.log('hi')
}
```


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


## 複習
#🧠 在styled-components的template-literal中，要如何實現讓template-literal內的樣式屬性根據執行情況而更改？->->-> `在styled-components的template-literal中，使用${}並加入callback，由於本身是template-literal，所以會先執行callback得到對應的結果並替代callback所在的地方，最後以替代後的結果來當styled-components的方法之參數`


#🧠 在styled-components的template-literal中所使用的callback會是取得什麼樣參數來處理？->->-> `callback 的參數是對應元件的props物件`

#🧠 對於JS來說，在template literal 使用\$\{callback\} 能夠先直接callback然後以其結果來替代嗎？->->-> `並不能，會被JS引擎無法識別，而直接被當作字串來處理。`

#🧠 在styled-components的template-literal中，為何可以使用callback？ ->->-> ` template literal ＋ ${} 對於expression 優先執行 + styled-components 對於expression 為callback的處理方式：當styled-components讀取到後，會先執行callback，並以其callback結果來替代${callback} 所在的位置`


---
Status: #🌱 
Tags:
[[React]] - [[CSS]]
Links:
References:
[[@styled-componentsStyledcomponentsBasics]]