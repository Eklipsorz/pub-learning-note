## 描述


### 整體表單的validity

表單的所有輸入欄位皆為valid，那麼整體表單就為valid
表單的任一輸入欄位為invalid，那麼整體表單就為invalid


### 方法1：決定整體表單的validity

整體表單的validity：

1.  註冊狀態
```
const [formIsValid, setFormIsValid] = useState(false);
```
2.  在useEffect 內定義整體表單的validity，原因為它本身會依據其他輸入欄位的狀態變動才有機會改設定validity ，useEffect本身存在著debouncing 機制、deps機制能夠協助表單

3. 根據狀態來渲染


#### 案例：

1.  註冊狀態
```
const [formIsValid, setFormIsValid] = useState(false);
```

2. 在useEffect 內定義整體表單的validity
```
  useEffect(() => {
    if (enteredNameIsValid) {
      setFormIsValid(true);
    } else {
      setFormIsValid(false);
    }
  }, [enteredNameIsValid]);
```

3. 根據狀態來渲染
```
  return (
	<div className='form-actions'>
        <button disabled={!formIsValid}>Submit</button>
    </div>
  )
```


```
import { useState, useEffect } from 'react';

const SimpleInput = (props) => {
  const [enteredName, setEnteredName] = useState('');
  const [formIsValid, setFormIsValid] = useState(false);
  const [enteredNameTouched, setEnteredNameTouched] = useState(false);

  const enteredNameIsValid = enteredName.trim() !== '';
  const nameInputIsInvalid = !enteredNameIsValid && enteredNameTouched;

  useEffect(() => {
    if (enteredNameIsValid) {
      setFormIsValid(true);
    } else {
      setFormIsValid(false);
    }
  }, [enteredNameIsValid]);

  const nameInputChangeHandler = (event) => {
    setEnteredName(event.target.value);
  };

  const nameInputBlurHandler = (event) => {
    setEnteredNameTouched(true);
  };

  const formSubmissionHandler = (event) => {
    event.preventDefault();

    setEnteredNameTouched(true);

    if (enteredName.trim() === '') {
      return;
    }

    console.log(enteredName);

    // nameInputRef.current.value = ''; => NOT IDEAL, DON'T MANIPULATE THE DOM
    setEnteredName('');
    setEnteredNameTouched(false);
  };

  const nameInputClasses = nameInputIsInvalid
    ? 'form-control invalid'
    : 'form-control';

  return (
    <form onSubmit={formSubmissionHandler}>
      <div className={nameInputClasses}>
        <label htmlFor='name'>Your Name</label>
        <input
          type='text'
          id='name'
          onChange={nameInputChangeHandler}
          onBlur={nameInputBlurHandler}
          value={enteredName}
        />
        {nameInputIsInvalid && (
          <p className='error-text'>Name must not be empty.</p>
        )}
      </div>
      <div className='form-actions'>
        <button disabled={!formIsValid}>Submit</button>
      </div>
    </form>
  );
};

export default SimpleInput;

```

### 方法2：決定整體表單的validity

1.  建立一個變數名為formIsValid
2. 設定判斷式，來根據所有輸入欄位是否全都合法來給予true或者false
3. 根據狀態來渲染

#### 案例：

1.  建立一個變數名為formIsValid
```
let formIsValid = false;
```

2. 設定判斷式，來根據所有輸入欄位是否全都合法來給予true或者false
```
 if (enteredNameIsValid) {
    formIsValid = true;
  }
```

3. 根據狀態來渲染

```
  return (
	<div className='form-actions'>
        <button disabled={!formIsValid}>Submit</button>
    </div>
  )
```


```
import { useState } from 'react';

const SimpleInput = (props) => {
  const [enteredName, setEnteredName] = useState('');
  const [enteredNameTouched, setEnteredNameTouched] = useState(false);

  const enteredNameIsValid = enteredName.trim() !== '';
  const nameInputIsInvalid = !enteredNameIsValid && enteredNameTouched;

  let formIsValid = false;
  if (enteredNameIsValid) {
    formIsValid = true;
  }

  const nameInputChangeHandler = (event) => {
    setEnteredName(event.target.value);
  };

  const nameInputBlurHandler = (event) => {
    setEnteredNameTouched(true);
  };

  const formSubmissionHandler = (event) => {
    event.preventDefault();

    setEnteredNameTouched(true);

    if (enteredName.trim() === '') {
      return;
    }

    console.log(enteredName);

    // nameInputRef.current.value = ''; => NOT IDEAL, DON'T MANIPULATE THE DOM
    setEnteredName('');
    setEnteredNameTouched(false);
  };

  const nameInputClasses = nameInputIsInvalid
    ? 'form-control invalid'
    : 'form-control';

  return (
    <form onSubmit={formSubmissionHandler}>
      <div className={nameInputClasses}>
        <label htmlFor='name'>Your Name</label>
        <input
          type='text'
          id='name'
          onChange={nameInputChangeHandler}
          onBlur={nameInputBlurHandler}
          value={enteredName}
        />
        {nameInputIsInvalid && (
          <p className='error-text'>Name must not be empty.</p>
        )}
      </div>
      <div className='form-actions'>
        <button disabled={!formIsValid}>Submit</button>
      </div>
    </form>
  );
};

export default SimpleInput;

```



## 複習

---
Status: #🌱 
Tags:
[[React]]
Links:
References: