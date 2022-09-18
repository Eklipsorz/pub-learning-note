## 描述





### useReducer 的狀態組成

通常使用useReducer將原本從useState所註冊的多個獨立狀態組合成一個物件，其物件屬性名稱和屬性值會是這些獨立狀態名稱和獨立狀態值。

比如說以下由useState所註冊的狀態變數
```
state1 = value1
state2 = value2
state3 = value3
.
.
```

經過useReducer轉換就變成：
```
{
	state1: value1,
	state2: value2,
	state3: value3,
	.
	.
}
```


### useReducer 所回傳的狀態
[[React：useReducer 是React 內建的HOOK，最主要是以多個狀態歸納成一個大狀態 的方式來控管狀態]]


useReducer 所回傳的狀態會由useReducer(reducer,..) 的reducer所決定，通常該函式主要會依據著dispatch給定的action來決定下一個新狀態是什麼？通常會是配給一個新記憶體來建立物件，物件屬性仍會以原有useState所註冊的狀態來組合。

```
function reducer(state, action) {
  let newState;
  switch (action.type) {
    case 'increase':
      newState = { counter: state.counter + 1 };
      break;
    case 'descrease':
      newState = { counter: state.counter - 1 };
      break;
    default:
      throw new Error();
  }
  return newState;
}
```


### 使用useReducer的狀態來做為useEffect 的執行依據



the effect runs too often


```
1.  useEffect(() => {
2.      const identifier = setTimeout(() => {
3.          console.log('Checking form validity!');
4.          setFormIsValid(......);
5.      }, 500);

7.      return () => {
8.          console.log('CLEANUP');
9.          clearTimeout(identifier);
10.      };
11.  },[emailState, passwordState]);
```


潛在問題：
- 每一次email輸入欄位或者password輸入欄位有變動就會觸發執行effect


實際上來說只想關注在輸入欄位上的validity是否有變動

  
解法為從eamilState、passwordState取出validity 的部分作為變動的基礎


```
1.  const {isValid: emailIsValid} = eamilState;
2.  const {isValid: passwordIsValid} = passwordState;

4.  useEffect(() => {
5.      const identifier = setTimeout(() => {
6.          console.log('Checking form validity!');
7.          setFormIsValid(emailIsValid && passwordIsValid);
8.      }, 500);

10.      return () => {
11.          console.log('CLEANUP');
12.          clearTimeout(identifier);
13.      };
14.  },[emailIsValid, passwordIsValid]);
```
  
好處：
- 減少大量不必要的處理，集中在email和password的合法性是否變動


## 複習


---
Status: #🌱 #📓 
Tags:
[[React]]
Links:
[[React：useReducer 是React 內建的HOOK，最主要是以多個狀態歸納成一個大狀態 的方式來控管狀態]]
[[React：使用useState 來管理多個狀態的潛在問題會容易衍生難以控管、維護狀態且bug眾多的代碼]]
References: