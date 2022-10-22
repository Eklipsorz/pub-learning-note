## 描述


### 單種驗證方式來進行


[[React：表格製作的難點為表格本身具有較多狀態要管理和控制]]
根據以上所提供，主要有以下驗證方向：
- 當表格提交時就驗證輸入欄位
- 當使用者輸入完輸入欄位或者從特定輸入欄位失去焦點就驗證
- 當使用者在輸入欄位輸入任意字元就驗證

#### 若表格都用同一種驗證的話

由於每一種驗證方式的觸發點皆為不一樣，不一定能夠滿足所有情況下的表格實現需求


### 多種驗證方式

將多種驗證方向組合在一起使用的原因會是：
- 利用各種驗證方向所擁有的利與弊來互補
- **由於每一種驗證方式的觸發點皆為不一樣，所以打造出更複雜的驗證方式**
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
### 案例：重構
- 第一點：去除掉enteredNameIsValid狀態，改用一般變數所存下的內容來判斷
```
  const [enteredName, setEnteredName] = useState('');
  const [enteredNameTouched, setEnteredNameTouched] = useState(false);

  const enteredNameIsValid = enteredName.trim() !== '';
  const nameInputIsInvalid = !enteredNameIsValid && enteredNameTouched;
```
而enteredNameIsValid源自於名字輸入欄位的change事件來的以及名字輸入欄位的blur事件，由於
change事件的合法性判斷源自於nameInputChangeHandler，在這裏可以直接取得從那更新的enteredName來判斷，接著一開始比對是否為非法，還可以透過blur事件所觸發的狀態更新來重執行一次函式來讓enteredName變成空值進而判斷成非法

- 第二點：去除掉handler內的enteredNameIsValid狀態更新
```
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
  };
```

- 第三點：解決名字重置後所需要重置的狀態-enteredNameTouched
```
    setEnteredName('');
    setEnteredNameTouched(false);
```


#### 完整版
```
import { useState } from 'react';

const SimpleInput = (props) => {
  const [enteredName, setEnteredName] = useState('');
  const [enteredNameTouched, setEnteredNameTouched] = useState(false);

  const enteredNameIsValid = enteredName.trim() !== '';
  const nameInputIsInvalid = !enteredNameIsValid && enteredNameTouched;

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
        <button>Submit</button>
      </div>
    </form>
  );
};

export default SimpleInput;

```


## 複習



#🧠 表格的驗證方式若同時搭配當表格提交時就驗證輸入欄位、當使用者輸入完輸入欄位或者從特定輸入欄位失去焦點就驗證、當使用者在輸入欄位輸入任意字元就驗證的原因是什麼？ ->->-> `由於每一種驗證方式的觸發點皆為不一樣，所以打造出更複雜的驗證方式、利用各種驗證方向所擁有的利與弊來互補`

#🧠 若表格都用同一種驗證來實現驗證的話，會有什麼潛在問題？->->-> `由於每一種驗證方式的觸發點皆為不一樣，不一定能夠滿足所有情況下的表格實現需求`


#🧠 若表格都用多種驗證來實現驗證的話，實現方式會是如何？ ->->-> ``




#💻 Question :: ->->-> ``

---
Status: #🌱 
Tags:
[[React]]
Links:
[[React：表格製作的難點為表格本身具有較多狀態要管理和控制]]
References: