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


useReducer 所回傳的狀態會由useReducer(reducer, init, initFn)中的reducer、初始狀態 init、給定初始狀態的函式 initFn的reducer所決定，通常前者函式主要會依據著dispatch給定的action來決定下一個新狀態是什麼？
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
- 當針對需要關注的狀態來觸發的話：整個狀態下的所有子狀態只要透過dispatch來改變狀態，那麼每個子狀態都能夠觸發side effect，而不是針對需要關注的狀態來觸發，這會造成不必要的效能浪費

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
<!--SR:!2023-07-14,185,250-->

#🧠  React 的 useReducer 是如何歸納多個狀態為一個結果狀態的？ ->->-> `通常使用useReducer將原本從useState所註冊的多個獨立狀態組合成一個物件，其物件屬性名稱和屬性值會是這些獨立狀態名稱和獨立狀態值。`
<!--SR:!2023-07-03,178,250-->

#🧠 useReducer 所回傳的狀態是由誰負責的？ ->->-> `useReducer(reducer, init, initFn)中的reducer、init、initFn`
<!--SR:!2023-05-09,24,190-->

#🧠 useReducer 所回傳的狀態在渲染週期是如何回傳新狀態作為snapshot，假設只有useReducer這個狀態管理工具 ->->-> `mounting 階段下的componentDidMount來以init或者initFn來給定，而updating階段則是以componentDidUpdate來以reducer回傳的新狀態為主。`
<!--SR:!2023-05-07,139,250-->

#🧠 通常使用useReducer將原本從useState所註冊的多個獨立狀態組合成一個物件，其物件屬性名稱和屬性值會是這些獨立狀態名稱和獨立狀態值，那麼reducer會如何以程式碼實現狀態更新 ->->-> `reducer會根據dispatch給定action資訊來決定狀態如何更新，而程式碼會是![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1663592245/blog/react/state/useReducer/useReducer-simple-usage_z2yho4.png)`
<!--SR:!2023-12-04,99,230-->

#🧠 若以useReducer 所回傳的狀態為useEffect 的 dependency，請問可以如何運用useReducer的歸納關係來使用(部分狀態、整個狀態)->->-> `1. 使用useReducer的整個狀態來做為useEffect 的執行依據、2. 使用useReducer能回傳完整狀態的一部分`
<!--SR:!2023-07-25,190,250-->


#🧠 若以useReducer 所回傳的狀態為useEffect 的 dependency，請問可以如何運用useReducer的歸納關係來使用->->-> `1. 使用useReducer的整個狀態來做為useEffect 的執行依據、2. 使用useReducer能回傳完整狀態的一部分`
<!--SR:!2023-05-27,149,250-->

#🧠 若以useReducer回傳的整份狀態作為useEffect的dependency，會有什麼潛在問題？ ->->-> `當針對需要關注的狀態來觸發的話：整個狀態下的所有子狀態只要透過dispatch來改變狀態，那麼每個子狀態都能夠觸發side effect，而不是針對需要關注的狀態來觸發，這會造成不必要的效能浪費`
<!--SR:!2023-07-25,193,250-->

#🧠 假設emailState、passwordState是分別從兩個useReducer所註冊的狀態，emailState狀態包含了email和validity，而passwordState狀態包含了password和validity，請問若下列useEffect原本只針對validity，會有什麼潛在問題？解法是什麼？![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1663592888/blog/react/state/useReducer/useReducer-question-example_tcgacn.png) ->->-> `- 每一次email輸入欄位或者password輸入欄位有變動就會觸發執行effect -  實際上來說只想關注在輸入欄位上的validity是否有變動`
<!--SR:!2023-11-19,94,230-->

#🧠 若以useReducer回傳的整份狀態作為useEffect的dependency，潛在問題為無法針對需要關注的狀態來觸發，只會每個子狀態觸發就執行，請問如何解決？具體程式碼會是如何？->->-> `若以useReducer回傳的部分狀態的話，useEffect(() => { // do something setState(...) or dispatch(....) }, [state.property1])、const [state, dispatch] = useReducer(reducer, init) const {property1: stateProperty1} = state useEffect(() => { // do something setState(...) or dispatch(....) }, [stateProperty1])`
<!--SR:!2025-01-13,515,250-->

#🧠 若以useReducer回傳的部分狀態的話，對於狀態處理效能會有什麼好處？ ->->-> `讓useEffect只針對著需要關注的狀態來做處理，繼而減少不必要的狀態處理。`
<!--SR:!2023-09-20,171,230-->





---
Status: #🌱 
Tags:
[[React]] - [[useEffect]]
Links:
[[React：useReducer 是React 內建的HOOK，最主要是以多個狀態歸納成一個大狀態 的方式來控管狀態]]
[[React：使用useState 來管理多個狀態的潛在問題會容易衍生難以控管、維護狀態且bug眾多的代碼]]
References: