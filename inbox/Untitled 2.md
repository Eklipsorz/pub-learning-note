## 描述


### 官方規則
> there are two main rules you have to know when it comes to working with react hooks

> 1. where you are allowed to use react hooks：you must only call react hooks in react functions (function component/react component function) or also allowed in custom hooks

> 2. you must only call react hooks at the top level of your react component functions or your custom hook functions：
 >  - don't call them in nested functions
>   - don't call them in any block statements

  


第一個規則的錯誤案例
```
1.  function xxx() {
2.      useEffect()
3.  }
4.  function Component(props) {
5.      // ....
6.  }
```




第二個規則的錯誤案例


```
1.  function Component(props) {
2.      useEffect(() => {
3.          useEffect(callback)
4.      })
5.  }
```

  


```
1.  function Component(props) {
2.      if (...) {
3.          useEffect(callback)
4.      }
5.  }
```



top-level 意指為function內部的最外圍的scope


## 複習


---
Status: #🌱 #📓 
Tags:
[[React]]
Links:
References: