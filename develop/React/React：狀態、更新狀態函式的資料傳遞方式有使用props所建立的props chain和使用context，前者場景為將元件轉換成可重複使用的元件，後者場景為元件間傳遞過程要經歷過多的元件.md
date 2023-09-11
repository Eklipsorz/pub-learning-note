## 描述

> when to use props
> 1. you always use props to pass data to components

> when to use context
> 1. only if you have something which you would forward through a lot of components and you're forwarding it to a component that does something very specific



重點：
- 狀態、更新狀態函式的資料傳遞方式有：
	- 使用props所建立的props chain
	- 使用能夠集中儲存狀態且分享狀態的元件：
		- context
- 使用props的場景為
	- 作為預設用的資料傳遞方式
	- 製作可重複使用(reusable)的元件，具體根據props傳遞過來的資訊來轉換
	- 元件間是較短的props chains
- 使用context的場景為
	- 當元件A和元件B間之間在props chain傳遞過程需要經過多個元件時，可採用context




### 案例：使用props的場景
```
const Home = (props) => {
  return (
    <Card className={classes.home}>
      <h1>Welcome back!</h1>
      <Button onClick={props.onLogout}>Logout</Button>
    </Card>
  );
};
```

#### 若將Button 改成context的話

就等同如下，若要讓按鈕能夠實現登出，就必須要在按鈕元件本身添加登出，這使得通用按鈕變成專門登出的按鈕，這讓其他元件很難透過這元件來打造其他元件，也就是可重複性降低。
```
const Home = (props) => {
  return (
    <Card className={classes.home}>
      <h1>Welcome back!</h1>
      <Button>Logout</Button>
    </Card>
  );
};
```


## 複習

#🧠 狀態、更新狀態函式的資料傳遞方式有哪些？ ->->-> `使用props所建立的props chain以及使用能夠集中儲存狀態且分享狀態的元件，如context`
<!--SR:!2023-12-14,101,230-->

#🧠 使用props chain的場景為何？(製作、短) ->->-> `製作可重複使用(reusable)的元件、元件間是較短的props chains`
<!--SR:!2023-10-08,228,248-->

#🧠 使用props chain的場景為何？->->-> `製作可重複使用(reusable)的元件、元件間是較短的props chains`
<!--SR:!2023-11-23,256,248-->


#🧠 使用props chain的場景是打算將元件轉換成可重複使用(reusable)的元件之場景下，請問具體props如何實現可重複使用 ->->-> `具體根據props傳遞過來的資訊來轉換相同結構且不同內容的元件`
<!--SR:!2024-04-29,354,250-->

#🧠 使用props chain的場景是打算將元件轉換成可重複使用(reusable)的元件之場景下，請問具體props在這的可重複使用的意思是？ ->->-> `這讓其他元件更容易以其為原型來打造其他元件`
<!--SR:!2023-12-16,95,230-->

#🧠 使用context的場景為何？ ->->-> `當元件A和元件B間之間在props chain傳遞過程需要經過多個元件時，可採用context`
<!--SR:!2024-12-31,504,250-->


#🧠 React：若按鈕中去除掉props，改用context的話，會產生什麼樣的程式碼才能實現原有登出按鈕？![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1663766887/blog/react/context/when-to-use/using-props-case_xzkuzp.png) ->->-> `通常若要讓按鈕還原成原有的功能，就只能從按鈕本身使用context![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1663766887/blog/react/context/when-to-use/using-context-case_zhkupg.png)`
<!--SR:!2023-08-30,200,230-->

#🧠 React：上圖是使用props來實現登出按鈕，下圖是改用context來將登出功能寫在按鈕元件上，請問下圖有什麼潛在問題？![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1663766887/blog/react/context/when-to-use/using-props-case_xzkuzp.png) ![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1663766887/blog/react/context/when-to-use/using-context-case_zhkupg.png)->->-> `這使得通用按鈕變成專門登出的按鈕，這讓其他元件很難透過這元件來打造其他元件，也就是可重複性降低。`
<!--SR:!2023-12-11,98,230-->

---
Status: #🌱 
Tags:
[[React]]
Links:
[[React：useContext 是React內建的HOOK，專門替當前元件取得指定context object的目前值]]
[[React：Context API擁有context object、provider、consumer，最前者為定義狀態的環境，中間者為提供狀態值給予最前者的一方，最後者為使用該環境的一方]]
References:
