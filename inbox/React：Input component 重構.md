## 描述


### 重構前

```
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
```


### 重構目標
重構目標將 每個如下形式的元件組合物重新轉換成一個大元件，並以props來傳遞指定資訊來塑造成可重複使用的輸入欄組合元件
```
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
```

預期結果會是

```
	<Input 
	  type="email" 
	  label="E-mail"
	  id="email" 
	  isValid={state.isValid} 
	  value={state.value}
	  onChange={stateChangeHandler}
	  onBlur={validateStateHandler}
	/>
```
### 重構後

1. 製作Input Component 並使用props接收parent 元件給定的訊息。
```
import classes from './Input.module.css';

const Input = (props) => {
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
        value={props.value}
        onChange={props.onChange}
        onBlur={props.onBlur}
      />
    </div>
  );
};

export default Input;

```



2. 將Input component 插入至登入頁面，其最後合併結果：
```
return (
    <Card className={classes.login}>
      <form onSubmit={submitHandler}>
        <Input
          type='email'
          id='email'
          label='E-mail'
          isValid={emailIsValid}
          value={emailState.value}
          onChange={emailChangeHandler}
          onBlur={validateEmailHandler}
        ></Input>
        <Input
          type='password'
          id='password'
          label='Password'
          isValid={passwordIsValid}
          value={passwordState.value}
          onChange={passwordChangeHandler}
          onBlur={validatePasswordHandler}
        ></Input>
        <div className={classes.actions}>
          <Button type='submit' className={classes.btn} disabled={!formIsValid}>
            Login
          </Button>
        </div>
      </form>
    </Card>
  );
```

## 複習

#💻 請到/react-builder/question-review/refactor-Input-question領取題目，請將/components/Login/Login.js中的input組合元件做出可重複使用的元件 ->->-> `https://github.com/academind/react-complete-guide-code/tree/10-side-effects-reducers-context-api/code/13-finished/src/components/UI/Input`


---
Status:  #🌱 
Tags:
[[React]]
Links:
[[在定義react element的for屬性時，由於for本身是JS的保留字且react element是JS延伸語法，貿然使用會有衝突的可能，所以會用htmlFor來替代for屬]]
References: