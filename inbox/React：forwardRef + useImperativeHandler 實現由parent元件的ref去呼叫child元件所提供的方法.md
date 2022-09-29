## 描述


### forwardRef + useImperativeHandler 實現由parent元件的ref去呼叫child元件所提供的方法

/components/Login/Login.js：在這裡建立二兩個ref 物件：emailInputRef和passwordInputRef並傳遞Input元件，從那獲取對應child元件所提供的方法：讓指定輸入欄位變成active element，以利實現：
	- 當email欄位沒輸入就設定email欄位為active element
	- 當password欄位沒輸入就設定password欄位為active element
```
import React, {
  useState,
  useEffect,
  useReducer,
  useContext,
  useRef,
} from 'react';
.
.
.
.
.
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



/components/UI/Input/Input.js：當接收到由Login傳送過來的emailInputRef、passwordInputRef物件，透過forwardRef傳遞至對應輸入欄位的component function，由他們useImperativeHandler，來設定這兩個ref物件獲取activate方法，好讓parent元件能獲取
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

### 獲取流程
- 當Login.js進行渲染時，會將那兩個ref物件直接放入至Input component function所對應的forwardRefs來呼叫，並由它轉發ref物件至對應component function
```
forwardRefs((props, refs) => {})
```
- 做完component function後，且處理完forwardRefs會回傳能進行ref處理的component和對應畫面，此時ref已經對應好一組指令

## 複習

#💻 請使用forwardRef+useImperativeHandler 實現從Login.js那邊能夠獲取Input元件所提供的方法，進而實現在Login能根據輸入狀況而調整輸入欄位的focus情形，檔案在/react-builder/question-review/useImperativeHandle-question，要修改的Login是/components/Login/Login.js，而Input則是/components/UI/Input/Input.js ->->-> `https://github.com/academind/react-complete-guide-code/tree/10-side-effects-reducers-context-api/code/13-finished/src/components`
<!--SR:!2022-10-09,10,250-->


---
Status: #🌱 #📓 
Tags:
Links:
[[DOM.focus() 會指在同一份文件下，將特定元件標記為active element。一份文件裡只會有0~1個active element]]
[[React：forwardRef 是React函式庫的方法，專門將指定元件A下的Ref物件傳送forwardRef函式，並由該函式轉發至另一個對應元件B下來對指定元件A的Ref物件進行處理]]
[[React：useImperativeHandle 是定義一組以DOM原生渲染指令為主的處理來賦予至對應ref物件的current屬性]]
References: