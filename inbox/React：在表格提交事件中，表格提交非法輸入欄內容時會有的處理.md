## 描述


瀏覽器對於資料上的內容需要一些驗證手段，然而由於每個使用者可透過瀏覽器來修改驗證手段使錯誤內容合法化，因此伺服器端也需要驗證手段來確保

### 提交非法輸入欄內容時會有的處理

1. 不允許提交
2. 使用特定樣式提示使用者目前輸入為非法

#### 案例：提交非法輸入欄內容時會有的處理

1. 不允許提交

```
  const submitHandler = (event) => {
    event.preventDefault();
    if (enteredName.trim() === '') {
      return;
    }
  };
```

2. 使用特定樣式提示使用者目前輸入為非法
- 註冊針對合法性的狀態，在這裡會設定為true，以利確保渲染部分不會直接印出非合法的樣式
```
const [enteredNameIsValid, setEnteredNameIsValid] = useState(true);
```
- 針對合法性的狀態之狀態更新邏輯
```
 const submitHandler = (event) => {
    event.preventDefault();

    if (enteredName.trim() === '') {
      setEnteredNameIsValid(false);
      return;
    }

    setEnteredNameIsValid(true);
    console.log(enteredName);
};
```
- 針對狀態來給予合適樣式
```
  const formControlCSS = enteredNameIsValid
    ? 'form-control'
    : 'form-control invalid';

  return (
    <form onSubmit={submitHandler}>
      <div className={formControlCSS}>
        <label htmlFor='name'>Your Name</label>
        <input
          type='text'
          id='name'
          onChange={changeHandler}
          value={enteredName}
        />
      </div>
      {!enteredNameIsValid && <p className='error-text'>Name is invalid!!</p>}
      <div className='form-actions'>
        <button>Submit</button>
      </div>
    </form>
  );
```

#### 案例：完整版
```
import { useState, useRef } from 'react';

const SimpleInput = (props) => {
  const [enteredName, setEnteredName] = useState('');
  const [enteredNameIsValid, setEnteredNameIsValid] = useState(true);

  const changeHandler = (event) => {
    setEnteredName(event.target.value);
  };

  const submitHandler = (event) => {
    event.preventDefault();

    if (enteredName.trim() === '') {
      setEnteredNameIsValid(false);
      return;
    }

    setEnteredNameIsValid(true);
    console.log(enteredName);
  };

  const formControlCSS = enteredNameIsValid
    ? 'form-control'
    : 'form-control invalid';

  return (
    <form onSubmit={submitHandler}>
      <div className={formControlCSS}>
        <label htmlFor='name'>Your Name</label>
        <input
          type='text'
          id='name'
          onChange={changeHandler}
          value={enteredName}
        />
      </div>
      {!enteredNameIsValid && <p className='error-text'>Name is invalid!!</p>}
      <div className='form-actions'>
        <button>Submit</button>
      </div>
    </form>
  );
};

export default SimpleInput;
```

## 複習


#🧠 React：面對要傳遞的資料，資料上的驗證要由誰負責？為何 ->->-> `前端和後端負責。瀏覽器對於資料上的內容需要一些驗證手段，然而由於每個使用者可透過瀏覽器來修改驗證手段使錯誤內容合法化，因此伺服器端也需要驗證手段來確保`
<!--SR:!2022-10-25,3,250-->

#🧠 React：在表格提交事件中，表格提交非法輸入欄內容時會有的處理是什麼？ ->->-> `1. 不允許提交 2. 使用特定樣式提示使用者目前輸入為非法`
<!--SR:!2022-11-04,10,250-->


---
Status: #🌱 
Tags:
[[React]]
Links:
[[React ：在表格提交事件中，表格下的輸入欄內容存取方式有兩種：第一種使用React體系的事件＋state；第二種為使用ref]]
References: