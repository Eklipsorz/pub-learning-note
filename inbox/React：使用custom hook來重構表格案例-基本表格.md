## 描述


### useInput 所需要的validation
將不需要重建的函式、物件、變數放在component之外
```
const isNotEmpty = (name) => name !== '';
const isValidEmail = (email) => email.includes('@');

function BasicForm = (props) => { ... }
```

### 針對每個輸入欄而註冊的hook
```
const BasicForm = (props) => {
  const {
    value: enteredFirstName,
    hasError: enteredFirstNameHasError,
    valueIsValid: enteredFirstNameIsValid,
    valueChangeHandler: firstNameChangeHandler,
    inputBlurHandler: firstNameInputBlurHandler,
    reset: firstNameReset,
  } = useInput(isNotEmpty);

  const {
    value: enteredLastName,
    hasError: enteredLastNameHasError,
    valueIsValid: enteredLastNameIsValid,
    valueChangeHandler: lastNameChangeHandler,
    inputBlurHandler: lastNameInputBlurHandler,
    reset: lastNameReset,
  } = useInput(isNotEmpty);

  const {
    value: enteredEmail,
    hasError: enteredEmailHasError,
    valueIsValid: enteredEmailIsValid,
    valueChangeHandler: emailChangeHandler,
    inputBlurHandler: emailInputBlurHandler,
    reset: emailReset,
  } = useInput(isValidEmail);
	.
	.
	.
}
```

### 根據custom hook所提供狀態來決定渲染

```
 let formIsValid = false;

  if (
    enteredFirstNameIsValid &&
    enteredLastNameIsValid &&
    enteredEmailIsValid
  ) {
    formIsValid = true;
  }

  const firstNameInputClasses = enteredFirstNameHasError
    ? 'form-control invalid'
    : 'form-control';

  const lastNameInputClasses = enteredLastNameHasError
    ? 'form-control invalid'
    : 'form-control';

  const emailInputClasses = enteredEmailHasError
    ? 'form-control invalid'
    : 'form-control';
```


### 提交事件處理

```
  const submitHandler = (event) => {
    event.preventDefault();
    event.stopPropagation();

    if (!formIsValid) return;

    console.log('submitted', enteredFirstName, enteredLastName, enteredEmail);

    firstNameReset();
    lastNameReset();
    emailReset();
  };
```

### 渲染部分(含錯誤提示部分)
```
return (
    <form onSubmit={submitHandler}>
      <div className='control-group'>
        <div className={firstNameInputClasses}>
          <label htmlFor='name'>First Name</label>
          <input
            type='text'
            id='name'
            value={enteredFirstName}
            onChange={firstNameChangeHandler}
            onBlur={firstNameInputBlurHandler}
          />
          {enteredFirstNameHasError && (
            <p className='error-text'>Please input a first name</p>
          )}
        </div>
        <div className={lastNameInputClasses}>
          <label htmlFor='name'>Last Name</label>
          <input
            type='text'
            id='name'
            value={enteredLastName}
            onChange={lastNameChangeHandler}
            onBlur={lastNameInputBlurHandler}
          />
          {enteredLastNameHasError && (
            <p className='error-text'>Please input a dlast name</p>
          )}
        </div>
      </div>
      <div className={emailInputClasses}>
        <label htmlFor='name'>E-Mail Address</label>
        <input
          type='text'
          id='name'
          value={enteredEmail}
          onChange={emailChangeHandler}
          onBlur={emailInputBlurHandler}
        />
        {enteredEmailHasError && (
          <p className='error-text'>Please input a valid email</p>
        )}
      </div>
      <div className='form-actions'>
        <button disabled={!formIsValid}>Submit</button>
      </div>
    </form>
  );
```

## 複習


#💻 請到/react-builder/question-review/form-adv-practice領取題目並切換至develop-complex-form-logic分支，請利用hooks中的useInput來對/src/BasicForm.js元件進行相關業務邏輯開發，需要的是 useInput 所需要的validation、針對每個輸入欄而註冊的hook、根據custom hook所提供狀態來決定渲染、提交事件處理、渲染部分(含錯誤提示部分)->->-> `https://github.com/academind/react-complete-guide-code/blob/16-working-with-forms/code/11-applying-our-hook-and-knowledge/src/components/BasicForm.js`
<!--SR:!2022-12-20,16,230-->




---
Status: #🌱 
Tags:
[[React]]
Links:
[[React：使用custom hook來重構表格]]
References: