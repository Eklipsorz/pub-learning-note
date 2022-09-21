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
	- 將元件轉換成可重複使用(reusable)的元件：可根據props傳遞過來的資訊
- 使用context的場景為
	- 當元件A和元件B間之間在props chain傳遞過程需要經過多個元件時，可採用context



### 
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

## 複習
#🧠 Question :: ->->-> ``

---
Status: #🌱 #📓 
Tags:
[[React]]
Links:
References: