## 描述



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
	- 執行setCount並不會更改count這個變數
	- setCount實際上：
		- 生成一個非同步更新狀態任務(生完就做下一步)：對該元件的(負責儲存狀態值)特殊變數進行狀態更新，其狀態會是以現有引數為主
		- 生成一個另一個非同步任務專門渲染(生完就做下一步)以現有的引數或者說
		- 

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


### Why is State Update Async?
[[@khatriWhyDonReact2021]]
> # Why is State Update Async?

> State updates alter the virtual DOM and cause re-rendering which may be an expensive operation. Making state updates synchronous could make the browser unresponsive due to huge number of updates.

> To avoid these issues a careful choice was made to make state updates async, as well as to batch those updates.

重點：
- state update 是非同步操作，且一個非同步操作包含兩個行為：
	- 更新對應元件的(專門儲存狀態值)特殊變數
	- 重新

## 複習
#🧠 Question :: ->->-> ``

---
Status: #🌱 
Tags:
[[React]] - [[JavaScript]]
Links:
References:
[[@dmitripavlutinHowReactUpdates2020]]
[[@khatriWhyDonReact2021]]