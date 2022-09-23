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
	  label="E-ma"
	  id="email" 
	  isValid={state.isValid} 
	  value={state.value}
	  onChange={stateChangeHandler}
	  onBlur={validateStateHandler}
	/>
```


## 複習


---
Status:  #🌱 #📓 
Tags:
[[React]]
Links:
[[在定義react element的for屬性時，由於for本身是JS的保留字且react element是JS延伸語法，貿然使用會有衝突的可能，所以會用htmlFor來替代for屬]]
References: