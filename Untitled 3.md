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
- automatic batching 為 **不管是不是在事件處理執行N個狀態更新指令，都直接自動以Batching來執行**。
- automatic batching 有個限制，同一個執行環境(EC)

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
- batching 是指以一群事物為單為來進行特定處理之過程、行為

## 複習
#🧠 Question :: ->->-> ``

---
Status: #🌱 
Tags:
[[React]] - [[JavaScript]]
Links:
References:
[[@gaearonAutomaticBatchingFewer]]