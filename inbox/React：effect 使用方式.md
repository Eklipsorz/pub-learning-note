## 描述

and it is executed after important, after component re-evaluation/evaluation

but it will not just run after component evaluation but only if the dependencies here changed.

useEffect(callback, dependencies)

### effect 使用方法

`useEffect(callback, [dependencies])`

useEffect 語法：會替當前元件註冊effect。
- 第一個引數為callback，這些callback只會在dependencies 改變的時候才執行，而不是在component重新渲染的時候呼叫
> a function that should be executed AFTER every component evaluation IF the specified dependencies changes
-  第二個引數為設定哪些dependencies 改變才會觸發前面的callback，會用陣列來表示所有的dependencies
> dependencies of this effect - the function only runs if the dependencies changed


#### dependencies
dependencies：
- dependencies 會是指目前執行環境所能夠存取的狀態、props
- 主要會指定監聽哪些dependency有沒有變動或者沒建立
- 若沒建立或者任一變動就允許執行useEffect
- 特例：
	- 若是空陣列[] 的話，就等同設定永不改變的dependency
	- 若是

#### 何時執行

1. 在mounting階段進行useEffect的hook綁定，就會直接執行
2. 歷經mounting階段後的階段，只要發生updating階段或者unmounting階段的同時，depenedencies有發生變動或者


##### 案例：


在首次渲染目前元件時，會註冊著useEffect這個effect，同時由於沒有任何

由於沒有任何dependencies，才觸發useEffect，若下次evaluation後，dependencies沒變動，useEffect的callback並不會執行，直到下次evaluation後且dependencies變動，才會執行對應的callback






進入登入頁前會先檢查特定儲存空間中是否指定使用者資料，若有就以指定資料來登入；若沒，就重新登入，藉由登入來儲存特定使用者資料至特定儲存空間中。

  

特定儲存空間為browser storage，這些空間是由瀏覽器內建的，分別為

1. cookie

2. local storage (選擇這個)



```
import React, { useState } from 'react';

import Login from './components/Login/Login';
import Home from './components/Home/Home';
import MainHeader from './components/MainHeader/MainHeader';

function App() {
  const [isLoggedIn, setIsLoggedIn] = useState(false);
  /// 會衍生無限迴圈
  const storedUserLoggedInInformation = localStorage.getItem('isLoggedIn');

  if (storedUserLoggedInInformation === '1') {
    setIsLoggedIn(true);
  }
  ///
  const loginHandler = (email, password) => {
    // We should of course check email and password
    // But it's just a dummy/ demo anyways
    localStorage.setItem('isLoggedIn', '1');
    setIsLoggedIn(true);
  };

  const logoutHandler = () => {
    setIsLoggedIn(false);
  };

  return (
    <React.Fragment>
      <MainHeader isAuthenticated={isLoggedIn} onLogout={logoutHandler} />
      <main>
        {!isLoggedIn && <Login onLogin={loginHandler} />}
        {isLoggedIn && <Home onLogout={logoutHandler} />}
      </main>
    </React.Fragment>
  );
}

export default App;

```




```
function App() {
	useEffect(() => {
		console.log('this is use effect')
	})
	
	console.log('this is rendering')
}
```

結果會是如下：
```
this is rendering 
this is use effect
```

[[@ithomeReactJsRuMen20]]
> 是`componentDidMount`、`componentWillUnmount`和`componentDidUpdate`這三個函數，而React hook把這三者整合起來，變成了`useEffect`。


useEffect(callback) -> is executed by react



### useEffect 執行頻率
[[@ReactUseEffect]]
```jsx
useEffect(() => {
  //Runs on every render
});
```

```jsx
useEffect(() => {
  //Runs only on the first render
}, []);
```


```jsx
useEffect(() => {
  //Runs on the first render
  //And any time any dependency value changes
}, [prop, state]);
```


### effect 綁定整個元件的生命週期

當元件處於mounting時，就會建立effect hook來綁定在該元件，並觸發effect，隨後若發生updating或者unmounting的話，預設上會再去觸發effect。

若同一個元件發生unmount並重新發生mounting，會再次產生額外的effect hook來綁定在該元件，觸發如同上述那樣


### 當畫面A被切換成畫面B時
當畫面A被切換成畫面B時，即為畫面A發生unmounting，並且mounting 畫面B

## 複習


---
Status: #🌱 
Tags:
[[React]]
Links:
[[React：effect 是指除了元件本身所要做的主要功能-渲染元件、與使用者互動來管理狀態以外的額外效果，額外效果會是指脫離渲染週期的任意功能]]
References:
[[@ReactUseEffect]]
[[@ithomeReactJsRuMen20]]