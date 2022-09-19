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


useReducer 所回傳的狀態會由useReducer(reducer,..) 的reducer所決定，通常該函式主要會依據著dispatch給定的action來決定下一個新狀態是什麼？
1. 通常會是配給一個新記憶體來建立物件
2. 物件屬性仍會以原有useState所註冊的狀態來組合
3. 將分派屬性完畢的新物件用來觸發渲染週期以及做為下一次snapshot的依據

形式會是如下：
```
function reducer(state, action) {
  switch (action.type) {
    case 'A':
      newState = { state1:..., state2:....,... };
      break;
    case 'B':
      newState = { state1:..., state2:....,... };
      break;
    default:
      throw new Error();
  }
  
  return newState;
}
```



```
const [state, dispatch] = useReducer(reducer, init)
```
這樣會每次從useReducer獲取到的snapshot會是以搭載新狀態的新物件。
```
{
	state1:....,
	state2:....,
	.
	.
}
```


### 使用useReducer的狀態來做為useEffect 的執行依據


#### 若以useReducer回傳的整份狀態的話

> But you should **avoid** this code:
```
1.  useEffect(() => {
2.    // code that only uses someProperty ...
3.  }, [someObject]);
```

> Why?
>
> Because now the **effect function would re-run whenever ANY property** of `someObject` changes - not just the one property (`someProperty` in the above example) our effect might depend on.



```
const [state, dispatch] = useReducer(reducer, init)

useEffect(() => {
	// do something
	setState(...) or dispatch(....)
}, [state])
```


會有的潛在問題：
- 整個狀態下的所有子狀態只要透過dispatch來改變狀態，那麼每個子狀態都能夠觸發side effect，而不是針對需要關注的狀態來觸發，這會造成不必要的效能浪費

##### 案例：若以useReducer回傳的整份狀態的話
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
11.  }, [emailState, passwordState]);
```


潛在問題：
- 每一次email輸入欄位或者password輸入欄位有變動就會觸發執行effect
-  實際上來說只想關注在輸入欄位上的validity是否有變動


#### 若以useReducer回傳的部分狀態的話

> In the previous lecture, we used object destructuring to add object properties as dependencies to `useEffect()`.

```
1.  const { someProperty } = someObject;
2.  useEffect(() => {
3.    // code that only uses someProperty ...
4.  }, [someProperty]);
```

> This is a **very common pattern and approach**, which is why I typically use it and why I show it here (I will keep on using it throughout the course).
>
> I just want to point out, that they **key thing is NOT that we use destructuring** but that we **pass specific properties instead of the entire object** as a dependency.
>
> We could also write this code and it would **work in the same way**.


```
1.  useEffect(() => {
2.    // code that only uses someProperty ...
3.  }, [someObject.someProperty]);
```
> This works just fine as well!

由於state的屬性就是原本useState註冊的子屬性，所以若要以特定狀態property1來觸發effect的話，那麼只需要從state這snapshot取出property1的狀態來讓useEffect去監測。

```
/* first way */
const [state, dispatch] = useReducer(reducer, init)

useEffect(() => {
	// do something
	setState(...) or dispatch(....)
}, [state.property1])

/* second way */
const [state, dispatch] = useReducer(reducer, init)

const {property1: stateProperty1} = state

useEffect(() => {
	// do something
	setState(...) or dispatch(....)
}, [stateProperty1])
```

這樣得到的好處是：
- 讓useEffect只針對著需要關注的狀態來做處理，繼而減少不必要的狀態處理。




#### 案例：若以useReducer回傳的部分狀態的話

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
#🧠 React 的 useReducer 所歸納的狀態通常會是什麼結果形式？歸納前又是什麼形式 ->->-> `歸納後 { state1: value1, state2: value2, state3: value3,... } 歸納前： state1 = value1 state2 = value2 state3 = value3 ....`

#🧠 Question :: ->->-> ``

#🧠 Question :: ->->-> ``

#🧠 Question :: ->->-> ``

#💻 Question :: ->->-> ``

---
Status: #🌱 #📓 
Tags:
[[React]]
Links:
[[React：useReducer 是React 內建的HOOK，最主要是以多個狀態歸納成一個大狀態 的方式來控管狀態]]
[[React：使用useState 來管理多個狀態的潛在問題會容易衍生難以控管、維護狀態且bug眾多的代碼]]
References: