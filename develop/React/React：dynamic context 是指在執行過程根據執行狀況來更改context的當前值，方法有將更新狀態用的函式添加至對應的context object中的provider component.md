## 描述

dynamic context：在執行過程中來根據執行狀況來更改context的當前狀態值

方式1：
- 將更新狀態用的函式註冊至指定context object中的provider component之value

```
return (
    <AuthContext.Provider
      value={{
        isLoggedIn: isLoggedIn,
        onLogout:logoutHandler
      }}
    >
      <MainHeader onLogout={logoutHandler} />
      <main>
        {!isLoggedIn && <Login onLogin={loginHandler} />}
        {isLoggedIn && <Home onLogout={logoutHandler} />}
      </main>
    </AuthContext.Provider>
  );
```

- 再讓想修改其context上的狀態的元件透過context object的consumer component語法糖採用ctx的目前狀態值-onLogout 好讓當前元件B透過自己的角度來改變context當前的狀態
```
const Navigation = (props) => {
  const ctx = useContext(AuthContext);

  return (
    <nav className={classes.nav}>
      <ul>
        {ctx.isLoggedIn && (
          <li>
            <a href='/'>Users</a>
          </li>
        )}
        {ctx.isLoggedIn && (
          <li>
            <a href='/'>Admin</a>
          </li>
        )}
        {ctx.isLoggedIn && (
          <li>
            <button onClick={ctx.onLogout}>Logout</button>
          </li>
        )}
      </ul>
    </nav>
  );
};
```



## 複習

#🧠 React Context：dynamic context 是什麼？ ->->-> `在執行過程中來根據執行狀況來更改context的當前狀態值`
<!--SR:!2023-01-14,74,250-->

#🧠 React Context：dynamic context 如何實現？ ->->-> `1. 將更新狀態用的函式添加至指定context object中的provider component之value 2. 再讓想修改其context上的狀態的元件透過context object的consumer component語法糖採用ctx的目前狀態值-onLogout 好讓當前元件B透過自己的角度來改變context當前的狀態`
<!--SR:!2023-02-14,85,230-->

#🧠 React：以下為dynamic context 的實現，上圖為App元件，下圖為Navigation元件，請說明如何利用context實現登出功能？![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1663768466/blog/react/context/dynamic-context/providing-component_bniuln.png) ![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1663768466/blog/react/context/dynamic-context/comsuming-component_qfkokd.png)->->-> ``
<!--SR:!2023-02-13,34,230-->

---
Status: #🌱 
Tags:
[[React]]
Links:
[[React：useContext 是React內建的HOOK，專門替當前元件取得指定context object的目前值]]
[[React：Context API擁有context object、provider、consumer，最前者為定義狀態的環境，中間者為提供狀態值給予最前者的一方，最後者為使用該環境的一方]]
References: