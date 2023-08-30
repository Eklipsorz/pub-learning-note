### state updating is asynchronous?
[[@dmitripavlutinHowReactUpdates2020]] 
> When you update the component's state, does React update the state _immediately_ (synchronously) or rather _schedules a state update_ (asynchronously)? This post answers this question.


#### example: problem
```
import { useState } from 'react';

function DoubleIncreaser() {

	const [count, setCount] = useState(0);
	const doubleIncreaseHandler = () => {
		setCount(count + 1);
		setCount(count + 1);
	};

	return (
		<>
			<button onClick={doubleIncreaseHandler}>
				Double Increase
			</button>
			<div>Count: {count}</div>
		</>
	);
}
```

> Open the [demo](https://codesandbox.io/s/usestate-broken-ytmxk?file=/src/index.js) and click the button _Double Increase_. The `count` is increased by `1` on each click.

> When `setCount(count + 1)` updates the state, the changes are not reflected immediately in the `count` variable. Rather React _schedules a state update_, and during the next rendering in the statement `const [count, setCount] = useState(0)` the hook assigns to `count` the new state value.

> For instance: if `count` variable is `0`, then calling `setCount(count + 1); setCount(count + 1);` is simply evaluated as `setCount(0 + 1); setCount(0 + 1);` — making the state on next render as `1`.

> The state update function `setValue(newValue)` of `[value, setValue] = useState()` updates the state asynchronously.

重點：
- 從上述案例來看，由於count本身因為以下因素：
	- count只不過是儲存特定狀態值的變數，它一直保持著0這個狀態值
	- 第一次執行setCount(count + 1);，就已經將目標狀態值設定為0 + 1，但由於啟用batching沒先更新count
	```
	setCount(count + 1);
	```
	- 第二次執行，也是拿目前的count = 0來做，而得到0 + 1
	- 最後執行的時候，會是以1這個狀態值來更新，並同時只執行一次狀態更新 & 渲染

- 要依據setCount實際更新的狀態來執行setCount，可以使用callback
	```
	setState(currentStatus)
	setState(newStatus1)
	setState(newStatus2)
	```

	- callback會由React setState 函式內來呼叫的，預設setState會將目前得到的狀態值來當callback的參數使用，其回傳值會成為setState新的狀態值。
	```
	setState(callback)	
	// callback
	function callback (xxx) { 
		return .....
	}
	```
	- 執行順序會是：
		- setState -> newState = callback(currentState) -> handling with newState
	- 若要成為解法的話，只需要設定callback為
	```
	// callback
	(prevState) => (prevState) + 1
	```
#### example: solution 1

> The state update function also accepts a callback to compute new state using the current state. In case of the `DoubleIncreaser`, you can use `setCount(actualCount => actualCount + 1)`:


```
import { useState } from 'react';

function DoubleIncreaser() {

	const [count, setCount] = useState(0);
	
	const doubleIncreaseHandler = () => {
		setCount((actualCount) => actualCount + 1);
		setCount((actualCount) => actualCount + 1);
	};

	return (
		<>
			<button onClick={doubleIncreaseHandler}>Double Increase</button>
			<div>Count: {count}</div>
		</>
	);

}
```

> When updating the state using a function `setCount(actualCount => actualCount + 1)`, then `actualCount` argument contains the actual value of the state.


> Open the [demo](https://codesandbox.io/s/usestate-fixed-callback-e4pp3?file=/src/index.js), and click the _Double Increase_ button. The count updates by `2` as expected.

重點：
- 在這裡改使用callback來當setCount參數，所以新狀態值會是callback的回傳值
- 第一次執行下面時，setCount 會拿目前的狀態值來當作actualCount並進行疊加，而得到1，其1會成為新的目前狀態值
```
setCount((actualCount) => actualCount + 1);
```
- 第二次執行類似語法時，setCount會拿目前的狀態值1來當作actualCount並進行疊加，而得到2，其2會成為新的目前狀態值
- 最後沒setCount等狀態更新指令，就執行目前狀態值2來更新和渲染

#### example: solution 2
> Of course, you can use an intermediate `let` variable:

```
import { useState } from 'react';

function DoubleIncreaser() {

	const [count, setCount] = useState(0);

	const doubleIncrease = () => {
		let actualCount = count;
		actualCount = actualCount + 1;
		actualCount = actualCount + 1;
		
		setCount(actualCount);
	};

	return (
		<>
			<button onClick={this.doubleIncrease}>Double Increase</button>
			<div>Count: {count}</div>
		</>
	);

}
```

> `let actualCount = count` is an intermediate variable that you can update at will. The updated intermediate variable to update the `setCount(actualCount)`.

>  Try the [demo](https://codesandbox.io/s/usestate-fixed-interm-variable-xo3n7?file=/src/index.js) using intermediate variable.


重點：
- 除了callback以外的解法，還可以先做完邏輯計算並將結果設定至setCount來更新狀態

## 複習
#🧠 請問發生按鈕點擊事件後，其狀態會是如何，count渲染又是如何？![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1661184977/blog/react/batching/setCounter/setState-expected-value-problem_zfagua.png) ->->-> `會是1，由於count只不過是儲存特定狀態值的變數，它一直保持著0這個狀態值，count只不過是儲存特定狀態值的變數，它一直保持著0這個狀態值，第二次執行，也是拿目前的count = 0來做，而得到0 + 1，最後執行的時候，會是以1這個狀態值來更新，並同時只執行一次狀態更新 & 渲染`
<!--SR:!2023-06-28,194,250-->


#🧠 執行第一個狀態更新就使0->1，執行第二個狀態更新就使1->2的話來改造下面的話，解法有哪些？![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1661184977/blog/react/batching/setCounter/setState-expected-value-problem_zfagua.png) ->->-> `以callback作為setCount的引數、先處理兩次count疊加的邏輯計算並且以其結果來渲染和更新`
<!--SR:!2024-07-15,418,250-->

#🧠 setState 參數為callback，會是如何進行的？->->-> `預設setState會將目前得到的狀態值來當callback的參數使用，其回傳值會成為setState新的狀態值`
<!--SR:!2023-06-28,194,250-->

#🧠 setState 參數為callback，預設setState會將目前得到的狀態值來當callback的參數使用，其回傳值會成為setState新的狀態值，那麼setState、callback、狀態的執行順序->->-> `setState -> newState = callback(currentState) -> handling with newState`
<!--SR:!2023-12-16,107,230-->

#🧠 若要以下面形式callback作為setCount的參數，來修改以下count狀態更新都必須以1、2來分別修改，那麼要如何修改 ![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1661184977/blog/react/batching/setCounter/setState-expected-value-problem_zfagua.png)->->-> `將setCount的參數都設定為(count) => count + 1`
<!--SR:!2024-06-11,397,250-->


#🧠 請說明當發生點擊事件時，會是如何更新狀態和渲染？![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1661184977/blog/react/batching/setCounter/setState-expected-value-solution_mbe5uf.png) ->->-> `第一次執行下面時，setCount 會拿目前的狀態值來當作actualCount並進行疊加，而得到1，其1會成為新的目前狀態值。第二次執行類似語法時，setCount會拿目前的狀態值1來當作actualCount並進行疊加，而得到2，其2會成為新的目前狀態值。最後沒setCount等狀態更新指令，就執行目前狀態值2來更新和渲染`
<!--SR:!2023-06-20,188,250-->


---
Status: #🌱 
Tags:
[[React]] - [[JavaScript]]
Links:
[[React：setState 會試著將多個狀態更新任務合併成一個任務，進而減少因一個任務而觸發一次渲染的渲染次數]]
[[React batching 是將N個狀態更新指令合併成一個指令並只引發一次畫面渲染]]
References:
[[@dmitripavlutinHowReactUpdates2020]]
[[@khatriWhyDonReact2021]]