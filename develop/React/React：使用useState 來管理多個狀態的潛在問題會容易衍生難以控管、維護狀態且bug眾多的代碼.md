## 描述




### 使用useState 來管理多個狀態的潛在問題

#### 多個狀態可大略分成兩種情況：
1. 多個獨立狀態，彼此間沒任何關係
2. 多個獨立狀態，狀態彼此間會改變自己的狀態或者這些狀態皆有關係


#### 第一種潛在問題：多個獨立狀態，彼此間沒任何關係
- 狀態過多，會有難以維護、開發的問題：
	- 案例：1000個狀態就要寫1000行useState來進行

#### 第二種潛在問題：多個獨立狀態，狀態彼此間會改變自己的狀態或者這些狀態皆有關係

- 狀態A依賴另一個狀態B來使用setState(狀態B)更新，但會面臨無法確保狀態B是最新的問題
	- 原因：
		1) 每個狀態的setState一執行到更新狀態之間是有時間差。
		2) 狀態A使用的狀態更新函式setState只能以callback來取得最新的狀態A來更新，無法取得最新狀態B來更新。

#### 總結
- 繼續使用useState 來實現會衍生出 難以控管、維護狀態且bug眾多的代碼



### 案例：使用useState 來管理多個狀態的潛在問題


多個獨立狀態，狀態彼此間會改變自己的狀態或者這些狀態皆有關係。


舉例來說：假如有enteredEmail、emailIsValid這兩個負責儲存兩個不同狀態值的變數，而emailIsValid儲存的狀態值是依據著enteredEmail儲存的狀態值是否包含@來決定的：
- 若有包含@，emailIsValid就會預定更新成true
- 若沒包含@，emailIsValid就會預定更新成false
```
const [enteredEmail, setEnteredEmail] = useState('');
const [emailIsValid, setEmailIsValid] = useState();

const emailChangeHandler = (event) => {
	setEnteredEmail(event.target.value);
};

const validateEmailHandler = () => {
	setEmailIsValid(enteredEmail.includes('@'));
};
```

```
return (
	<input 
	  type='email' 
	  id='email'
	  value={enteredEmail}
	  onChange={emailChangeHandler}
	  onBlur={validateEmailHandler}
	/>
);
```

這會引發一個潛在問題：
- emailIsValid的狀態值會是依賴著另一個狀態值enteredEmail來做決定，而狀態值enteredEmail很有可能因為setState變更狀態的時間差而不會是最新的。
- emailIsValid變更狀態用的函式所支援的callback只會以emailIsValid目前要求的最新狀態來更新，並不能夠以callback形式來取得enteredEmail目前要求的最新狀態值來更新



解法：
將多個狀態合併成一個狀態來管理：如狀態改以物件來儲存enteredEmail, emailIsValid，以此試著進行合併。
```
  const [enteredEmail, setEnteredEmail] = useState('');
  const [emailIsValid, setEmailIsValid] = useState();
```



### 解法：使用useState 來管理多個狀態的潛在問題

解法思路為：
	- 將多個狀態合併成一個大狀態來管理

實現手段為
	- 使用 useReducer 

> useReducer() can be used as a replacement for useState() if you need more powerful state management

## 複習


#🧠 React：多個狀態之間的關係可大略分成哪兩大情況？ ->->-> `多個獨立狀態，彼此間沒任何關係、多個獨立狀態，狀態彼此間會改變自己的狀態或者這些狀態皆有關係`
<!--SR:!2023-07-01,178,250-->

#🧠 React：使用useState 來管理多個狀態的潛在問題是什麼？ ->->-> `多個獨立狀態，彼此間沒任何關係：狀態過多，會有難以維護、開發的問題。 多個獨立狀態，狀態彼此間會改變自己的狀態或者這些狀態皆有關係：面臨無法確保狀態B是最新的問題 `
<!--SR:!2023-11-23,98,230-->

#🧠 React：請舉例說明 **useState在多個獨立狀態，彼此間沒任何關係的情況下** 會有潛在問題 - 會有難以維護、開發的問題 ->->-> `1000個狀態就要寫1000行useState來進行`
<!--SR:!2024-09-03,431,250-->

#🧠 React：請詳細說明 **useState在多個獨立狀態，狀態彼此間會改變自己的狀態或者這些狀態皆有關係的情況下** 會有潛在問題 - 狀態A依賴另一個狀態B來使用setState(狀態B)更新，但會面臨無法確保狀態B是最新的問題 ->->-> `每個狀態的setState一執行到更新狀態之間是有時間差。、狀態A使用的狀態更新函式setState只能以callback來取得最新的狀態A來更新，無法取得最新狀態B來更新。`
<!--SR:!2023-11-12,77,210-->

#🧠 React：使用useState 來管理多個狀態的潛在問題是什麼？（請用一句話來說明) ->->-> `繼續使用useState 來實現會衍生出 難以控管、維護狀態且bug眾多的代碼`
<!--SR:!2023-05-22,149,250-->


#🧠 React：使用useState 來管理多個狀態的潛在問題之解法思路是什麼？->->-> `將多個狀態合併成一個大狀態來管理`
<!--SR:!2023-07-11,183,250-->

#🧠 React：假如有enteredEmail、emailIsValid這兩個負責儲存兩個不同狀態值的變數，而emailIsValid儲存的狀態值是依據著enteredEmail儲存的狀態值是否包含@來決定的，在這裡頭會有什麼潛在問題？![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1663511454/blog/react/state/useReducer/useReducer-background-example_xva8gs.png) ->->-> `- emailIsValid的狀態值會是依賴著另一個狀態值enteredEmail來做決定，而狀態值enteredEmail很有可能因為setState變更狀態的時間差而不會是最新的。 - emailIsValid變更狀態用的函式所支援的callback只會以emailIsValid目前要求的最新狀態來更新，並不能夠以callback形式來取得enteredEmail目前要求的最新狀態值來更新`
<!--SR:!2023-08-17,149,230-->


---
Status: #🌱 
Tags:
[[React]]
Links:
References: