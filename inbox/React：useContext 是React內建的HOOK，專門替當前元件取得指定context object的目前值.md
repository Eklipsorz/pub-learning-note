## 描述
[[@reactHooksAPICanKao]]
> useContext
```
const value = useContext(MyContext);
```

> 接收一個 context object（React.createContext 的回傳值）並回傳該 context 目前的值。Context 目前的值是取決於由上層 component 距離最近的 <MyContext.Provider> 的 value prop。
> 
> 當 component 上層最近的 <MyContext.Provider> 更新時，該 hook 會觸發重新 render，並使用最新傳遞到 MyContext 的 context value 傳送到 MyContext provider。即便 ancestor 使用 React.memo 或 shouldComponentUpdate，重新 render 仍然從使用 useContext 的 component 本身開始。

> 不要忘記 useContext 的參數必需為 context object 自己：
```
正確: useContext(MyContext)
錯誤: useContext(MyContext.Consumer)
錯誤: useContext(MyContext.Provider)
```


重點：
- useContext 是React內建的HOOK，會註冊每個元件下
- 用途為：
	- 替代context object的consumer component來使用狀態值
	- 獲取指定context object的目前狀態值
- 語法為
	  - context ： 指定要使用的context object是什麼
	  - 回傳內容為：context object的目前狀態值，該狀態值會是離當前元件最近的特定parent 元件所提供給context object的value，且parent 元件會是context object的provider component所組成。
```
const value = useContext(context)
```
- 正確 & 錯誤用法：
	- 正確
	```
	useContext(context)
	```
	- 錯誤
	```
	useContext(context.Provider)
	useContext(context.Consumer)
	```

## 複習


---
Status: #🌱 #📓 
Tags:
[[React]]
Links:
[[React：Context API擁有context object、provider、consumer，最前者為定義狀態的環境，中間者為提供狀態值給予最前者的一方，最後者為使用該環境的一方]]
References:
[[@reactHooksAPICanKao]]