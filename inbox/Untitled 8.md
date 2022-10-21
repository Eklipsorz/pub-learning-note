## 描述
```
1.  const nameInputChangeHandler = (event) => {
2.      setEnteredName(event.target.value);
3. 
4.      if (event.target.value.trim() !== '') {
5.          setEnteredNameIsValid(true);
6.      }
7.  }
```


```
1.  const nameInputBlurHandler = (event) => {
2.      setEnteredNameTouched(true);
3. 
4.      if (enteredName.trim() === '') {
5.          setEnteredNameIsValid(false);
6.      }
7.  }
```


典型多個驗證方式的案例：將比對是否合法和是否非法分按照需求給不同種類的驗證方式來處理

- blur 負責比對是否為非法，實現當使用者沒點選就呈現沒錯誤以及點選並切換其他元件為active element就驗證

- input 負責比對是否為合法，實現使用者一輸入就驗證成功



## 複習


---
Status: #🌱 
Tags:
Links:
References: