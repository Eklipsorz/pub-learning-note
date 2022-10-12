

## 描述

### 目標
1. 當使用者沒輸入任何內容就提交，就讓部分元件更改樣式來提醒使用者要輸入
	- Label => 錯誤：文字顏色為紅色
	- Input => 錯誤：框色為紅色以及背景為salmon
2. 當使用者輸入內容時，元件要以正確的形式來呈現
	- Label => 正確：文字顏色為黑色
	- Input => 正確：框色#ccc、background為transparent

### 實現概念

1. 當使用者沒輸入任何內容就提交，就讓部分元件更改樣式來提醒使用者要輸入
	- 當表單提交事件處理時，檢查有沒有輸入內容，沒的話就呈現錯誤樣式並停止增加

2. 當使用者輸入內容時，元件要以正確的形式來呈現
	- 當使用者要對輸入欄輸入時，就將樣式一率調整成正確的樣式

### 實現1：使用state + inline style + conditional operator

註冊狀態：
```
const [isValid, setIsValid] = useState(true);
```

輸入欄位變動就檢查是否有輸入，有的話藉由更新狀態函式來重新渲染並更新狀態為true
```
 const goalInputChangeHandler = (event) => {
    const value = event.target.value;

    if (value.trim().length) setIsValid(true);
    setEnteredValue(value);
  };
```


表單提交時檢查是否有輸入，沒的話，就藉由更新狀態函式來重新渲染並更新狀態為false
```
const formSubmitHandler = (event) => {
    event.preventDefault();
    event.stopPropagation();

    if (!enteredValue.trim().length) {
      setIsValid(false);
      return;
    }
    props.onAddGoal(enteredValue);
  };
```

根據isValid 來分別指定label、input會有的樣式，以inline style實現
```
return (
    <form onSubmit={formSubmitHandler}>
      <div className='form-control'>
        <label
          style={{
            color: !isValid ? 'red' : 'black',
          }}
        >
          Course Goal
        </label>
        <input
          type='text'
          style={{
            borderColor: !isValid ? 'red' : '#ccc',
            background: !isValid ? 'salmon' : 'transparent',
          }}
          onChange={goalInputChangeHandler}
        />
      </div>
      <Button type='submit'>Add Goal</Button>
    </form>
  );
```




```
import React, { useState } from 'react';

import Button from '../../UI/Button/Button';
import './CourseInput.css';

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
      <div className='form-control'>
        <label
          style={{
            color: !isValid ? 'red' : 'black',
          }}
        >
          Course Goal
        </label>
        <input
          type='text'
          style={{
            borderColor: !isValid ? 'red' : '#ccc',
            background: !isValid ? 'salmon' : 'transparent',
          }}
          onChange={goalInputChangeHandler}
        />
      </div>
      <Button type='submit'>Add Goal</Button>
    </form>
  );
};

export default CourseInput;

```


### 實現2 ：使用state + class + conditional operator
事先定義輸入正常的樣式和輸入錯誤的樣式在CSS檔案內，接著利用元件的class屬性來新增字串來切換成不合法的樣式，接著當要恢復正常時，就將新增的字串弄成空字串，以恢復原有正常的樣式

事先在輸入錯誤的樣式在CSS檔案內，正確版本已經事先設定好
```
// 設定在處於invalid狀態的control下的label 元件
.form-control.invalid label {
  color: red;
}

// 設定在處於invalid狀態的control下的input 元件
.form-control.invalid input {
  background: salmon;
  border-color: red;
}
```


註冊狀態：
```
const [isValid, setIsValid] = useState(true);
```

輸入欄位變動就檢查是否有輸入，有的話藉由更新狀態函式來重新渲染並更新狀態為true
```
 const goalInputChangeHandler = (event) => {
    const value = event.target.value;

    if (value.trim().length) setIsValid(true);
    setEnteredValue(value);
  };
```


表單提交時檢查是否有輸入，沒的話，就藉由更新狀態函式來重新渲染並更新狀態為false
```
const formSubmitHandler = (event) => {
    event.preventDefault();
    event.stopPropagation();

    if (!enteredValue.trim().length) {
      setIsValid(false);
      return;
    }
    props.onAddGoal(enteredValue);
  };
```

由於JSX語法糖中只有{expression}才是唯一能夠執行JS的地方，所以只能從div元件的className來使用{}，接著在使用template literal 來建立模板字元來透過事先執行的結果和form-control結合成新的多個class，而事先執行則是看isValid是否為true，true就空字串，false就invalid，以此來切換
```
  return (
    <form onSubmit={formSubmitHandler}>
      <div className={`form-control ${isValid ? '' : 'invalid'}`}>
        <label>Course Goal</label>
        <input type='text' onChange={goalInputChangeHandler} />
      </div>
      <Button type='submit'>Add Goal</Button>
    </form>
  );
```

## 複習

#🧠 在不使用任何能夠將樣式侷限於元件的技術下，如何用inline style的程式碼來實現以下功能：當使用者沒輸入任何內容就提交，會讓標籤文字顏色變成red和輸入欄框線和背景分別變成red和salmon；當使用者輸入內容時，標籤文字顏色變成黑色和輸入欄框線色和背景分別為#ccc 和 transparent ![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1662045565/blog/react/style/input-style_r9h5bj.png) ->->-> ``
<!--SR:!2022-12-04,58,250-->


#🧠 在不使用任何能夠將樣式侷限於元件的技術下，如何使用除了inline style以外的程式碼來實現以下功能：當使用者沒輸入任何內容就提交，會讓標籤文字顏色變成red和輸入欄框線和背景分別變成red和salmon；當使用者輸入內容時，標籤文字顏色變成黑色和輸入欄框線色和背景分別為#ccc 和 transparent ![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1662045565/blog/react/style/input-style_r9h5bj.png)  ->->-> ``
<!--SR:!2022-12-21,70,250-->




---
Status: #🌱 
Tags:
[[React]] - [[CSS]]
Links:
References:



