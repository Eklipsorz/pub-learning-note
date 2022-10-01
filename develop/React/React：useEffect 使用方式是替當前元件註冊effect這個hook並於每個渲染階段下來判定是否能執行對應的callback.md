## 描述


### 每個effect hook皆為獨立的

當元件處於mounting時，就會建立對應effect hook函式物件來綁定在該元件，並觸發effect，隨後若發生updating或者unmounting的話，預設上會再去觸發effect。

若同一個元件因為viewport的畫面切換而發生unmount並重新發生mounting，在發生unmount 就會移除舊有effect，並於mounting時期會再次產生額外的effect hook來綁定在該元件，觸發如同上述那樣


### 當畫面A被切換成畫面B時
當畫面A被切換成畫面B時，即為畫面A發生unmounting，並且mounting 畫面B，在這裡可分為：
- 畫面A 和 畫面B 都是畫面A
- 畫面A 和 畫面B 都不一樣


### effect 使用方法


#### effect 使用語法
`useEffect(callback, [dependencies])`

useEffect 語法：會替當前元件註冊effect。
- 第一個引數為callback，這些callback只會在dependencies 改變的時候才執行，而不是在component重新渲染的時候呼叫
> a function that should be executed AFTER every component evaluation IF the specified dependencies changes
-  第二個引數為設定哪些dependencies 改變才會觸發前面的callback，會用陣列來表示所有的dependencies
> dependencies of this effect - the function only runs if the dependencies changed


#### dependencies
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

dependencies：
- dependencies 會是定義著callback所需要的狀態、props、其他代表互動且跟著互動而變動的資料
- 主要會指定監聽哪些dependency有沒有變動
- 若任一變動就允許執行useEffect
- 特例：
	- 若是空陣列[] 的話，就等同設定永不改變的dependency
	- 若是沒設定任何dependency的話，就等同設定永遠改變的dependency


#### 何時執行side effect

[[@ithomeReactJsRuMen20]]
> 是`componentDidMount`、`componentWillUnmount`和`componentDidUpdate`這三個函數，而React hook把這三者整合起來，變成了`useEffect`。

每一次useEffect的side effect 觸發時間點會是同個元件的生命週期函式：
- mounting階段時的componentDidMount週期函式
- updating階段時的componentDidUpdate 週期函式
- ~~unmount階段時的componentWillUnmoun週期函式~~


1. 在mounting階段進行useEffect的hook綁定，並於mounting階段的componentDidMount週期來直接執行useEffect的callback
2. 若觸發updating階段，那麼就會在componentDidUpdate週期檢查useEffect的dependency是否有變動，若有的話，就執行callback；若沒有的話，就不執行callback
3. ~~若觸發unmount的階段，那麼就會在componentWillUnmount週期檢查useEffect的dependency是否有變動，若有的話，就執行callback；若沒有的話，就不執行callback~~
3. 在unmounting 階段下，會無視dependency是什麼，直接執行side effect中的cleanup function

[[React：當元件上註冊了useEffect並觸發unmount上的componentWillUnmount時，無論dependency是什麼，都會執行cleanup，而非side effect]]

#### 總結

React：useEffect註冊在一個元件下，請問元件下的哪些階段會執行useEffect的side effect ？ `mounting階段的componentDidMount、updating階段下的componentDidUpdate`

React：useEffect註冊在一個元件下，請問元件下的哪些階段會觸發useEffect的檢查來執行 ？`updating階段下的componentDidUpdate`

React：useEffect註冊在一個元件下，元件的unmount如何執行useEffect ？ `會無視dependency，直接執行useEffect下的cleanup`


##### 案例：

假設進入登入頁前會先檢查特定儲存空間中是否指定使用者資料，若有就以指定資料來登入；若沒，就重新登入，藉由登入來儲存特定使用者資料至特定儲存空間中。

特定儲存空間為browser storage，這些空間是由瀏覽器內建的，分別為
1. cookie
2. local storage (選擇這個)



