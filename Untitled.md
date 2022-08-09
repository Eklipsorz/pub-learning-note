JSX which is basically HTML code inside of JavaScript

JSX stands for JavaScript XML (HTML)

which is not normally supported in the browser

為了什麼而提出額外的程式語言，然後進而轉譯成javascript?

### JSX 起源
JSX 全名為JavaScript XML
1. 是由React團隊額外從JavaScript、



### JSX 語法

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


```
import './index.css';
```