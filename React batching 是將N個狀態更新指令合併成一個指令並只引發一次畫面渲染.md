## 描述
### what is batching 
[[@gaearonAutomaticBatchingFewer]]
> ## What is batching?

> Batching is when React **groups multiple state updates into a single re-render** for better performance.

> For example, if you have two state updates inside of the same click event, React has always batched these into one re-render. If you run the following code, you’ll see that every time you click, React only performs a single render although you set the state twice:

```
function App() {
  const [count, setCount] = useState(0);
  const [flag, setFlag] = useState(false);

  function handleClick() {
    setCount(c => c + 1); // Does not re-render yet
    setFlag(f => !f); // Does not re-render yet
    // React will only re-render once at the end (that's batching!)
  }

  return (
    <div>
      <button onClick={handleClick}>Next</button>
      <h1 style={{ color: flag ? "blue" : "black" }}>{count}</h1>
    </div>
  );
}
```


> This is great for performance because it avoids unnecessary re-renders. It also prevents your component from rendering “half-finished” states where only one state variable was updated, which may cause bugs. This might remind you of how a restaurant waiter doesn’t run to the kitchen when you choose the first dish, but waits for you to finish your order.

> However, React wasn’t consistent about when it batches updates. For example, if you need to fetch data, and then update the state in the `handleClick` above, then React would _not_ batch the updates, and perform two independent updates.

> This is because React used to only batch updates _during_ a browser event (like click), but here we’re updating the state _after_ the event has already been handled (in fetch callback):

```
function App() {
  const [count, setCount] = useState(0);
  const [flag, setFlag] = useState(false);

  function handleClick() {
    fetchSomething().then(() => {
      // React 17 and earlier does NOT batch these because
      // they run *after* the event in a callback, not *during* it
      setCount(c => c + 1); // Causes a re-render
      setFlag(f => !f); // Causes a re-render
    });
  }

  return (
    <div>
      <button onClick={handleClick}>Next</button>
      <h1 style={{ color: flag ? "blue" : "black" }}>{count}</h1>
    </div>
  );
}
```

> Until React 18, we only batched updates during the React event handlers. Updates inside of promises, setTimeout, native event handlers, or any other event were not batched in React by default.

重點：
- React Batching 是指React 將N個狀態更新指令(setState)為一組來進行特定處理：
	- 在這裡的特定處理就是指 **合併成一個具有特定狀態的狀態更新指令**
	- 特定狀態會是指N個更新指令所指示的狀態合併結果，其結果產出方式為：
		- 狀態為單一值的話，就以最後解析到的狀態值為主。
		- 狀態為物件的話，定義目前合併結果為空物件A，每一次解析到的屬性名稱和屬性值就直接覆蓋/納入至物件A中。
- React Batching 好處：
	- 透過合併來減少大量重複渲染的操作：每一個狀態更新指令(setState)就會引發一次updating的渲染
- 在React 18之前的版本：
	- Batching 實際上會依據著 **isBatchUpdate** 是否為true：true就以Batching執行，false就不合併
	- Batching 只開放在事件處理，理由為React可以直接從瀏覽器的事件擷取
	- Batching 在Promise、setTimeOut中無法被執行且被設定為**isBatchUpdate**為false，理由為React 無法從中控制，除非改寫Promise、setTimeOut
- 在React 18起的版本：
	- Batching 開放在事件處理、Promise、setTimeOut
	- Batching 在盡量將N個狀態更新指令合併的情況下，就自動按照算法判定如何合併
### what is automatic batching

> ## What is automatic batching?

> Starting in React 18 with [`createRoot`](https://github.com/reactwg/react-18/discussions/5), all updates will be automatically batched, no matter where they originate from.

> This means that updates inside of timeouts, promises, native event handlers or any other event will batch the same way as updates inside of React events. We expect this to result in less work rendering, and therefore better performance in your applications:

```
function App() {
  const [count, setCount] = useState(0);
  const [flag, setFlag] = useState(false);

  function handleClick() {
    fetchSomething().then(() => {
      // React 18 and later DOES batch these:
      setCount(c => c + 1);
      setFlag(f => !f);
      // React will only re-render once at the end (that's batching!)
    });
  }

  return (
    <div>
      <button onClick={handleClick}>Next</button>
      <h1 style={{ color: flag ? "blue" : "black" }}>{count}</h1>
    </div>
  );
}
```


重點：
- automatic batching 為 **不管是不是在事件處理執行N個狀態更新指令，都直接自動以Batching來執行**
- 換言之，即使在Promise/setTimeOut中出現N個狀態更新指令，皆會像是在事件處理那樣可以被合併
- automatic batching 只要使用createRoot來建立Virtual DOM的root節點，並於其節點建立子節點就會夠擁有automatic batching 特性
```
const root = ReactDOM.createRoot(document.getElementById('root'));

root.render(
	<React.StrictMode>
		<App />
	</React.StrictMode>
);
```

- Batching：
	- 在同一個生命週期函式下，事件處理/Promise/setTimeOut的N個狀態更新指令才會合併；若N個狀態更新指令遍佈在多個生命週期函式下，這N個狀態更新指令不會合併，只會按照同一個週期函式來處理
	- 在同一個生命週期函式下，事件處理、Promise、setTimeOut 這三者所會做的Batching 皆為獨立，並不會以3\*N個指令來進行合併，也就是同為事件處理就一起合併，每種內含的狀態更新指令不會合併再一起，只會以同一種的狀態更新指令來進行合併，比如說：
	- case 1 會和 case 3 合併
	- case 2 會和 case 5 合併
	- case 4 會和 case 6 合併

```
fimctopm handler() {
	// case 1
	setCount(count + 1);
	setCount(count + 1);
	
	// case 2
	setTimeout(() => {
		setCount(count + 1);
	}, 1000);

	// case 3
	setCount(count + 1);
	setCount(count + 1);

	// case 4
	Promise.resolve().then(() => {
		setCount(count + 1);
	});

	// case 5
	setTimeout(() => {
		setCount(count + 1);
	}, 1000);

	// case 6
	Promise.resolve().then(() => {
		setCount(count + 1);
	});
}
```

React will batch updates automatically, no matter where the updates happen, so this:
```
function handleClick() {
  setCount(c => c + 1);
  setFlag(f => !f);
  // React will only re-render once at the end (that's batching!)
}
```


behaves the same as this:
```
setTimeout(() => {
  setCount(c => c + 1);
  setFlag(f => !f);
  // React will only re-render once at the end (that's batching!)
}, 1000);

```

behaves the same as this:
```
fetch(/*...*/).then(() => {
  setCount(c => c + 1);
  setFlag(f => !f);
  // React will only re-render once at the end (that's batching!)
})
```


behaves the same as this:
```
elm.addEventListener('click', () => {
  setCount(c => c + 1);
  setFlag(f => !f);
  // React will only re-render once at the end (that's batching!)
});
```



###  Batch 命名緣由

batch：
> to group (items) for efficient processing

重點：
- batch 動詞是指以一群事物為單位來進行特定處理
- batching 是指以一群事物為單位為來進行特定處理之過程、行為

## 複習
#🧠 Batch 命名緣由->->-> `以一群事物為單位來進行特定處理`

#🧠 batching 命名緣由 ->->-> `以一群事物為單位為來進行特定處理之過程、行為`


#🧠 React Batching 是指什麼技術？ ->->-> `是指React 將N個狀態更新指令(setState)為一組來進行特定處理`

#🧠 React Batching 是指將N個狀態更新指令(setState)為一組來進行特定處理，那麼特定處理會是什麼？跟上面那句結合會是指什麼意思？ >->-> `合併成一個具有特定狀態的狀態更新指令，具體是將N個狀態更新指令(setState)合併成一個特定狀態的狀態更新指令`




#🧠 React Batching 是指將N個狀態更新指令(setState)為一組來合併成一個具有特定狀態的狀態更新指令，其特定狀態會是什麼？ ->->-> `具體是N個狀態更新指令所要求改變的狀態之合併後的狀態，若是單一值的狀態，就以最後一個接收到的狀態值為主；若是物件的話，首先會是以空物件來表示，接著將遍歷這n個指令看看狀態上屬性是什麼，接著將屬性納入物件或者直接以最新的屬性值覆蓋上去。`

#🧠 React Batching 好處是什麼？ ->->-> `透過合併來減少大量重複渲染的操作：每一個狀態更新指令(setState)就會引發一次updating的渲染`

#🧠 React Batching 在React 18之前的版本為何？ ->->-> `主要依據著isBatchUpdate是否為true來決定是否執行Batching，若false，就不以Batching來執行；若true，就以Batching`

#🧠 React Batching 在React 18之前的版本為何？ 會開放在事件處理上嗎？為什麼？ ->->-> `Batching 只開放在事件處理，理由為React可以直接從瀏覽器的事件擷取`

#🧠 React Batching 在React 18之前的版本為何？ 會開放在Promise、setTimeOut嗎？為什麼？ ->->-> `Batching 在Promise、setTimeOut中無法被執行且被設定為**isBatchUpdate**為false，理由為React 無法從中控制，除非改寫Promise、setTimeOut`

#🧠 React Batching 在 React 18起的版本會是？ ->->-> `Batching 開放在事件處理、Promise、setTimeOut。 Batching 在盡量將N個狀態更新指令合併的情況下，就自動按照算法判定如何合併`

#🧠 React automatic batching 是什麼？ ->->-> `automatic batching 為 **不管是不是在事件處理執行N個狀態更新指令，都直接自動以Batching來執行**`

#🧠 React automatic batching是為 **不管是不是在事件處理執行N個狀態更新指令，都直接自動以Batching來執行** ，換言之在Promise/setTimeOut/事件處理上出現N個狀態更新指令會是？  ->->-> `即使在Promise/setTimeOut中出現N個狀態更新指令，皆會像是在事件處理那樣可以被合併`


#🧠 React automatic batching 啟用條件為何？ ->->-> `automatic batching 只要使用createRoot來建立Virtual DOM的root節點，並於其節點建立子節點就會夠擁有automatic batching 特性`

#🧠 React automatic batching 啟用條件為何？用程式碼來表示 ->->-> ``





---
Status: #🌱 
Tags:
[[React]] - [[JavaScript]]
Links:
References:
[[@gaearonAutomaticBatchingFewer]]