```
import React, { useState, useEffect } from 'react';

import Login from './components/Login/Login';
import Home from './components/Home/Home';
import MainHeader from './components/MainHeader/MainHeader';

function App() {
  const [isLoggedIn, setIsLoggedIn] = useState(false);

  useEffect(() => {
    const storedUserLoggedInInformation = localStorage.getItem('isLoggedIn');
    if (storedUserLoggedInInformation === '1') {
      setIsLoggedIn(true);
    }
  }, []);

  const loginHandler = (email, password) => {
    // We should of course check email and password
    // But it's just a dummy/ demo anyways
    localStorage.setItem('isLoggedIn', '1');
    setIsLoggedIn(true);
  };

  const logoutHandler = () => {
    localStorage.removeItem('isLoggedIn');
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


當App這個元件進行mounting來呈現實際DOM時，會註冊著useEffect這個hook：
	- 第一個引數為callback
	- 第二個引數為dependencies，在這裡是空陣列，表示著永不改變的dependency
```
useEffect(callback, [])
```

並於mounting階段下的componentDidMount生命週期函式觸發callback，由於是第一次執行，所以會直接先執行callback，而callback會檢查localStorage的isLoggedIn是否為1，若1就認為是合法使用者在登入，若不是就認為必須要進行登入來寫入isLoggedIn='1'至localStorage

在這裡會沒這筆資料，所以就透過登入的成功來將isLoggedIn='1'寫入至localStorage，之後每一次只要重新進行App的mounting階段：
	- 畫面A 切換成 畫面B (畫面AB都可以一樣和不一樣)
就會直接被系統認定為合法使用者，而引領使用者登入成功的畫面


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

## 複習

#🧠 React：useEffect註冊在一個元件下，請問元件下的哪些階段會執行useEffect的side effect ->->-> `mounting階段的componentDidMount、updating階段下的componentDidUpdate`
<!--SR:!2022-10-01,10,250-->

#🧠 React：useEffect註冊在一個元件下，請問元件下的哪些階段會觸發useEffect的檢查來執行 ->->-> `updating階段下的componentDidUpdate`
<!--SR:!2022-10-25,25,250-->

#🧠 React：useEffect註冊在一個元件下，元件的unmount如何執行useEffect ->->-> `會無視dependency，直接執行useEffect下的cleanup`
<!--SR:!2022-10-25,25,250-->


#🧠 在React中，當元件本身寫上effect hook，請問週期上(mounting、updating、unmounting)會讓effect 有什麼表現 ->->-> `mounting 直接執行effect、updating檢查dependency看是否變動，有變動就先執行cleanup，後看depenedency是否變動來決定執行effect、unmounting 是直接執行cleanup`
<!--SR:!2022-10-04,10,250-->



#🧠 React：若同一個元件因為viewport的畫面切換而發生unmount並重新發生mounting，請問會如何保留新舊的hook? ->->-> `在發生unmount 就會移除舊有effect，並於mounting時期會再次產生額外的effect hook來綁定在該元件，觸發如同上述那樣`
<!--SR:!2022-10-22,25,250-->
`

#🧠 React：當畫面A被切換成畫面B時，unmounting 和 mounting會是如何？ ->->-> `當畫面A被切換成畫面B時，即為畫面A發生unmounting，並且mounting 畫面B`
<!--SR:!2022-10-22,25,250-->

#🧠 React：當畫面A被切換成畫面B時，即為畫面A發生unmounting，並且mounting 畫面B，請問畫面A會和畫面B一樣嗎？->->-> `- 畫面A 和 畫面B 都是畫面A - 畫面A 和 畫面B 都不一樣`
<!--SR:!2022-10-22,25,250-->

#🧠 React：useEffect(a, b) 語法中的a 和 b是什麼？useEffect又是做什麼？ ->->-> `useEffect 語法：會替當前元件註冊effect。第一個引數為callback，第二個引數為設定哪些dependencies 改變才會觸發前面的callback，用陣列表示`
<!--SR:!2022-10-26,28,250-->

#🧠 React：useEffect(callback, dependecies) 產生出來的effect 要何時觸發? ->->-> `會是同個元件的生命週期函式： - mounting階段時的componentDidMount週期函式 - updating階段時的componentDidUpdate 週期函式 `
<!--SR:!2022-10-29,28,250-->


#🧠 React：useEffect(callback, dependecies) 在unmount階段會執行什麼？ ->->-> `useEffect的cleanup函式`
<!--SR:!2022-10-01,10,250-->

#🧠 React：useEffect(callback, dependecies) 在mounting階段時的componentDidMount週期函式會做什麼？ ->->-> `直接執行useEffect的callback`
<!--SR:!2022-10-13,18,250-->

#🧠 React：useEffect(callback, dependecies) 在updating階段時的componentDidUpdate 週期函式會做什麼？->->-> `就會在componentDidUpdate週期檢查dependency是否變動，若有的話，先執行cleanup，在來執行callback，若沒有的話就什麼也不執行`
<!--SR:!2022-10-05,10,250-->



#🧠 React：useEffect(callback, dependecies)中的dependencies沒設定的話，會如何執行callback ->->-> `除了只會在元件的mounting階段下直接執行以外，會在元件的updating觸發並檢查，但檢查結果會是dependency一直變動而直接執行`
<!--SR:!2022-10-24,24,250-->


#🧠 React：useEffect(callback, dependecies)中的dependencies設定空陣列的話，會如何執行callback ->->-> `只會在元件的mounting階段下直接執行，並於元件的updating階段觸發並檢查，但檢查會認為dependency沒在變動而不執行`
<!--SR:!2022-10-26,26,250-->


#🧠 React：useEffect(callback, dependecies)中的dependencies設定成特定內容的話，會如何執行callback  ->->-> `除了只會在元件的mounting階段下直接執行以外，updating階段下觸發，並檢查有任一dependencies是否有變動，有變動就執行，沒變動就不執行。`
<!--SR:!2022-10-25,27,250-->

#🧠 React：useEffect(callback, dependecies) 在unmount階段時的componentWillUnmount週期函式會做什麼？ ->->-> `會無視dependency，直接執行useEffect的cleanup function`
<!--SR:!2022-10-01,10,250-->


#🧠 React：useEffect(callback, dependencies)上的callback和dependencies之間的關係在每個元件的生命週期階段(mounting、unmounting、updating)是如何 ->->-> `在mounting和unmount並不會將dependencies納入使用，只會在updating才納入使用，每當effect觸發時機到了，系統會檢查任一dependency是否變動來決定是否執行callback，若變動就執行；若不變動就不執行`
<!--SR:!2022-10-23,23,250-->

#🧠 React：useEffect(callback, dependencies)上的callback和dependencies之間的關係是哪個階段才能運作->->-> `updating階段下的componentDidUpdate`
<!--SR:!2022-10-02,10,250-->


#🧠 React：useEffect(callback, \[dependencies\]) dependency 主要是指哪些？ ->->-> `定義著callback所需要的狀態、props、其他代表互動且跟著互動而變動的資料`
<!--SR:!2022-10-02,10,250-->


#🧠 React：useEffect(callback, \[dependencies\])  的dependencies 是空陣列的話，會是指什麼？ ->->-> `若是空陣列[] 的話，就等同設定永不改變的dependency`
<!--SR:!2022-10-23,26,250-->


#🧠 React：useEffect(callback, \[dependencies\])  的dependencies 是空的話，會是指什麼？->->-> `若是沒設定任何dependency的話，就等同設定永遠改變的dependency`
<!--SR:!2022-10-22,25,250-->

#🧠 React：useEffect(callback, \[dependencies\]) 在進行mounting的時後，會判斷任一dependency是否變動而執行callback？ ->->-> `並不會，會直接執行callback`
<!--SR:!2022-10-02,10,250-->



#🧠 React：請解釋以下的useEffect案例![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1663250177/blog/react/effect/react-useeffect-example_knoaw1.png)->->-> `當App這個元件進行mounting來呈現實際DOM時，會註冊著useEffect這個hook，並於mounting階段下的componentDidMount生命週期函式觸發callback，由於是第一次執行，所以會直接先執行callback，而callback會檢查localStorage的isLoggedIn是否為1，若1就認為是合法使用者在登入，若不是就認為必須要進行登入來寫入isLoggedIn='1'至localStorage 在這裡會沒這筆資料，所以就透過登入的成功來將isLoggedIn='1'寫入至localStorage，之後每一次只要重新進行App的mounting階段： - 畫面A 切換成 畫面B (畫面AB都可以一樣和不一樣)，就會直接被系統認定為合法使用者，而引領使用者登入成功的畫面`
<!--SR:!2022-10-25,27,250-->

---
Status: #🌱 
Tags:
[[React]]
Links:
[[React：effect 是指除了元件本身所要做的主要功能-渲染元件、與使用者互動來管理狀態以外的額外效果，額外效果會是指脫離渲染週期的任意功能]]
[[React：useEffect cleanup 技術主要是停止當前side effect所產生的非同步任務]]
[[React：當元件上註冊了useEffect並觸發unmount上的componentWillUnmount時，無論dependency是什麼，都會執行cleanup，而非side effect]]
References:
[[@ReactUseEffect]]
[[@ithomeReactJsRuMen20]]