## 描述


### Firebase Auth REST API
1. firebase auth rest api 是一個簡單版的auth 認證後端伺服器，以REST風格來提供對應服務


#### API 案例

註冊API端點：
- API_KEY 為 firebase 專案的API KEY
```
https://identitytoolkit.googleapis.com/v1/accounts:signUp?key=[API_KEY]
```




##### 註冊端點使用案例
 - 設定註冊請求
 ```
 const res = await fetch(
        'https://identitytoolkit.googleapis.com/v1/accounts:signUp?key=xxx',
        {
          method: 'post',
          headers: { 'content-type': 'application/json' },
          body: JSON.stringify({
            email: enteredEmail,
            password: enteredPasssword,
            returnSecureToken: true,
          }),
        },
      );
```
 - 註冊請求處理狀態-isLoading
 - 在表單提交事件設定isLoading
```

	  setIsLoading(true);
	  // 處理請求前
      const res = await fetch(
		  'https://identitytoolkit.googleapis.com/v1/accounts:signUp?key=xxx',
        {
          method: 'post',
          headers: { 'content-type': 'application/json' },
          body: JSON.stringify({
            email: enteredEmail,
            password: enteredPasssword,
            returnSecureToken: true,
          }),
        },
      );
	  // 處理請求後
      setIsLoading(false);
      if (res.ok) {
      } else {
        const data = await res.json();
        if (data && data.error && data.error.message) alert(data.error.message);
      }
      console.log('successfully registered!!');
    }
```

- 註冊失敗就顯示視窗來提示
```
if (res.ok) {
} else {
    const data = await res.json();
    if (data && data.error && data.error.message) alert(data.error.message);
}
```
- 根據註冊狀態isLoading來呈現註冊請求正在處理中
```
return (
    <section className={classes.auth}>
      <h1>{isLogin ? 'Login' : 'Sign Up'}</h1>
      <form onSubmit={submitHandler}>
        <div className={classes.control}>
          <label htmlFor='email'>Your Email</label>
          <input type='email' id='email' ref={emailRef} required />
        </div>
        <div className={classes.control}>
          <label htmlFor='password'>Your Password</label>
          <input type='password' id='password' required ref={passwordRef} />
        </div>
        <div className={classes.actions}>
          {!isLoading ? (
            <button>{isLogin ? 'Login' : 'Create Account'}</button>
          ) : (
            <p>Sending Request...</p>
          )}

          <button
            type='button'
            className={classes.toggle}
            onClick={switchAuthModeHandler}
          >
            {isLogin ? 'Create new account' : 'Login with existing account'}
          </button>
        </div>
      </form>
    </section>
  );
```

##### 完整代碼
```
import { useState, useRef } from 'react';

import classes from './AuthForm.module.css';

const AuthForm = () => {
  const [isLogin, setIsLogin] = useState(true);
  const [isLoading, setIsLoading] = useState(false);

  const emailRef = useRef();
  const passwordRef = useRef();
  const switchAuthModeHandler = () => {
    setIsLogin((prevState) => !prevState);
  };

  const submitHandler = async (event) => {
    event.preventDefault();
    const enteredEmail = emailRef.current.value;
    const enteredPasssword = passwordRef.current.value;
    if (isLogin) {
    } else {
      setIsLoading(true);
      const res = await fetch(
        'https://identitytoolkit.googleapis.com/v1/accounts:signUp?key=AIzaSyA2nJWp4N2_qcV48cl-y0dTJCGAw6VHqLs',
        {
          method: 'post',
          headers: { 'content-type': 'application/json' },
          body: JSON.stringify({
            email: enteredEmail,
            password: enteredPasssword,
            returnSecureToken: true,
          }),
        },
      );

      setIsLoading(false);
      if (res.ok) {
      } else {
        const data = await res.json();
        if (data && data.error && data.error.message) alert(data.error.message);
      }
      console.log('successfully registered!!');
    }
  };

  return (
    <section className={classes.auth}>
      <h1>{isLogin ? 'Login' : 'Sign Up'}</h1>
      <form onSubmit={submitHandler}>
        <div className={classes.control}>
          <label htmlFor='email'>Your Email</label>
          <input type='email' id='email' ref={emailRef} required />
        </div>
        <div className={classes.control}>
          <label htmlFor='password'>Your Password</label>
          <input type='password' id='password' required ref={passwordRef} />
        </div>
        <div className={classes.actions}>
          {!isLoading ? (
            <button>{isLogin ? 'Login' : 'Create Account'}</button>
          ) : (
            <p>Sending Request...</p>
          )}

          <button
            type='button'
            className={classes.toggle}
            onClick={switchAuthModeHandler}
          >
            {isLogin ? 'Create new account' : 'Login with existing account'}
          </button>
        </div>
      </form>
    </section>
  );
};

export default AuthForm;
```

## 複習

#💻 請到/githubRepo/react-builder/question-review/react-auth-question 領取題目並切換至build-registration-practice分支，請在/src/components/Auth下的AuthForm增加帳密註冊功能，請調用Firebase上的Authentication REST API來用 ->->-> `https://github.com/academind/react-complete-guide-code/tree/22-authentication/code/03-showing-feedback`


---
Status: #🌱 
Tags:
[[Firebase]] - [[Authentication]] - [[React]]
Links:
References: