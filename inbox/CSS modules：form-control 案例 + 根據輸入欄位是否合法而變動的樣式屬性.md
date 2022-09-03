## 描述

### css

```
.form-control {
  margin: 0.5rem 0;
}

.form-control label {
  font-weight: bold;
  display: block;
  margin-bottom: 0.5rem;
}

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

### js

從CSS載入對應CSS 模組，並取得form-control selector的對應屬性styles['form-control']：
	- 在這裡要取styles的form-control屬性的話，是用styles['form-control'] ，而不是styles.form-control是因爲-這個字元會被當作數字運算符號，所以只能用另一種方式
	- 接著就是判斷目前輸入欄位是否合法，在這裡由於CSS Modules會把CSS內容的所有class selector全都重命名，所以必須以styles.invalid來表示，而不能夠以invalid這字元


```
<div className={`${styles['form-control']} ${!isValid && styles.invalid}`}>
	...
</div>
```





```
import React, { useState } from 'react';

import Button from '../../UI/Button/Button';
import styles from './CourseInput.module.css';

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
      <div
        className={`${styles['form-control']} ${!isValid && styles.invalid}`}
      >
        <label>Course Goal</label>
        <input type='text' onChange={goalInputChangeHandler} />
      </div>
      <Button type='submit'>Add Goal</Button>
    </form>
  );
};

export default CourseInput;
```


## 複習

---
Status: #🌱 #📓 
Tags:
[[React]] - [[CSS]]
Links:
[[CSS modules 為webpack的延伸套件，主要會在CSS 檔案 和JS檔案各自分開的情況下，實現讓每個元件都有各自屬於自己的樣式屬性內容]]
References: