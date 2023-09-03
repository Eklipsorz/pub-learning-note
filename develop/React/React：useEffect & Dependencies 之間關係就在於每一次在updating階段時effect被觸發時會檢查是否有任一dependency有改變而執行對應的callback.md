## 描述



### callback 設定目的


useEffect 的 callback則是定義side effect的內容、cleanup內容

[[瀏覽器發送後端請求，回應之前，會先有預設畫面瀏覽給客戶端來增加使用體驗，而非等到回應才渲染，隨後等到回應到來後，就重新渲染]]
### dependency 設定目的
```
useEffect(callback, dependency)
```
> 由於要在觸發渲染週期的期間內，執行到componentDidMount、componentDidUpdate、componentWillUnmount時所依賴的dependency是有變動，才會觸發side effect

[[@ithomeDay21UseEffect]]
> # **dependencies 是一種效能最佳化，而非邏輯控制**

> 理解「dependencies 是一種效能最佳化手段，而非邏輯控制」是掌握 `useEffect` 相當重要的一環。**它用來告訴 React 何時可以因為依賴的原始資料沒有變化而安全地略過本次 effect 的同步，而並不是用來「指定」effect 在什麼特定的「生命週期」或「商業邏輯條件」下才要執行。**你應該要永遠**誠實地根據真實的資料依賴情況來填寫 dependencies 陣列**，

[[@ithomeDay21UseEffect]]
> `useEffect` 其實並不是一種 function component 生命週期的 API。雖然說它的執行時機確實與 `componentDidMount` 以及 `componentDidUpdate` 類似（不過其實有些微區別），但它被設計的用途並不是讓你在 React 運作的特定時機來執行一個自定義的 callback ，而是有一種明確的指定用途 — **用來將原始資料同步到 React elements 以外的東西上**。並且在理想上**這個 effect 無論隨著 render 重複執行了多少次，你的程式都應該保持同步且正常運作。**

重點：
- Dependencies 設定目的主要為效能最佳化，並非邏輯上控制，換言之，一種資料是否同步到給effect來執行的手段
- 具體效能最佳化手段：減少不必要的effect執行
	- 若為mounting階段會是
		- 執行對應effect
		- 儲存dependency指定的記憶體內容
	- 若為updating階段會是
		- 比對這次dependency指定的內容和上一次儲存的內容是否一致，若不一致就執行effect，然後儲存這次dependency內容；若一致就不執行
- useEffect 通常會為了能將資料同步到render之後的effect來執行，特意將dependency設定成這些資料，這些資料的來源主要都是能代表元件互動並跟著互動而變動的資料：
	- props
	- 狀態
	- 其他能代表互動並跟著互動而變動的資料



### dependency 會設定成props、狀態、互動資料的原因
由於這些useEffect本就是將資料同步到render之後的effect執行，在這裡的資料會是render用上的，而那些資料主要會是由能夠代表元件互動並跟互動而變動的資料


#### 除了效能最佳化以外的作用
1. 單純解決邏輯上控制，比如解決擁有能夠觸發渲染的side effect所引起的無限迴圈問題

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
	- dependency 不需要添加effect內部定義的變數/函式，因為他們本身就無法代表元件的互動狀態，且只有effect執行時才有機會變動
	- dependency 不需要添加effect內部定義的函式之引數，因為他們本身就無法代表元件的互動狀態，且只有effect執行時才有機會變動
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

#🧠 React：useEffect(callback, dependencies) 的callback設定目的->->-> `useEffect 的 callback則是定義side effect的內容、cleanup內容`
<!--SR:!2023-05-04,107,249-->


#🧠 React：useEffect(callback, dependencies) 的dependency設定主要目的 ->->-> `Dependencies 設定目的主要為效能最佳化，並非邏輯上控制，換言之，一種資料是否同步到給effect來執行的手段`
<!--SR:!2023-11-24,230,249-->

#🧠 React useEffect：Dependencies 設定目的主要為效能最佳化，並非邏輯上控制，換言之，一種資料是否同步到給effect來執行的手段，具體手段為何？如何做到效能最佳化？？  ->->-> `減少不必要的effect執行`
<!--SR:!2023-06-23,75,209-->

#🧠 React：Dependencies 設定目的主要為效能最佳化，並非邏輯上控制，換言之，一種資料是否同步到給effect來執行的手段，減少不必要的effect執行的流程會是什麼？ ->->-> `若為mounting階段會是 執行對應effect和儲存dependency指定的記憶體內容；若為updating階段會是- 比對這次dependency指定的內容和上一次儲存的內容是否一致，若不一致就執行effect，然後儲存這次dependency內容；若一致就不執行`
<!--SR:!2024-03-11,207,229-->


#🧠  React：Dependencies 設定目的主要為效能最佳化，並非邏輯上控制，換言之，一種資料是否同步到給effect來執行的手段，那麼dependency會設定什麼？為什麼？(不同反應如何做) ->->-> `  - props - 狀態 - 其他能代表互動並跟著互動而變動的資料，由於想依據資料作出不同的反應`


#🧠  React：Dependencies 設定目的主要為效能最佳化，並非邏輯上控制，換言之，一種資料是否同步到給effect來執行的手段，那麼dependency會設定什麼？為什麼？ ->->-> `  - props - 狀態 - 其他能代表互動並跟著互動而變動的資料，由於想依據資料作出不同的反應`



#🧠 React：Dependencies 設定目的主要為效能最佳化，在這裡會儲存什麼來比對是否能繼續執行？ ->->-> `deps資訊`
<!--SR:!2024-05-24,337,249-->

#🧠 React：Dependencies 設定目的主要為效能最佳化，在mounting階段的話，useEffect會做什麼？？ ->->-> `		- 執行對應effect - 儲存dependency指定的記憶體內容`
<!--SR:!2023-11-11,223,249-->


#🧠 React：Dependencies 設定目的主要為效能最佳化，在updating階段的話，useEffect會做什麼？？ ->->-> `比對這次dependency指定的內容和上一次儲存的內容是否一致，若不一致就執行effect，然後儲存這次dependency內容；若一致就不執行`
<!--SR:!2023-12-12,242,249-->



#🧠 React：Dependencies 設定目的主要為效能最佳化，在mounting階段的話，useEffect會做執行對應effect，為啥會直接做 ->->-> `因為當時沒事先儲存好的deps可以比對`
<!--SR:!2024-03-14,295,249-->


#🧠 React：Dependencies 設定目的主要為效能最佳化，在updating階段的話，useEffect會做比對，按照結果執行對應effect，為啥不能在updating階段直接做effect ->->-> `因為當時有事先儲存好的deps可以比對`
<!--SR:!2024-03-22,301,249-->


#🧠 React：Dependencies 設定目的主要是邏輯上的控制嗎？ 為什麼？->->-> `並不是，具體目的為效能最佳化，根據資料是否變動從而決定是否執行render之後的effect`
<!--SR:!2023-10-21,212,249-->


#🧠 React：Dependencies 設定主要目的是效能最佳化，若排除這目的的話，它還能做什麼？ ->->-> `單純解決邏輯上控制，比如解決擁有能夠觸發渲染的side effect所引起的無限迴圈問題`
<!--SR:!2023-12-13,242,249-->

#🧠 React：Dependencies 設定主要目的是效能最佳化，若排除這目的的話，它還能做單純解決邏輯上控制，舉例來說會是？？ ->->-> `比如解決擁有能夠觸發渲染的side effect所引起的無限迴圈問題`
<!--SR:!2023-05-31,47,229-->

#🧠 React：side effect 通常會應用在運用互動狀態的資訊來渲染特定內容，會需要什麼才能實現？->->-> `這就需要一個表示互動狀態的資訊和一個觸發渲染並根據資訊的手段`
<!--SR:!2023-05-29,50,229-->


#🧠 React：通常會為了讓side effect也能夠運用互動狀態的資訊來渲染特定內容，這就需要一個表示互動狀態的資訊和一個觸發渲染並根據資訊的手段，具體會將dependency設定什麼？(什麼東西能表示互動？) ->->-> `- props - 狀態 - 能代表互動並跟著互動而變動的資料`
<!--SR:!2023-10-06,203,249-->


#🧠 React：通常會為了讓side effect也能夠運用互動狀態的資訊來渲染特定內容，這就需要一個表示互動狀態的資訊和一個觸發渲染並根據資訊的手段，具體會將dependency設定什麼？ ->->-> `- props - 狀態 - 能代表互動並跟著互動而變動的資料`
<!--SR:!2023-10-12,206,249-->


#🧠 React：side effect 通常會應用在運用互動狀態的資訊來渲染特定內容，而表示互動狀態的資訊會是指什麼？ ->->-> `能代表互動並跟著互動而變動的資料`
<!--SR:!2023-11-25,201,230-->

#🧠 React：side effect 通常會應用在運用互動狀態的資訊來渲染特定內容，互動狀態的資訊會是指資訊會因為與使用者或者元件進行互動而有所不同，那麼能夠代表互動且跟著互動而變動的資料搭載在dependency，能使side effect有什麼樣的功能？ ->->-> `促使effect 的 callback會因為狀態的改變而跟著渲染出不同的畫面`
<!--SR:!2025-01-16,518,250-->


#🧠 React： 若useEffect 想運用互動狀態的資訊來渲染特定內容，這就需要一個表示互動狀態的資訊和一個觸發渲染並根據資訊的手段，那麼dependency 不需要添加的部分，主要會是什麼？->->-> `主要會是不能夠代表互動狀態的資訊`
<!--SR:!2023-09-30,200,230-->

#🧠 React： 若useEffect 想運用互動狀態的資訊來渲染特定內容那麼dependency 不需要添加的部分，主要會是不能夠代表互動狀態的資訊，那麼內容具體是什麼？ ->->-> `更新狀態用的函式、其他非React能夠支援的API 或者對應函式、屬於其他元件或者元件以外的變數/函式`
<!--SR:!2025-02-07,530,250-->

#🧠 React： 若useEffect 想運用互動狀態的資訊來渲染特定內容，那麼dependency可以添加更新狀態用的函式嗎？為什麼 ->->-> `不建議，因為更新狀態用的函式本身就不會被改變，且無法代表目前元件的互動狀態`
<!--SR:!2025-01-30,532,250-->

#🧠 React： 若useEffect 想運用互動狀態的資訊來渲染特定內容，那麼dependency可以添加非React能夠支援的API 或者對應函式嗎？為什麼  ->->-> `不建議，因爲它們本身不會改變，且無法代表目前元件的互動狀態`
<!--SR:!2024-08-22,427,250-->

#🧠 React： 若useEffect 想運用互動狀態的資訊來渲染特定內容，那麼dependency可以添加effect內部定義的變數/函式嗎？為什麼 ->->-> `因為他們本身就無法代表元件的互動狀態，且只有effect執行時才有機會變動`
<!--SR:!2023-12-13,100,230-->

#🧠 React：useEffect的deps設定中，哪些是不建議添加的？ ->->-> `更新狀態用的函式、其他非React能夠支援的API 或者對應函式、屬於其他元件或者元件以外的變數/函式、添加effect內部定義的變數/函式、effect內部定義的函式之引數`
<!--SR:!2023-10-26,197,230-->

#🧠 React： 若useEffect 想運用互動狀態的資訊來渲染特定內容，那麼dependency可以添加effect內部定義的函式之引數嗎？為什麼 ->->-> `因為他們本身就無法代表元件的互動狀態，且只有effect執行時才有機會變動`
<!--SR:!2023-12-03,98,230-->

#🧠 React： 若useEffect 想運用互動狀態的資訊來渲染特定內容，那麼dependency可以添加屬於其他元件或者元件以外的變數/函式嗎？為什麼  ->->-> `不建議，他們本身一改變就無法代表目前元件的互動狀態。`
<!--SR:!2025-01-17,521,250-->

#🧠 React：請問timerIsActive、timerDuration、setTimerIsActive、myTimer、setTimeout 可不可以放到dependency裡頭，為什麼？ ![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1663256225/blog/react/effect/react-use-effect-dependency-example_q3poat.png) ->->-> `- timerIsActive 本身是狀態，狀態本身只要更新就觸發更新和渲染而進入渲染週期，也就可以觸發useEffect，所以可以加入至dependency - timerDuration 本身是props的值，只要parent元件給定的資訊一改變，其元件就會跟著渲染而進入渲染週期，也就可以觸發useEffect，所以可以加入至dependency - setTimerIsActive 本身是狀態更新用的函式，就不會改變，無法代表目前元件的互動狀態，所以可以不用加入至dependency - myTimer 本身是元件外的變數，它的改變沒辦法代表目前元件的互動狀態，所以可以不用加入至dependency - setTimeOut 本身是非React的API，獨立於React，無法代表目前元件的互動狀態，所以不用加入dependency
<!--SR:!2023-07-08,182,250-->



---
Status: #🌱 
Tags:
[[React]] - [[useEffect]]
Links:
[[React：useEffect 使用方式是替當前元件註冊effect這個hook並於每個渲染階段下來判定是否能執行side effect]]
[[React：Effect 等同於 Side Effect，effect 本身是指執行主要處理(結果)所帶來的任意額外處理(結果)，主要處理(結果)會是指元件渲染(render)任務。任意額外處理(結果)指useEffect所定義的執行處理]]
[[瀏覽器發送後端請求，回應之前，會先有預設畫面瀏覽給客戶端來增加使用體驗，而非等到回應才渲染，隨後等到回應到來後，就重新渲染]]
References:
[[@academindReactcompleteguidecodeButtonModule]]