## 描述


### IDE auto-completion.
若要讓IDE對Context的使用語法提供自動完成(auto-completion)功能，可以試著
1. 事先在createContext中的defaultValue設定未來會用到的資料型別是什麼，好讓IDE能夠更好地決定要添入什麼字元來完成程式碼，比如當寫下ctx.時，IDE會判斷ctx會有什麼屬性

2. 型別若是函式且沒引數，就設定dummy function，形式會是：
`onLogout: () => {}`

3. 型別若是函式且有引數，就設定dummy function，形式會是：
`onLogin: (email, password) => {}`



### 從Components抽離出專門處理Context狀態的Component和渲染對應畫面的Component
從Components抽離出專門處理狀態的Component，可獲得：
1. 專門處理狀態的Component
2. 渲染對應元件的Component

#### 專門處理狀態的Component 結構
如何做：
1. 重新建立一個Component代表著專門處理狀態
2. 該Component以對應Context的Provider Component為主來構築
3. 其內容在搭載著與Context相關的狀態、更新狀態用的函式、Effect


#### 渲染對應元件的Component 結構
如何做：
1. 移除被抽離的狀態、更新狀態用的函式、Effect

被抽離之後，剩下的Component就保有渲染對應元件畫面的職責，Provider Component就維持著負責狀態管理的職責



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


/src/index.js：將Provider Component為主的Component包含App Component，使該Component成為最頂層來將它擁有的狀態值往下傳遞
```
import React from 'react';
import ReactDOM from 'react-dom/client';
import { AuthContextProvider } from './store/auth-context';
import './index.css';
import App from './App';

const root = ReactDOM.createRoot(document.getElementById('root'));
root.render(
  <AuthContextProvider>
    <App />
  </AuthContextProvider>
);
```


#### 案例：被抽離後的component

App.js

1. 在main下，元件原本是如下，但由於onLogin和onLogout等更新isLoggedIn狀態的函式已經由AuthContext所擁有，後續想要使用其功能的元件只需要從context取得，不用從app component取得
```
{!ctx.isLoggedIn && <Login onLogin={...} />}
{ctx.isLoggedIn && <Home onLogout={...} />}
```


  

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
- 原則是為了提升易讀性和降低維護/開發難度

### auto-completion
Autocomplete
> Autocomplete, or word completion, is a feature in which an application predicts the rest of a word a user is typing.

重點：
- Autocomplete 或者 auto-completion 是由特定應用程式提供使用者藉由目前輸入內容來預判接下來的完整內容是什麼的功能


## 複習

#🧠 auto-completion 命名緣由是什麼？ ->->-> `Autocomplete 或者 auto-completion 是由特定應用程式提供使用者藉由目前輸入內容來預判接下來的完整內容是什麼的功能`

#🧠 single responsibility principle 是什麼原則->->-> `每一個類別、模組、函式都只會有一個職責或者單一目的來開發`

#🧠 提出single responsibility principle 是為了什麼？(開發、維護) ->->-> `提升易讀性和降低維護/開發難度`

#🧠 提出single responsibility principle 是為了什麼？ ->->-> `提升易讀性和降低維護/開發難度`

#🧠 React：假如以Context為主的管理狀態業務邏輯和其他Components寫在一塊，那麼還能有什麼樣重構方法？->->-> `從Components抽離出專門處理狀態的Component，分別為1. 專門處理狀態的Component 2. 渲染對應元件的Component`

#🧠 React：假如以Context為主的管理狀態業務邏輯和其他Components寫在一塊，若從Components抽離出專門處理狀態的Component，會獲得什麼哪兩種Component->->-> `1. 專門處理狀態的Component 2. 渲染對應元件的Component`

#🧠 React：假如以Context為主的管理狀態業務邏輯和其他Components寫在一塊，若從Components抽離出專門處理狀態的Component，會如何做？ ->->-> `1. 重新建立一個Component代表著專門處理狀態 2. 該Component以對應Context的Provider Component為主來構築 3. 其內容在搭載著與Context相關的狀態、更新狀態用的函式、Effect`

#🧠 React：假如以Context為主的管理狀態業務邏輯和其他Components寫在一塊，若從Components抽離出專門處理狀態的Component，那渲染對應元件的Component會如何得到？->->-> `移除被抽離的狀態、更新狀態用的函式、Effect`

#🧠 為何要從Components抽離出專門處理狀態的Component和渲染對應元件的Component？ ->->-> `實現單一職責原則，管理狀態就由負責管理狀態的component來負責，負責對應元件渲染就由該component負責`

#💻 請至/react-builder/question-review/useContext-Refactor-question下，請試著以抽離出專門處理Context狀態的Component和渲染對應畫面的Component ->->-> `https://github.com/academind/react-complete-guide-code/tree/10-side-effects-reducers-context-api/code/12-building-and-using-a-custom-context-provider-cmp/src`

---
Status: #🌱
Tags:
[[React]]
Links:
References:
[[@freecodecampSOLIDDefinitionSOLID2022]]