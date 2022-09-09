## 描述


在這裡會直接引入錯誤對話視窗至這邊的元件，當使用者輸入空值或者輸入負值歲數就會跑出錯誤訊息，並且將error物件當狀態變數來註冊在元件，拿error物件的建立來指示是否要渲染錯誤對話視窗：
	- 若輸入空值或者輸入負值歲數就會產出error物件，此時就會判定要渲染錯誤對話視窗
	- 若正確，就不用顯示

```
import { useState } from 'react';
import Card from '../UI/Card';
import Button from '../UI/Button';
import ErrorModal from '../UI/ErrorModal';
import styles from './UserInfoForm.module.css';

const UserInfoForm = (props) => {
  const [error, setError] = useState(null);
  const [userName, setUserName] = useState('');
  const [age, setAge] = useState('');

  const userNameChangeHandler = (event) => {
    setUserName(event.target.value);
  };

  const ageChangeHandler = (event) => {
    setAge(event.target.value);
  };

  const submitHandler = (event) => {
    event.preventDefault();
    event.stopPropagation();

    let title = '';
    let text = '';
    switch (true) {
      case age.trim().length && Number(age) <= 0: {
        title = 'Invalid Input';
        text = 'Please enter a valid age (> 0).';
        break;
      }
      case !userName.trim().length || !age.trim().length: {
        title = 'Invalid Input';
        text = 'Please enter a valid name and age (non-empty values).';
        break;
      }

      default:
        break;
    }

    if (title.length) {
      setError({ title, text });
      return;
    }

    const userData = {
      id: Math.random().toString(),
      name: userName,
      age: age,
    };

    props.onAddItem(userData);
    setUserName('');
    setAge('');
  };

  const onErrorModalClickHandler = () => {
    setError(null);
  };

  return (
    <div>
      {error && (
        <ErrorModal
          title={error.title}
          text={error.text}
          onErrorModal={onErrorModalClickHandler}
        ></ErrorModal>
      )}

      <Card>
        <form className={styles['form']} onSubmit={submitHandler}>
          <div className={styles['form-control']}>
            <label>Username</label>
            <input value={userName} onChange={userNameChangeHandler} />
          </div>
          <div className={styles['form-control']}>
            <label>Age(Years)</label>
            <input value={age} onChange={ageChangeHandler} />
          </div>
          <Button type='submit'>Add User</Button>
        </form>
      </Card>
    </div>
  );
};

export default UserInfoForm;
```

### modal 
在這裡會從parent 元件接收到title、text這些資訊以及搭配parent給予的callback-onErrorModal來建立對應對話視窗，onErrorModal主要會負責處理當使用者按下okay或者點擊modal外圍的話就讓modal消失。

modal 結構會有：
	- modal (負責存放modal-content)
	- modal-content (主要定義modal有什麼樣的內容)
		- modal-header
		- modal-body
		- modal-footer

```
import Button from './Button';
import styles from './ErrorModal.module.css';

const ErrorModal = (props) => {
  const { title, text } = props;

  const clickHandler = (event) => {
    props.onErrorModal();
  };

  return (
    <div className={styles['modal']} onClick={clickHandler}>
      <div className={styles['modal-content']}>
        <div className={styles['modal-header']}>
          <h2>{title}</h2>
        </div>
        <div className={styles['modal-body']}>
          <p>{text}</p>
        </div>
        <div className={styles['modal-footer']}>
          <Button onClick={clickHandler}>Okay</Button>
        </div>
      </div>
    </div>
  );
};

export default ErrorModal;
```


## 複習


---
Status: #🌱 
Tags:
[[React]] - [[CSS]]
Links:
[[modal 是一個專門與使用者互動並從互動中將資訊傳遞給主程式，其結構為存放modal、modal-content，製作方式請詳讀本文章]]
References:
