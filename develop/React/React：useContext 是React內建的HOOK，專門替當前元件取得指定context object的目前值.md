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
- useContext 是包裝著 **對應Context的Consumer Component獲取對應Context值方法** 的語法糖
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

#🧠 useContext 是什麼？  ->->-> `是包裝著 對應Context的Consumer Component獲取對應Context值方法的語法糖`
<!--SR:!2024-12-28,489,250-->

#🧠 useContext 在元件上代表著？ ->->-> ` useContext 是React內建的HOOK，會註冊每個元件下`
<!--SR:!2023-08-11,168,230-->

#🧠 useContext  用途是什麼？ ->->-> `替代context object的consumer component來使用狀態值、獲取指定context object的目前狀態值`
<!--SR:!2023-07-29,194,250-->

#🧠 useContext 語法為何？->->-> `const value = useContext(context)`
<!--SR:!2023-07-29,194,250-->

#🧠 useContext 語法是const value = useContext(context)，其中context和value會是指什麼？->->-> `context是指定要存取的context object是哪個，value會是對應context object的目前狀態值，其值會以離目前元件較近的Provider Component所提供或者由createContext的預設值所提供`
<!--SR:!2023-07-29,194,250-->

#🧠 useContext(context.Provider) 這樣對於React的useContext的用法是對的嗎->->-> `不對，只能填入Context object`
<!--SR:!2024-03-14,324,250-->

#🧠 useContext(context.Consumer) 這樣對於React的useContext的用法是對的嗎->->-> `不對，只能填入Context object`
<!--SR:!2023-06-27,170,250-->

#🧠 useContext(contex) 這樣對於React的useContext的用法是對的嗎->->-> `對，只能填入Context object`
<!--SR:!2023-07-06,179,250-->


---
Status: #🌱 
Tags:
[[React]]
Links:
[[React：Context API擁有context object、provider、consumer，最前者為定義狀態的環境，中間者為提供狀態值給予最前者的一方，最後者為使用該環境的一方]]
References:
[[@reactHooksAPICanKao]]