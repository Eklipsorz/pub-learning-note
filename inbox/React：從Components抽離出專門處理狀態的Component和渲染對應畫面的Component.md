## 描述

for better IDE auto-completion.

1. 會事先在createContext中的defaultValue設定未來會用到的資料型別是什麼，好讓IDE能夠更好地補全程式碼，比如當寫下ctx.時，IDE會判斷ctx會有什麼屬性

2. 型別若是函式且沒引數，就設定dummy function，形式會是：
`onLogout: () => {}`

3. 型別若是函式且有引數，就設定dummy function，形式會是：
`onLogin: (email, password) => {}`



### 從Components抽離出專門處理狀態的Component和渲染對應畫面的Component


專門處理狀態的Component 會以對應Context的Provider Component為主來構築，其Component會夾雜著與Context相關的狀態、更新用函式、Effect

被抽離之後，Component就保有渲染對應元件畫面的職責，Provider Component就維持著負責狀態管理的職責



#### 目的
1. 實現單一職責原則(Single responsibility principle)

#### 案例：專門處理狀態的component

/src/store/auth-context.js
```
import React from 'react';

const AuthContext = React.createContext({
  isLoggedin: false,
});

export default AuthContext;
```

從components抽離出專門處理狀態的Component： /src/store/auth-context.js
```
import React, { useState, useEffect } from 'react';

const AuthContext = React.createContext({
  isLoggedIn: false,
  onLogout: () => {},
  onLogin: (email, password) => {},
});

const AuthContextProvider = (props) => {
  /* State Section */
  const [isLoggedIn, setIsLoggedIn] = useState(false);

  const loginHandler = (email, password) => {
    localStorage.setItem('isLoggedIn', '1');
    setIsLoggedIn(true);
  };
  const logoutHandler = () => {
    localStorage.removeItem('isLoggedIn');
    setIsLoggedIn(false);
  };

  /* Effect Section */
  useEffect(() => {
    const storedUserLoggedInInformation = localStorage.getItem('isLoggedIn');

    if (storedUserLoggedInInformation === '1') {
      setIsLoggedIn(true);
    }
  }, []);

  const resultValues = {
    isLoggedIn,
    onLogin: loginHandler,
    onLogout: logoutHandler,
  };

  return (
    <AuthContext.Provider value={resultValues}>
      {props.children}
    </AuthContext.Provider>
  );
};
export { AuthContextProvider };
export default AuthContext;
```

#### 案例：被抽離後的component

App.js
```
import React, { useContext } from 'react';

import Login from './components/Login/Login';
import Home from './components/Home/Home';
import MainHeader from './components/MainHeader/MainHeader';
import AuthContext from './store/auth-context';

function App() {
  const authCtx = useContext(AuthContext);

  return (
    <React.Fragment>
      <MainHeader />
      <main>
        {!authCtx.isLoggedIn && <Login />}
        {authCtx.isLoggedIn && <Home />}
      </main>
    </React.Fragment>
  );
}

export default App;

```


Login.js
```
import React, { useState, useEffect, useReducer, useContext } from 'react';

import Card from '../UI/Card/Card';
import classes from './Login.module.css';
import Button from '../UI/Button/Button';
import AuthContext from '../../store/auth-context';


const emailReducer = (prevState, action) => {
  switch (action.type) {
    case 'INPUT_CHANGE':
      return { value: action.value, isValid: action.value.includes('@') };
    case 'INPUT_BLUR':
      return { value: prevState.value, isValid: prevState.isValid };
    default:
      return { value: '', isValid: null };
  }
};

const passwordReducer = (prevState, action) => {
  switch (action.type) {
    case 'INPUT_CHANGE':
      return { value: action.value, isValid: action.value.trim().length > 6 };
    case 'INPUT_BLUR':
      return { value: prevState.value, isValid: prevState.isValid };
    default:
      return { value: '', isValid: null };
  }
};

const Login = (props) => {

  const authCtx = useContext(AuthContext)
	.
	.
	.
	.
  const submitHandler = (event) => {
    event.preventDefault();
    console.log('submit', emailState, passwordState);
    authCtx.onLogin(emailState.value, passwordState.value);
  };

  return (
    <Card className={classes.login}>
      <form onSubmit={submitHandler}>
        <div
          className={`${classes.control} ${
            emailState.isValid === false ? classes.invalid : ''
          }`}
        >
          <label htmlFor='email'>E-Mail</label>
          <input
            type='email'
            id='email'
            value={emailState.value}
            onChange={emailChangeHandler}
            onBlur={validateEmailHandler}
          />
        </div>
        <div
          className={`${classes.control} ${
            passwordState.isValid === false ? classes.invalid : ''
          }`}
        >
          <label htmlFor='password'>Password</label>
          <input
            type='password'
            id='password'
            value={passwordState.value}
            onChange={passwordChangeHandler}
            onBlur={validatePasswordHandler}
          />
        </div>
        <div className={classes.actions}>
          <Button type='submit' className={classes.btn} disabled={!formIsValid}>
            Login
          </Button>
        </div>
      </form>
    </Card>
  );
};

export default Login;

```

Home.js
```
import React, { useContext } from 'react';

import Card from '../UI/Card/Card';
import classes from './Home.module.css';
import Button from '../UI/Button/Button';
import AuthContext from '../../store/auth-context';

const Home = (props) => {
  const authCtx = useContext(AuthContext);
  return (
    <Card className={classes.home}>
      <h1>Welcome back!</h1>
      <Button onClick={authCtx.onLogout}>Logout</Button>
    </Card>
  );
};

export default Home;

```

### Single responsibility principle 

[[@freecodecampSOLIDDefinitionSOLID2022]]
> ## The Single Responsibility Principle (SRP)
> The idea behind the SRP is that every class, module, or function in a program should have one responsibility/purpose in a program. As a commonly used definition, "every class should have only one reason to change".


重點：
- 每一個類別、模組、函式都只會有一個職責或者單一目的來開發


## 複習


---
Status: #🌱 #📓 
Tags:
[[React]]
Links:
References:
[[@freecodecampSOLIDDefinitionSOLID2022]]