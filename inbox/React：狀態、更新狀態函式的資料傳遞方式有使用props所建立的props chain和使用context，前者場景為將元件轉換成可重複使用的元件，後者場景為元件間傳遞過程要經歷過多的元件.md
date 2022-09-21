## 描述

> when to use props
> 1. you always use props to pass data to components

> when to use context
> 1. only if you have something which you would forward through a lot of components and you're forwarding it to a component that does something very specific


重點：
- 狀態、更新狀態函式的資料傳遞方式有：
	- 使用props所建立的props chain
	- 使用context
- 使用props的場景為
	- 作為預設用的資料傳遞方式
	- 將元件轉換成可重複使用(reusable)的元件，具體根據props傳遞過來的資訊來轉換
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

就等同如下，若要讓按鈕能夠實現登出，就必須要在按鈕元件本身添加登出，這使得通用按鈕變成專門登出的按鈕，使可重複性降低。
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
#🧠 Question :: ->->-> ``

---
Status: #🌱 #📓 
Tags:
[[React]]
Links:
[[React：useContext 是React內建的HOOK，專門替當前元件取得指定context object的目前值]]
[[React：Context API擁有context object、provider、consumer，最前者為定義狀態的環境，中間者為提供狀態值給予最前者的一方，最後者為使用該環境的一方]]
References: