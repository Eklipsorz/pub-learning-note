## 描述

### 表格若出現大量重複狀態設定和判斷

重構手段：

- 建立一個獨立的輸入欄元件並夾雜這些狀態設定和判斷
- 建立一個custom hook來包含業務邏輯



### custom hook 注意事項
keep in mind that the hook (and custom hooks in general) should be generic - it's not limited to one specific input

重點：
- 盡量讓custom hook保持通用，不可將業務邏輯限制在特定元件

### custom-hook：use-input.js



```
import { useState } from 'react';

const useInput = (validation) => {
  const [value, setValue] = useState('');
  const [isTouched, setIsTouched] = useState(false);

  const valueIsValid = validation(value);
  const hasError = !valueIsValid && isTouched;

  const valueChangeHandler = (event) => {
    setValue(event.target.value);
  };

  const inputBlurHandler = (event) => {
    setIsTouched(true);
  };
  
  const reset = () => {
    setValue('');
    setIsTouched(false);
  }

  return {
    value,
    hasError,
    valueIsValid,
    valueChangeHandler,
    inputBlurHandler,
    reset
  };
};

export default useInput;
```

#### 重構後的custom hook function 會回傳


```
- value：輸入欄內容
- isValid：輸入欄合法性
- hasError：是否有錯
- valueChangeHandler：change 事件處理器
- inputBlurHandler：blur 事件處理器
- reset：重置輸入欄內容、touched
```

#### 刪除表格提交處理器的第一個setEnteredNameTouched(true)

setEnteredNameTouched(true)原本是為了確定非法情況而添加，現在因為表格在非法情況下是不允許按下提交，所以也就可以去除掉該行

> because the form can't be submitted if the inputs are invalid anyways






### 完整代碼
```
import { useState } from 'react';
import useInput from '../hooks/use-input';

const SimpleInput = (props) => {
  const nameValidation = (name) => {
    return name !== '';
  };

  const emailValidation = (email) => {
    return email.includes('@');
  }

  const {
    value: enteredName,
    hasError: enteredNameHasError,
    valueIsValid: enteredNameIsValid,
    valueChangeHandler: nameInputChangeHandler,
    inputBlurHandler: nameInputBlurHandler,
    reset: nameInputReset,
  } = useInput(nameValidation);

  const {
    value: enteredEmail,
    hasError: enteredEmailHasError,
    valueIsValid: enteredEmailIsValid,
    valueChangeHandler: emailInputChangeHandler,
    inputBlurHandler: emailInputBlurHandler,
    reset: emailInputReset,
  } = useInput(emailValidation);

  let formIsValid = false;
  if (enteredNameIsValid && enteredEmailIsValid) {
    formIsValid = true;
  }

  const formSubmissionHandler = (event) => {
    event.preventDefault();

    if (enteredName.trim() === '' || enteredEmail.trim() === '') {
      return;
    }

    console.log(enteredName, enteredEmail);

    // nameInputRef.current.value = ''; => NOT IDEAL, DON'T MANIPULATE THE DOM

    nameInputReset();
    emailInputReset();
  };

  const nameInputClasses = enteredNameHasError
    ? 'form-control invalid'
    : 'form-control';

  const emailInputClasses = enteredEmailHasError
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
        {enteredNameHasError && (
          <p className='error-text'>Name must not be empty.</p>
        )}
      </div>
      <div className={emailInputClasses}>
        <label htmlFor='name'>Your Email</label>
        <input
          type='text'
          id='email'
          onChange={emailInputChangeHandler}
          onBlur={emailInputBlurHandler}
          value={enteredEmail}
        />
        {enteredEmailHasError && (
          <p className='error-text'>Email must includes @.</p>
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

#💻 請至/react-builder/question-review/form-adv-practice領取題目並切換至refactor-with-custom-hook分支，利用custom hook將輸入欄的value、touch、valid獲取邏輯包含並直接取代SimpleInput.js裡頭的輸入欄所擁有的業務邏輯 ->->-> `https://github.com/academind/react-complete-guide-code/tree/16-working-with-forms/code/10-re-using-the-custom-hook/src`
<!--SR:!2022-12-03,28,250-->


#🧠 React：表格若出現大量重複狀態設定和判斷，重構手段會是什麼？ ->->-> `- 建立一個獨立的輸入欄元件並夾雜這些狀態設定和判斷- 建立一個custom hook來包含業務邏輯 `
<!--SR:!2022-11-06,10,250-->

#🧠 React：custom hook 注意事項要保持什麼？ ->->-> `盡量讓custom hook保持通用，不可將業務邏輯限制在特定元件`
<!--SR:!2022-11-06,10,250-->






---
Status: #🌱 
Tags:
[[React]]
Links:
References: