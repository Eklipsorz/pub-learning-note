## 描述


### 官方準則
> there are two main rules you have to know when it comes to working with react hooks

> 1. where you are allowed to use react hooks：you must only call react hooks in react functions (function component/react component function) or also allowed in custom hooks

> 2. you must only call react hooks at the top level of your react component functions or your custom hook functions：
 >  - don't call them in nested functions
>   - don't call them in any block statements

  
重點：
- react hook functions的官方準則
	- 哪裏可以允許使用hook：只能在react functions(function component/react componet function) 或者 custom hook function 才能調用hook function
	- 在允許函式下的哪個區塊能用：
		- 只能在componet function或者custom hook function的最一開始執行的地方才能呼叫hook
		- 不能在巢狀函式結構下呼叫 hook function
		- 不能在block scope下呼叫 hook function



#### 錯誤案例：第一準則

第一個規則的錯誤案例：在這裏是在component function以外的地方呼叫hook function
```
1.  function xxx() {
2.      useEffect()
3.  }
4. 
5.  function Component(props) {
6.      // ....
7.  }
```



#### 錯誤案例：第二準則

第二個規則的錯誤案例：在這裏是在巢狀函式結構下呼叫hook function
```
1.  function Component(props) {
2.      useEffect(() => {
3.          useEffect(callback)
4.      })
5.  }
```

  以及在block scope下呼叫hook function
```
1.  function Component(props) {
2.      if (...) {
3.          useEffect(callback)
4.      }
5.  }
```


### 非官方準則

> third rule：not directly related to all hooks, but to one specific hook.

> useEffect：make sure that you always add everything you refer to inside of use effect as a dependency unless there is a good reason not to do that


重點：
- 該準則適用於useEffect
- 確保你總是以effect內部使用的東西做為dependency，除非你有特別需求，在這裏系統會預判哪些內部內容是得添加至dependency，通常第三方API、元件外的變數是可允許不被添加


#### 錯誤案例：

比如原本要將比較添加的emailIsValid 和 passwordIsValid 原本納入至dependency，但只有添加emailIsValid
```
1.    useEffect(() => {
2.      const identifier = setTimeout(() => {
3.        console.log('Checking form validity!');
4.        setFormIsValid(emailIsValid && passwordIsValid);
5.      }, 500);

7.      return () => {
8.        console.log('CLEANUP');
9.        clearTimeout(identifier);
10.      };
11.    }, [emailIsValid]);
```



### top level 命名緣由
[[@pythonMainToplevelCode]]
> “Top-level code” is the first user-specified Python module that starts running. It’s “top-level” because it imports all other modules that the program needs. Sometimes “top-level code” is called an _entry point_ to the application.

重點：
- top-level 會是指應用程式最一開始進入執行的地方或者函式最一開始進入執行的地方

## 複習

#🧠 react hook functions的官方準則主要定義了哪裏可以允許使用hook、 在允許函式下的哪個區塊能用，請問具體會是什麼？ ->->-> `哪裏可以允許使用hook：只能react functions(function component/react componet function) 或者 custom hook function 才能調用hook function、在允許函式下的哪個區塊能用：只能在componet function或者custom hook function的最一開始執行的地方才能呼叫hook`
<!--SR:!2022-10-30,24,250-->

#🧠 react hook functions的官方準則大致上分為哪兩種 ->->-> `哪裏可以允許使用hook、 在允許函式下的哪個區塊能用`
<!--SR:!2022-11-03,28,250-->

#🧠 react hook functions的官方準則主要定義了在允許函式下的哪個區塊能用，請問在允許函式下哪些地方是不能呼叫hook->->-> `	- 不能在巢狀函式結構下呼叫 hook function - 不能在block scope下呼叫 hook function`
<!--SR:!2022-10-23,20,250-->

#🧠 react hook functions ：除了官方那兩大準則以外，還有非官方準則適用於useEffect，具體是什麼？ ->->-> `確保你總是以effect內部使用的東西做為dependency`
<!--SR:!2022-10-24,20,250-->

#🧠 react hook functions ：除了官方那兩大準則以外，還有非官方準則適用於useEffect，具體是確保你總是以effect內部使用的東西做為dependency，系統如何判定？->->-> `在這裏系統會預判哪些內部內容是得添加至dependency，通常第三方API、元件外的變數是可允許不被添加`
<!--SR:!2022-10-06,10,250-->

#🧠 React：對於使用hook的第一準則而言，只能在react functions(function component/react componet function) 或者 custom hook function 才能調用hook function，請舉一個錯誤案例 ->->-> `![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1663873168/blog/react/hook/principle/wrong-case-block-scope-with-hook_fzb7bf.png)`
<!--SR:!2022-11-03,28,250-->

#🧠 React：對於使用hook的第二準則而言，只能在componet function或者custom hook function的最一開始執行的地方才能呼叫hook，請舉一個錯誤案例 ->->-> `![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1663873168/blog/react/hook/principle/wrong-case-nest-function-with-hook_wpuzh0.png)`
<!--SR:!2022-11-03,28,250-->

#🧠 React：對於使用hook的第三準則而言，確保你總是以effect內部使用的東西做為dependency，請舉一個錯誤案例 ->->-> `![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1663873168/blog/react/hook/principle/wrong-case-dependency-effect_wetmfo.png)`
<!--SR:!2022-11-03,28,250-->


---
Status: #🌱 
Tags:
[[React]]
Links:
References:
[[@pythonMainToplevelCode]]