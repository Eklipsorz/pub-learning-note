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
- automatic batching 為 **不管是不是在事件處理執行N個狀態更新指令，只要在root節點下的子節點都直接自動以Batching來執行**
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
	- 在同一個生命週期函式下，事件處理、Promise、setTimeOut 這三者所會做的Batching 皆為獨立：
		- 多個事件處理中的每個事件處理都自行做自己內部的batching
		- 多個夾雜狀態更新指令的Promise都算在一起做batching
		- 多個夾雜狀態更新指令的setTimeOut都算在一起做batching
	
	- 每種內含的狀態更新指令不會合併再一起，只會以同一種的狀態更新指令來進行合併，比如說：
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

### 同個生命週期下，多個不同狀態的狀態更新

在同個生命週期下，即使是每個狀態更新指令要求更新的狀態是不同的，都會以batching來做處理

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
<!--SR:!2023-07-11,174,230-->

#🧠 batching 命名緣由 ->->-> `以一群事物為單位為來進行特定處理之過程、行為`
<!--SR:!2023-05-29,65,230-->


#🧠 React Batching 是指什麼技術？ ->->-> `是指React 將N個狀態更新指令(setState)為一組來進行特定處理`
<!--SR:!2024-10-11,477,250-->

#🧠 React Batching 是指將N個狀態更新指令(setState)為一組來進行特定處理，那麼特定處理會是什麼？跟上面那句結合會是指什麼意思？ >->-> `合併成一個具有特定狀態的狀態更新指令，具體是將N個狀態更新指令(setState)合併成一個特定狀態的狀態更新指令`


#🧠 React Batching 是指將N個狀態更新指令(setState)為一組來合併成一個具有特定狀態的狀態更新指令，其特定狀態會是什麼？ ->->-> `具體是N個狀態更新指令所要求改變的狀態之合併後的狀態，若是單一值的狀態，就以最後一個接收到的狀態值為主；若是物件的話，首先會是以空物件來表示，接著將遍歷這n個指令看看狀態上屬性是什麼，接著將屬性納入物件或者直接以最新的屬性值覆蓋上去。`
<!--SR:!2023-06-26,193,250-->

#🧠 React Batching 好處是什麼？ ->->-> `透過合併來減少大量重複渲染的操作：每一個狀態更新指令(setState)就會引發一次updating的渲染`
<!--SR:!2023-12-21,108,230-->

#🧠 React Batching 在React 18之前的版本為何？ ->->-> `主要依據著isBatchUpdate是否為true來決定是否執行Batching，若false，就不以Batching來執行；若true，就以Batching`
<!--SR:!2024-04-24,295,230-->

#🧠 React Batching 在React 18之前的版本為何？ 會開放在事件處理上嗎？為什麼？ ->->-> `Batching 只開放在事件處理，理由為React可以直接從瀏覽器的事件擷取`
<!--SR:!2023-06-19,188,250-->

#🧠 React Batching 在React 18之前的版本為何？ 會開放在Promise、setTimeOut嗎？為什麼？ ->->-> `Batching 在Promise、setTimeOut中無法被執行且被設定為**isBatchUpdate**為false，理由為React 無法從中控制，除非改寫Promise、setTimeOut`
<!--SR:!2023-12-05,107,230-->

#🧠 React Batching 在 React 18起的版本會是？ ->->-> `Batching 開放在事件處理、Promise、setTimeOut。 Batching 在盡量將N個狀態更新指令合併的情況下，就自動按照算法判定如何合併`
<!--SR:!2023-06-25,192,250-->

#🧠 React automatic batching 是什麼？ ->->-> `不管是不是在事件處理執行N個狀態更新指令，只要在root節點下的子節點都直接自動以Batching來執行`
<!--SR:!2023-08-14,118,210-->


#🧠 React automatic batching是為 **不管是不是在事件處理執行N個狀態更新指令，都直接自動以Batching來執行** ，換言之在Promise/setTimeOut/事件處理上出現N個狀態更新指令會是？  ->->-> `即使在Promise/setTimeOut中出現N個狀態更新指令，皆會像是在事件處理那樣可以被合併`
<!--SR:!2023-10-17,254,250-->


#🧠 React automatic batching 啟用條件為何？ ->->-> `automatic batching 只要使用createRoot來建立Virtual DOM的root節點，並於其節點建立子節點就會夠擁有automatic batching 特性`
<!--SR:!2023-12-22,228,230-->

#🧠 React automatic batching 啟用條件為何？用程式碼來表示 ->->-> `const root = ReactDOM.createRoot(document.getElementById('root')); root.render(	<React.StrictMode> <App /> </React.StrictMode>);`
<!--SR:!2024-01-24,314,250-->


#🧠 React18: 若N個狀態更新指令遍佈在多個生命週期函式下的事件處理，這N個狀態可以被合併成一個指令嗎？ ->->-> `並不會，只會針對同一個生命週期函式內含事件處理下的多個狀態更新指令來合併`
<!--SR:!2024-10-22,476,250-->

#🧠 React18: 若N個狀態更新指令遍佈在多個生命週期函式下的Promise，這N個狀態可以被合併成一個指令嗎？ ->->-> `並不會，只會針對同一個生命週期函式內含Promise的多個狀態更新指令來合併`
<!--SR:!2024-07-25,426,250-->


#🧠 React18: 若N個狀態更新指令遍佈在多個生命週期函式下的setTimeOut，這N個狀態可以被合併成一個指令嗎？ ->->-> `並不會，只會針對同一個生命週期函式內含setTimeOut的多個狀態更新指令來合併`
<!--SR:!2025-03-17,568,250-->



#🧠 React18: 在同一個生命週期函式下，事件處理、Promise、setTimeOut下都夾雜著多個狀態更新指令，請問Batching會合併處理嗎？為什麼? ->->-> `並不會，只會在同一個生命週期中，讓事件處理、Promise、setTimeOut各自處理自己的Batching`
<!--SR:!2023-12-25,295,250-->


#🧠 React18: 在同一個生命週期函式下，那麼如果發生多個事件處理來處理，會如何處理batching？ 全部事件處理都算在一塊做batching? ->->-> `多個事件處理中的每個事件處理都自行做自己內部的batching`
<!--SR:!2024-06-26,408,250-->

#🧠  React18: 在同一個生命週期函式下，那麼如果發生多個夾雜狀態更新指令的Promise，會如何處理batching？  ->->-> `多個夾雜狀態更新指令的Promise都算在一起做batching`
<!--SR:!2024-06-14,396,250-->


#🧠 React18: 在同一個生命週期函式下，那麼如果發生多個夾雜狀態更新指令的setTimeOut，會如何處理batching？->->-> `多個夾雜狀態更新指令的setTimeOut都算在一起做batching`
<!--SR:!2023-12-14,109,230-->

#🧠 React18: 考慮以下事件處理，請問react batching 會如何處理這內含的case1-case6，目前react是18![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1661171193/blog/react/batching/batching-example_hhfzvj.png) ->->-> `- case 1 會和 case 3 合併 - case 2 會和 case 5 合併 - case 4 會和 case 6 合併`
<!--SR:!2023-06-01,177,250-->


#🧠  react batching ：考慮以下事件處理，請問多個事件所衍生出來的handler 所衍生batching狀況是如何，目前react是18![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1661171193/blog/react/batching/batching-example_hhfzvj.png) ->->-> `由於多個事件處理中的每個事件處理都自行做自己內部的batching，所以每個handler都各自合併`
<!--SR:!2025-03-05,566,250-->

#🧠 React batching：請問目前版本為react 18，請問該渲染狀態更新指令會如何處理![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1661174173/blog/react/batching/react-batching-setTimeOut-example_q337id.png) ->->-> `會合併成一個狀態更新指令，來觸發`
<!--SR:!2024-11-09,494,250-->

#🧠 React batching：請問目前版本為react 18，請問該渲染狀態更新指令會如何處理![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1661174173/blog/react/batching/react-batching-promise-example_oc4lrv.png)->->-> `會合併成一個狀態更新指令，來觸發`
<!--SR:!2024-06-07,396,250-->

#🧠 React batching：請問目前版本為react 18，請問該渲染狀態更新指令會如何處理 ![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1661174173/blog/react/batching/react-batching-handler-example_pjtidy.png) ->->-> `會合併成一個狀態更新指令，來觸發`
<!--SR:!2025-01-31,533,250-->

#🧠 React batching：同一個生命週期函式下，多個渲染狀態指令要求的狀態都不一樣，會如何做處理 ->->-> `通常會合併成一個特定狀態的狀態更新指令，特定狀態為多個渲染指令的狀態要求合併之結果`
<!--SR:!2024-10-29,483,250-->



---
Status: #🌱 
Tags:
[[React]] - [[JavaScript]]
Links:
References:
[[@gaearonAutomaticBatchingFewer]]