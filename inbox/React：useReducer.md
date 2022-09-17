## 描述

useReducer：
1. React 內建的HOOK
2. 用作於狀態管理(與useState相似，但比較多功能來處理較為複雜狀態)


> sometimes, you have more complex state - for example if it got multiple states, multiple ways of changing it or dependencies to other states


multiple states that kind of belong together, that are managing the same thing, just different aspects of it

比如實際上有多個狀態B可以組裝成一個狀態A，只是分離從龐大的狀態A分離成好幾個狀態B

  

  

多個狀態＋這些狀態原本從一個大狀態分離出來 ，舉例：一個表單狀態本身可以按照輸入欄位的多寡而區分成好幾個狀態

```
const [enteredEmail, setEnteredEmail] = useState('');
const [emailIsValid, setEmailIsValid] = useState();
const [enteredPassword, setEnteredPassword] = useState('');
const [passwordIsValid, setPasswordIsValid] = useState();
const [formIsValid, setFormIsValid] = useState(false);
```



多個狀態＋這些狀態彼此改變自己的狀態，舉例：狀態A的改變會間接促使改變狀態B，而狀態B的改變會促使狀態A的改變。

多個狀態＋這些狀態彼此皆有關係



### 繼續使用useState的潛在問題
多個狀態＋這些狀態原本從一個大狀態分離出來

多個狀態＋這些狀態彼此改變自己的狀態

多個狀態＋這些狀態彼此皆有關係

  

繼續使用useState 來實現會衍生出 難以控管、維護狀態且bug眾多的代碼

#### 替代方案

會改用useReducer 來解決這複雜狀態的問題

useReducer() can be used as a replacement for useState() if you need more powerful state management

### reduce / reduction
> reduction refers to **the rewriting of an expression into a simpler form**.

重點：
- reduce 是將複雜的事物轉換成單一簡單的事物

## 複習


---
Status: #🌱 #📓 
Tags:
[[React]]
Links:
References: