## 描述


在這裡會有兩個輸入欄位會使用以下元件的渲染內容，並於mount階段透過useRef來對著對應輸入欄位執行focus()來決定active element是什麼，結果會因為限制，最終會是由最後渲染的輸入欄來成為active element

```
import { useRef, useEffect } from 'react';
import classes from './Input.module.css';

const Input = (props) => {

  const inputRef = useRef()

  useEffect(() => {
    inputRef.current.focus()
  },[])

  return (
    <div
      className={`${classes.control} ${
        props.isValid === false ? classes.invalid : ''
      }`}
    >
      <label htmlFor={props.id}>{props.label}</label>
      <input
        type={props.type}
        id={props.id}
        ref={inputRef}
        value={props.value}
        onChange={props.onChange}
        onBlur={props.onBlur}
      />
    </div>
  );
};

export default Input;
```


> useImperativeHandle

> allows us to use this Component or functionalities from  inside this Component imperatively, which simple means not through the regular state props management not by controlling the component through state in the parent Component, but instead by directly calling or manipulating something in the Component programmatically


that is something you rarely wanna use and therefore, you shouldn't use it very often

  

function component

1. 大部分情況下，引數會是只有一個props

2. 少部分會有第二個引數 - ref (從外部引入進來的)

1.  function parent (props) {
2.    const ref = useRef
3.     return (
4.        <Component ref={...} />
5.      )
6.  }

8.  function Component(props, ref) {

10.   .....
11.  }

1. Component 是自製的

2. ref 是源自於parent 元件所建立的useRef回傳而來的ref

3. 當對Component標籤添加ref 這屬性(attribute)，就會在Component 對應的function component的ref引數接收到

  

  

  

useImperativeHandle(ref, callback)

  

callback：

1. 回傳一個物件，物件上會夾雜著資料

> you will be able to use from outside

```
import React, {
  useState,
  useEffect,
  useReducer,
  useContext,
  useRef,
} from 'react';

import Card from '../UI/Card/Card';
import classes from './Login.module.css';
import Button from '../UI/Button/Button';
import AuthContext from '../../store/auth-context';
import Input from '../UI/Input/Input';

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
  const authCtx = useContext(AuthContext);
  const emailInputRef = useRef();
  const passwordInputRef = useRef();
  const [emailState, emailDispatch] = useReducer(emailReducer, {
    value: '',
    isValid: null,
  });

  const [passwordState, passwordDispatch] = useReducer(passwordReducer, {
    value: '',
    isValid: null,
  });

  const [formIsValid, setFormIsValid] = useState(false);

  useEffect(() => {
    console.log('EFFECT RUNNING');

    return () => {
      console.log('EFFECT CLEANUP');
    };
  }, []);

  const { isValid: emailIsValid } = emailState;
  const { isValid: passwordIsValid } = passwordState;

  useEffect(() => {
    const identifier = setTimeout(() => {
      console.log('Checking form validity!');
      setFormIsValid(emailIsValid && passwordIsValid);
    }, 500);

    return () => {
      console.log('CLEANUP');
      clearTimeout(identifier);
    };
  }, [emailIsValid, passwordIsValid]);

  const emailChangeHandler = (event) => {
    emailDispatch({ type: 'INPUT_CHANGE', value: event.target.value });
  };

  const passwordChangeHandler = (event) => {
    passwordDispatch({ type: 'INPUT_CHANGE', value: event.target.value });
  };

  const validateEmailHandler = () => {
    emailDispatch({ type: 'INPUT_BLUR' });
  };

  const validatePasswordHandler = () => {
    passwordDispatch({ type: 'INPUT_BLUR' });
  };

  const submitHandler = (event) => {
    event.preventDefault();
    if (emailIsValid && passwordIsValid) {
      authCtx.onLogin(emailState.value, passwordState.value);
    } else if (!emailIsValid) {
      emailInputRef.current.focus();
    } else {
      passwordInputRef.current.focus();
    }
  };

  return (
    <Card className={classes.login}>
      <form onSubmit={submitHandler}>
        <Input
          type='email'
          id='email'
          label='E-mail'
          ref={emailInputRef}
          isValid={emailIsValid}
          value={emailState.value}
          onChange={emailChangeHandler}
          onBlur={validateEmailHandler}
        ></Input>
        <Input
          type='password'
          id='password'
          label='Password'
          ref={passwordInputRef}
          isValid={passwordIsValid}
          value={passwordState.value}
          onChange={passwordChangeHandler}
          onBlur={validatePasswordHandler}
        ></Input>
        <div className={classes.actions}>
          <Button type='submit' className={classes.btn}>
            Login
          </Button>
        </div>
      </form>
    </Card>
  );
};

export default Login;

```




```
import { useRef, useEffect, forwardRef, useImperativeHandle } from 'react';
import classes from './Input.module.css';

const Input = forwardRef((props, ref) => {
  const inputRef = useRef();

  const activate = () => {
    inputRef.current.focus();
  };

  useImperativeHandle(ref, () => {
    return {
      focus: activate,
    };
  });

  return (
    <div
      className={`${classes.control} ${
        props.isValid === false ? classes.invalid : ''
      }`}
    >
      <label htmlFor={props.id}>{props.label}</label>
      <input
        type={props.type}
        id={props.id}
        ref={inputRef}
        value={props.value}
        onChange={props.onChange}
        onBlur={props.onBlur}
      />
    </div>
  );
});

export default Input;

```




## 複習


---
Status: #🌱 #📓 
Tags:
Links:
[[DOM.focus() 會指在同一份文件下，將特定元件標記為active element。一份文件裡只會有0~1個active element]]
[[React：forwardRef 是React函式庫的方法，專門將指定元件A下的Ref物件傳送forwardRef函式，並由該函式轉發至另一個對應元件B下來對指定元件A的Ref物件進行處理]]
[[React：useImperativeHandle 是定義一組以DOM原生渲染指令為主的處理來賦予至對應ref物件的current屬性]]
References: