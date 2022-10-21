## 描述


### 單種驗證方式來進行


[[React：表格製作的難點為格本身具有較多狀態要管理，主要有validity和value以及validity得要考量什麼時候驗證以及如何驗證]]
根據以上所提供，主要有以下驗證方向：
- 當表格提交時就驗證輸入欄位
- 當使用者輸入完輸入欄位或者從特定輸入欄位失去焦點就驗證
- 當使用者在輸入欄位輸入任意字元就驗證


以單獨使用特定驗證方式來看的話：
- 第一個方式很難及時驗證和回饋
- 第二個方式仍然很難及時驗證和回饋，只是可以憑藉輸入欄的blur事件來更快處理
- 第三個方式可以很及時驗證和回饋，只是會產生大量錯誤和不必要的計算，如剛開始的輸入


#### 在通常情況下，是否包含其他驗證能夠做的？

- 當表格提交時就驗證輸入欄位，包含著：
	- 無
- 當使用者輸入完輸入欄位或者從特定輸入欄位失去焦點就驗證，包含著：
	- 當表格提交時就驗證輸入欄位：由於點選提交按鈕勢必會從輸入欄位切換至按鈕為active element，這也剛好觸發blur事件以及提交事件來做驗證
- 當使用者在輸入欄位輸入任意字元就驗證，包含著：
	- 當表格提交時就驗證輸入欄位：由於是每一次輸入就驗證，所以本身就能包含
	- 當使用者輸入完輸入欄位或者從特定輸入欄位失去焦點就驗證：由於是每一次輸入就驗證，所以本身就能包含
	
### 多種驗證方式

將多種驗證方向組合在一起使用的原因會是：
- 利用各種驗證方向所擁有的利與弊來互補
實現方式：將比對是否合法和是否非法分按照需求給不同種類的驗證方式來處理

### 案例：未重構

blur 事件處理只專注在：比對是否為非法
- 比對是否為非法-即輸入欄位是否為空
- 若為空就變動
```
  const nameInputChangeHandler = (event) => {
    setEnteredName(event.target.value);
    if (event.target.value.trim() !== '') {
      setEnteredNameIsValid(true);
    }
  };
```


input 事件只專注在：比對是否為合法
- 比對是否為非法-即輸入欄位是否為空
```
  const nameInputBlurHandler = (event) => {
    setEnteredNameTouched(true);

    if (enteredName.trim() === '') {
      setEnteredNameIsValid(false);
    }
  };
```

#### 完整版

```
import { useState } from 'react';

const SimpleInput = (props) => {
  const [enteredName, setEnteredName] = useState('');
  const [enteredNameIsValid, setEnteredNameIsValid] = useState(false);
  const [enteredNameTouched, setEnteredNameTouched] = useState(false);

  const nameInputChangeHandler = (event) => {
    setEnteredName(event.target.value);
    if (event.target.value.trim() !== '') {
      setEnteredNameIsValid(true);
    }
  };

  const nameInputBlurHandler = (event) => {
    setEnteredNameTouched(true);

    if (enteredName.trim() === '') {
      setEnteredNameIsValid(false);
    }
  };

  const formSubmissionHandler = (event) => {
    event.preventDefault();

    setEnteredNameTouched(true);

    if (enteredName.trim() === '') {
      setEnteredNameIsValid(false);
      return;
    }

    setEnteredNameIsValid(true);

    console.log(enteredName);

    // nameInputRef.current.value = ''; => NOT IDEAL, DON'T MANIPULATE THE DOM
    setEnteredName('');
  };

  const nameInputIsInvalid = !enteredNameIsValid && enteredNameTouched;

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
        <button>Submit</button>
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
[[React：表格製作的難點為格本身具有較多狀態要管理，主要有validity和value以及validity得要考量什麼時候驗證以及如何驗證]]
References: