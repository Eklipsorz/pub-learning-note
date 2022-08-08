ReactDOM.createRoot => create the main entry point
the main hook of the overall user interface you are about to build with React
That's the idea behind createRoot


createRoot()
```
createRoot(container[, options]);
```
Create a React root for the supplied `container` and return the root. The root can be used to render a React element into the DOM with `render`:
```
const root = createRoot(container);
root.render(element);
```

- container ：會是指dom節點
- createRooot：主要指定哪個dom節點或者容器會是react層級的root節點，並回傳root
- 每個react層級的root節點可以呼叫render來將react element 指定放入在對應DOM節點 或者告訴系統 root節點對應的dom節點要如何被渲染




public 下的 index.html是最主要載入bundle.js的html，由index.html來搭配互動來讓bundle.js產生對應的畫面



  
```
function App() {
    return (
         <div>
             <h2> ....</h2>
        </div>
   );
}
```

1. It's also not valid JavaScript code normally
2. This is JSX


```
<App />
```

<App />：
1. that is definitely not regular JavaScript syntax here
2. This is a syntax called JSX
3. It means React component

  

JSX：
1. it's a special syntax invented
2. it's introduced by the React team
3. JSX ->(babel or transcompiler) -> JavaScript



root.render(<App />); 中的 App 是指 App.js 下的 App

另外import 細節  
1. 若想引入的import是js檔案，可以忽略副檔名



CSS-in-JS：一種允許JavaScript能夠解析CSS內容的技術，並讓它透過JavaScript的執行形式來根據執行狀態來更新對應CSS的內容


