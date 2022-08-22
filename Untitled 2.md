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

- 要依據setCount每次執行而得到目前結果值，可以使用callback
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




## 複習
#🧠 Question :: ->->-> ``
<!--SR:!2022-08-31,10,250-->

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