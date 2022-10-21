## 描述


### 單種驗證方式來進行


[[React：表格製作的難點為格本身具有較多狀態要管理，主要有validity和value以及validity得要考量什麼時候驗證以及如何驗證]]
根據以上所提供，主要有以下驗證方向：
- 當表格提交時就驗證輸入欄位
- 當使用者輸入完輸入欄位或者從特定輸入欄位失去焦點就驗證
- 當使用者在輸入欄位輸入任意字元就驗證


以單獨使用特定驗證方式來看的話：
- 第一個方式很難及時驗證和回饋
- 第二個方式仍然很難及時驗證和回饋，只是可以憑藉輸入欄的blur事件來更快處理
- 第三個方式可以很及時驗證和回饋，只是會產生大量錯誤和不必要的計算，如剛開始的輸入


### 多種驗證方式

將多種驗證方向組合在一起使用的原因會是：
- 利用各種驗證方向所擁有的利與弊來互補


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
[[React]]
Links:
[[React：表格製作的難點為格本身具有較多狀態要管理，主要有validity和value以及validity得要考量什麼時候驗證以及如何驗證]]
References: