## 描述



### callback 設定目的


在常見的開發中，useEffect 通常會是產生出觸發渲染週期的side effect，而callback則是定義side effect的內容。

[[瀏覽器發送後端請求，回應之前，會先有預設畫面瀏覽給客戶端來增加使用體驗，而非等到回應才渲染，隨後等到回應到來後，就重新渲染]]
### dependency 設定目的
```
useEffect(callback, dependency)
```
> 由於要在觸發渲染週期的期間內，執行到componentDidMount、componentDidUpdate、componentWillUnmount時所依賴的dependency是有變動，才會觸發side effect

1. 決定能否在每次觸發effect並執行side effect的因素
2. 給予一個手段來防止effect的觸發執行於每次元件的渲染週期內不會產生出無限循環


通常會為了讓side effect也能夠運用互動狀態的資訊來渲染特定內容，這就需要一個表示互動狀態的資訊和一個觸發渲染並根據資訊的手段，而將dependency設定為能代表互動並跟著互動而變動的資料：
- props
- 狀態
- 其他能代表互動並跟著互動而變動的資料


#### 其他能代表互動並跟著互動而變動的資料？？
其他能代表互動並跟著變動的資料通常會因為與使用者或者元件進行互動而有所不同，而這剛好可以促使effect 的 callback會因為狀態的改變而跟著渲染出不同的畫面




### dependency 設定的注意事項
[[@academindReactcompleteguidecodeButtonModule]]
> You learned, that you should add "everything" you use in the effect function as a dependency - i.e. all state variables and functions you use in there.
>
> That is correct, but there are a **few exceptions** you should be aware of:

> -   You **DON'T need to add state updating functions** (as we did in the last lecture with `setFormIsValid`): React guarantees that those functions never change, hence you don't need to add them as dependencies (you could though)
    
> -   You also **DON'T need to add "built-in" APIs or functions** like `fetch()`, `localStorage` etc (functions and features built-into the browser and hence available globally): These browser APIs / global functions are not related to the React component render cycle and they also never change
    
> -   You also **DON'T need to add variables or functions** you might've **defined OUTSIDE of your components** (e.g. if you create a new helper function in a separate file): Such functions or variables also are not created inside of a component function and hence changing them won't affect your components (components won't be re-evaluated if such variables or functions change and vice-versa)


> So long story short: You must add all "things" you use in your effect function **if those "things" could change because your component (or some parent component) re-rendered.** That's why variables or state defined in component functions, props or functions defined in component functions have to be added as dependencies!


side effect也能夠運用props、狀態、其他還能觸發渲染週期的資料來根據資訊的不同來渲染

重點：
- 若useEffect 想運用互動狀態的資訊來渲染特定內容，這就需要一個表示互動狀態的資訊和一個觸發渲染並根據資訊的手段，那麼dependency 不需要添加的部分，主要會是不能夠代表能代表互動並跟著變動的資料：
	- dependency 不需要添加更新狀態用的函式：因為React本身和使用者本身就不會變動該函式本身，且無法代表目前元件的互動狀態
	- dependency 不要添加其他非React能夠支援的API 或者對應函式：因為他們本身就不會改變，且無法代表目前元件的互動狀態
	- dependency 不要添加屬於其他元件或者元件以外的變數/函式，因為它們本身就屬於其他元件或者非元件，它們一改變這件事本身就無法代表目前元件的互動狀態。
- 若useEffect 想運用互動狀態的資訊來渲染特定內容，這就需要一個表示互動狀態的資訊和一個觸發渲染並根據資訊的手段，那麼dependency 需要添加的部分：
	- props、狀態、其他能代表互動並跟著變動的資料


### 案例：denpendency 設定細節

```
    import { useEffect, useState } from 'react';
     
    let myTimer;
     
    const MyComponent = (props) => {
      const [timerIsActive, setTimerIsActive] = useState(false);
	  // using destructuring to pull out specific props values
      const { timerDuration } = props; 
     
      useEffect(() => {
        if (!timerIsActive) {
          setTimerIsActive(true);
          myTimer = setTimeout(() => {
            setTimerIsActive(false);
          }, timerDuration);
        }
      }, [timerIsActive, timerDuration]);
    };
```



>In this example:
>
> -   `timerIsActive` is **added as a dependency** because it's component state that may change when the component changes (e.g. because the state was updated)
>    
>-   `timerDuration` is **added as a dependency** because it's a prop value of that component - so it may change if a parent component changes that value (causing this MyComponent component to re-render as well)
 >   
>-   `setTimerIsActive` is **NOT added as a dependency** because it's that **exception**: State updating functions could be added but don't have to be added since React guarantees that the functions themselves never change
 >   
>-   `myTimer` is **NOT added as a dependency** because it's **not a component-internal variable** (i.e. not some state or a prop value) - it's defined outside of the component and changing it (no matter where) **wouldn't cause the component to be re-evaluated**
>    
>-   `setTimeout` is **NOT added as a dependency** because it's **a built-in API** (built-into the browser) - it's independent from React and your components, it doesn't change


重點：
- timerIsActive 本身是狀態，狀態本身只要更新就觸發更新和渲染而進入渲染週期，也就可以觸發useEffect，所以可以加入至dependency
- timerDuration 本身是props的值，只要parent元件給定的資訊一改變，其元件就會跟著渲染而進入渲染週期，也就可以觸發useEffect，所以可以加入至dependency
- setTimerIsActive 本身是狀態更新用的函式，就不會改變，無法代表目前元件的互動狀態，所以可以不用加入至dependency
- myTimer 本身是元件外的變數，它的改變沒辦法代表目前元件的互動狀態，所以可以不用加入至dependency
- setTimeOut 本身是非React的API，獨立於React，無法代表目前元件的互動狀態，所以不用加入dependency

## 複習

#🧠 React：useEffect(callback, dependencies) 的callback設定目的->->-> `callback則是定義side effect的內容。`
<!--SR:!2022-09-29,10,250-->

#🧠 React：useEffect(callback, dependencies) 的dependency設定目的 ->->-> `決定能否在每次觸發effect並執行side effect的因素、給予一個手段來防止effect的觸發執行於每次元件的渲染週期內不會產生出無限循環`
<!--SR:!2022-10-14,18,250-->


#🧠 React：side effect 通常會應用在運用互動狀態的資訊來渲染特定內容，會需要什麼才能實現？->->-> `這就需要一個表示互動狀態的資訊和一個觸發渲染並根據資訊的手段`
<!--SR:!2022-09-29,10,250-->

#🧠 React：通常會為了讓side effect也能夠運用互動狀態的資訊來渲染特定內容，這就需要一個表示互動狀態的資訊和一個觸發渲染並根據資訊的手段，而將dependency設定什麼？ ->->-> `- props - 狀態 - 能代表互動並跟著互動而變動的資料`
<!--SR:!2022-09-29,10,250-->

#🧠 React：side effect 通常會應用在運用互動狀態的資訊來渲染特定內容，而表示互動狀態的資訊會是指什麼？ ->->-> `能代表互動並跟著互動而變動的資料`
<!--SR:!2022-10-24,26,250-->

#🧠 React：side effect 通常會應用在運用互動狀態的資訊來渲染特定內容，互動狀態的資訊會是指資訊會因為與使用者或者元件進行互動而有所不同，那麼能夠代表互動且跟著互動而變動的資料搭載在dependency，能使side effect有什麼樣的功能？ ->->-> `促使effect 的 callback會因為狀態的改變而跟著渲染出不同的畫面`
<!--SR:!2022-10-03,10,250-->


#🧠 React： 若useEffect 想運用互動狀態的資訊來渲染特定內容，這就需要一個表示互動狀態的資訊和一個觸發渲染並根據資訊的手段，那麼dependency 不需要添加的部分，主要會是什麼？->->-> `主要會是不能夠代表互動狀態的資訊`
<!--SR:!2022-09-29,10,250-->

#🧠 React： 若useEffect 想運用互動狀態的資訊來渲染特定內容那麼dependency 不需要添加的部分，主要會是不能夠代表互動狀態的資訊，那麼內容具體是什麼？ ->->-> `更新狀態用的函式、其他非React能夠支援的API 或者對應函式、屬於其他元件或者元件以外的變數/函式`
<!--SR:!2022-09-29,10,250-->

#🧠 React： 若useEffect 想運用互動狀態的資訊來渲染特定內容，那麼dependency可以添加更新狀態用的函式嗎？為什麼 ->->-> `不建議，因為更新狀態用的函式本身就不會被改變，且無法代表目前元件的互動狀態`
<!--SR:!2022-09-29,10,250-->

#🧠 React： 若useEffect 想運用互動狀態的資訊來渲染特定內容，那麼dependency可以添加非React能夠支援的API 或者對應函式嗎？為什麼  ->->-> `不建議，因爲它們本身不會改變，且無法代表目前元件的互動狀態`
<!--SR:!2022-09-28,9,250-->

#🧠 React： 若useEffect 想運用互動狀態的資訊來渲染特定內容，那麼dependency可以添加屬於其他元件或者元件以外的變數/函式嗎？為什麼  ->->-> `不建議，他們本身一改變就無法代表目前元件的互動狀態。`
<!--SR:!2022-09-29,10,250-->

#🧠 React：請問timerIsActive、timerDuration、setTimerIsActive、myTimer、setTimeout 可不可以放到dependency裡頭，為什麼？ ![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1663256225/blog/react/effect/react-use-effect-dependency-example_q3poat.png) ->->-> `- timerIsActive 本身是狀態，狀態本身只要更新就觸發更新和渲染而進入渲染週期，也就可以觸發useEffect，所以可以加入至dependency - timerDuration 本身是props的值，只要parent元件給定的資訊一改變，其元件就會跟著渲染而進入渲染週期，也就可以觸發useEffect，所以可以加入至dependency - setTimerIsActive 本身是狀態更新用的函式，就不會改變，無法代表目前元件的互動狀態，所以可以不用加入至dependency - myTimer 本身是元件外的變數，它的改變沒辦法代表目前元件的互動狀態，所以可以不用加入至dependency - setTimeOut 本身是非React的API，獨立於React，無法代表目前元件的互動狀態，所以不用加入dependency
<!--SR:!2022-09-29,10,250-->



---
Status: #🌱 
Tags:
[[React]]
Links:
[[React：useEffect 使用方式是替當前元件註冊effect這個hook並於每個渲染階段下來判定是否能執行對應的callback]]
[[React：effect 是指除了元件本身所要做的主要功能-渲染元件、與使用者互動來管理狀態以外的額外效果，額外效果會是指脫離渲染週期的任意功能]]
[[瀏覽器發送後端請求，回應之前，會先有預設畫面瀏覽給客戶端來增加使用體驗，而非等到回應才渲染，隨後等到回應到來後，就重新渲染]]
References:
[[@academindReactcompleteguidecodeButtonModule]]