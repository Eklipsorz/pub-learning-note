## 描述


### 單種驗證方式來進行


### 多種驗證方式

典型多個驗證方式的案例：將比對是否合法和是否非法分按照需求給不同種類的驗證方式來處理

- blur 負責比對是否為非法，實現當使用者沒點選就呈現沒錯誤以及點選並切換其他元件為active element就驗證

- input 負責比對是否為合法，實現使用者一輸入就驗證成功


### 案例：

blur 事件處理只專注在：比對是否為非法
- 比對是否為非法-即輸入欄位是否為空
- 若為空就變動
```
  const nameInputChangeHandler = (event) => {
    setEnteredName(event.target.value);
    if (event.target.value.trim() !== '') {
      setEnteredNameIsValid(true);
    }
  };
```


input 事件只專注在：比對是否為合法
- 比對是否為非法-即輸入欄位是否為空
```
  const nameInputBlurHandler = (event) => {
    setEnteredNameTouched(true);

    if (enteredName.trim() === '') {
      setEnteredNameIsValid(false);
    }
  };
```



## 複習


---
Status: #🌱 
Tags:
Links:
References: