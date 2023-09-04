## 描述






### effect 使用方法
[[React：Effect 等同於 Side Effect，effect 本身是指執行主要處理(結果)所帶來的任意額外處理(結果)，主要處理(結果)會是指元件渲染(render)任務。任意額外處理(結果)指useEffect所定義的執行處理]]

side effect / effect 本身指由主要任務所帶來的任意額外任務，也就是系統執行完Render之後所要接著執行的任意額外任務，而useEffect 正是定義該任意額外任務





#### effect 使用語法
`useEffect(callback, [dependencies])`

useEffect 語法：
- 第一個引數為callback，主要定義side effect的任務內容
- 第一個引數的callback會回傳一個cleanup function，且每一次effect從那獲取對應cleanup function並在那執行指定清除上一次side effect所產生的影響 ，**好保證effect指定任務無論隨著render執行了多少次，effect都能按照資料來正確呈現和正常運作，不會因為上一個effect的影響結果而無法正常/正確呈現**，通常手段會是**清除上一次side effect所產生的非同步任務** 
	- 該cleanup function 盡量別以asynchronous function來處理，理由有一個：
		- 會無法正常執行，由於async function會將回傳內容以promise object來包裝，但useEffect並不支援提取promise object回傳的function來執行
> a function that should be executed AFTER every component evaluation IF the specified dependencies changes
-  第二個引數為設定哪些dependencies 改變才會觸發前面的callback，會用陣列來表示所有的dependencies
[[React：擁有deps 機制的hook  想運用互動狀態的資訊來當deps之注意事項]]
> dependencies of this effect - the function only runs if the dependencies changed

##### useEffect 的callback不能是async的原因

[[@HowUseAsync]]
```
// ❌ don't do this
useEffect(async () => {
  const data = await fetchData();
}, [fetchData])
```


> The issue here is that the first argument of `useEffect` is supposed to be a function that returns either nothing (`undefined`) or a function (to clean up side effects). But an async function returns a Promise, which can't be called as a function! It's simply not what the `useEffect` hook expects for its first argument.

> ## Write the asynchronous function inside the `useEffect`

> Usually the solution is to simply write the data fetching code inside the `useEffect` itself, like so:

```jsx
useEffect(() => {
  // declare the data fetching function
  const fetchData = async () => {
    const data = await fetch('https://yourapi.com');
  }

  // call the function
  fetchData()
    // make sure to catch any error
    .catch(console.error);
}, [])
```


重點：
- useEffect 預期callback會是回傳函式物件，但async會使得回傳promise 物件，這會無法正常執行
- 若要運用async/await語法，替代方案為在callback內部定義async function來進行



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
[[@ithomeDay21UseEffect]]
> 在預設的情況下，**effects 其實會在每次 render 後都被執行**。

0. effects 會是在每次render之後被執行
1. 在mounting 階段進行useEffect的hook綁定，並因為render執行完畢會連帶執行side effect，接著將指定dependency事先儲存下來，好做下一次的比較
	- 此時沒有dependency事先儲存，所以也就不需要檢查dependency
	- 這是第一次執行side effect，本身就沒有上一個side effect，所以就不需要執行cleanup
2. 在updating 階段，執行到useEffect時就拿目前deps內容和上一次effect所儲存的deps進行比對，看是否一樣：
		- 若不一樣，就儲存這次deps資訊好下次比對
			- render執行完畢後就開始執行side effect
			- 執行side effect對應的cleanup 
			- 執行side effect的主體-callback
			- 設定對應cleanup任務來好方便下次清除這次side effect造成的影響
		- 若一樣：
			- 當前render之後不執行任何side effect
3. 在unmounting 階段，就會無視dependency，直接執行useEffect的cleanup function 來清除最後一次side effect造成的影響
		- unmount 階段就沒render，所以也就沒有side effect

[[React：當元件上註冊了useEffect並觸發unmount，無論dependency是什麼，都會執行cleanup，而非side effect]]

### 在unmount階段時是無視dependency，直接執行useEffect的cleanup function，為何要執行cleanup？

`避免unmount之後還殘留side effect影響在那，所以要執行cleanup來還原`


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


#🧠 React：useEffect 會是什麼？ ？ ->->-> `定義著執行完Render之後所要接著執行的任意額外任務`
<!--SR:!2024-02-25,286,250-->

#🧠 React：useEffect的side effect 在 render 上來說是什麼？->->-> `render執行完畢所應該要有的處理`
<!--SR:!2023-09-14,195,250-->


#🧠 React：useEffect的side effect 在 render 上來說是render執行完畢所應該要有的處理，那麼render和side effect之間的存在關係是什麼？->->-> `有render就會有side effect`
<!--SR:!2023-08-10,171,250-->

#🧠 React：useEffect 語法是什麼？->->-> `useEffect(callback, [dependencies]`
<!--SR:!2024-06-19,355,250-->

#🧠 React：useEffect 的cleanup function 通常手段會是什麼？->->-> `通常手段會是**清除上一次side effect所產生的非同步任務** `
<!--SR:!2023-11-02,210,230-->

#🧠 React：useEffect(a, b) 語法中的a 是什麼 ->->-> `第一個引數為callback，主要定義side effect的任務內容`
<!--SR:!2023-09-12,193,250-->

#🧠  React：useEffect(a, b) 語法中的a 會回傳什麼？做什麼？ ->->-> `第一個引數的callback會回傳一個cleanup function，且每一次effect從那獲取對應cleanup function並在那執行指定清除上一次side effect所產生的影響`
<!--SR:!2023-09-11,192,250-->

#🧠  React：useEffect 的cleanup 是用來做什麼？ ->->-> `cleanup function並在那執行指定清除上一次side effect所產生的影響`
<!--SR:!2023-09-14,195,250-->


#🧠 React：useEffect 的cleanup 是清除上一次side effect所產生的影響，為何要清除？->->-> `好保證effect指定任務無論隨著render執行了多少次，effect都能按照資料來正確呈現和正常運作，不會因為上一個effect的影響結果而無法正常/正確呈現`
<!--SR:!2024-03-21,300,250-->


#🧠 React：useEffect(a, b) 語法中的b 是什麼 ->->-> `第二個引數為設定哪些dependencies 改變才會觸發前面的callback，會用陣列來表示所有的dependencies`
<!--SR:!2024-01-31,270,250-->



#🧠 React：useEffect 本身在functional component會像是什麼？主要會做什麼 ->->-> `useEffect 語法：functional component 是像是function呼叫執行useEffect呼叫，其中會替當前元件註冊effect`
<!--SR:!2024-10-04,416,250-->



#🧠 React：useEffect(callback, dependecies) 產生出來的effect 在理論上會何時執行? ->->-> `effects 會是在每次render之後被執行`
<!--SR:!2024-01-21,202,248-->
<!--SR:!2023-07-21,157,250-->

#🧠 React：useEffect(callback, dependecies) 產生出來的effect 在理論上會何時執行? ->->-> `effects 會是在每次render之後被執行`
<!--SR:!2024-01-21,202,248-->


#🧠 React：useEffect(callback, dependecies) 產生出來的effect會是在每次render之後被執行，在mounting階段會是做什麼？->->-> `在mounting 階段進行useEffect的hook綁定，並因為render執行完畢會連帶執行side effect，接著將指定dependency事先儲存下來，好做下一次的比較`
<!--SR:!2023-11-11,81,210-->


#🧠 React：useEffect(callback, dependecies) 產生出來的effect會是在每次render之後被執行，在mounting階段會是直接執行side effect，而沒比較deps，為什麼？ ->->-> `此時沒有dependency事先儲存，所以也就不需要檢查dependency`
<!--SR:!2023-07-08,149,250-->

#🧠 React：useEffect(callback, dependecies) 產生出來的effect會是在每次render之後被執行，在mounting階段會是直接執行side effect，而沒執行cleanup，為什麼？ ->->-> `這是第一次執行side effect，本身就沒有上一個side effect，所以就不需要執行cleanup`
<!--SR:!2023-08-03,168,250-->


#🧠 React：useEffect(callback, dependecies) 在unmount階段會執行什麼？ ->->-> `useEffect的cleanup函式`
<!--SR:!2024-10-29,439,250-->




#🧠 React：useEffect(callback, dependecies) 產生出來的effect會是在每次render之後被執行，在updating階段會是做什麼？->->-> `在updating 階段，執行到useEffect時就拿目前deps內容和上一次effect所儲存的deps進行比對，看是否一樣： - 若不一樣，就儲存這次deps資訊好下次比對 - render執行完畢後就開始執行side effect - 執行side effect對應的cleanup  - 執行side effect的主體-callback - 設定對應cleanup任務來好方便下次清除這次side effect造成的影響 - 若一樣：- 當前render之後不執行任何side effect`
<!--SR:!2024-01-07,199,230-->


#🧠 React：useEffect(callback, dependecies) 產生出來的effect會是在每次render之後被執行，在updating階段會是執行到useEffect時就拿目前deps內容和上一次effect所儲存的deps進行比對，看是否一樣，若不一樣的話，會是做什麼？ ->->-> ` 若不一樣，就儲存這次deps資訊好下次比對 - render執行完畢後就開始執行side effect - 執行side effect對應的cleanup  - 執行side effect的主體-callback - 設定對應cleanup任務來好方便下次清除這次side effect造成的影響 `
<!--SR:!2024-05-17,271,230-->


#🧠 React：useEffect(callback, dependecies) 產生出來的effect會是在每次render之後被執行，在updating階段會是執行到useEffect時就拿目前deps內容和上一次effect所儲存的deps進行比對，看是否一樣，若一樣的話，會是做什麼？ ->->-> ` 若一樣：- 當前render之後不執行任何side effect`
<!--SR:!2023-09-09,192,250-->


#🧠 React：useEffect(callback, dependecies)中的dependencies沒設定的話，會如何執行callback ->->-> `除了只會在元件的mounting階段下直接執行以外，會在元件的updating觸發並檢查，但檢查結果會是dependency一直變動而直接執行`
<!--SR:!2025-01-02,486,250-->



#🧠 React：useEffect(callback, dependecies)中的dependencies設定空陣列的話，會如何執行callback ->->-> `只會在元件的mounting階段下直接執行，並於元件的updating階段觸發並檢查，但檢查會認為dependency沒在變動而不執行`
<!--SR:!2023-08-21,180,250-->



#🧠 React：useEffect(callback, dependecies)中的dependencies設定成特定內容的話，會如何執行callback  ->->-> `除了只會在元件的mounting階段下直接執行以外，updating階段下觸發，並檢查有任一dependencies是否有變動，有變動就執行，沒變動就不執行。`
<!--SR:!2023-08-14,174,250-->

#🧠 React：useEffect(callback, dependecies) 在unmount階段時？ ->->-> `會無視dependency，直接執行useEffect的cleanup function`
<!--SR:!2023-07-08,147,250-->

#🧠 React：useEffect(callback, dependecies) 在unmount階段時是無視dependency，直接執行useEffect的cleanup function，為何要執行cleanup？  ->->-> `避免unmount之後還殘留side effect影響在那，所以要執行cleanup來還原`
<!--SR:!2023-06-08,128,250-->



#🧠 React：useEffect(callback, dependencies)上的callback和dependencies之間的關係在每個元件的生命週期階段(mounting、unmounting、updating)是如何 ->->-> `在mounting和unmount並不會將dependencies納入使用，只會在updating才納入使用，每當effect觸發時機到了，系統會檢查任一dependency是否變動來決定是否執行callback，若變動就執行；若不變動就不執行`
<!--SR:!2023-05-18,148,250-->

#🧠 React：useEffect(callback, dependencies)上的callback和dependencies之間的關係是哪個階段才能運作->->-> `updating階段下`
<!--SR:!2023-08-21,178,250-->

#🧠  React：useEffect(callback, dependencies)在unmount階段沒辦法執行side effect? ->->-> `unmount 階段就沒render，所以也就沒有side effect`
<!--SR:!2023-08-16,176,250-->


#🧠 React：useEffect(callback, \[dependencies\]) dependency 主要是指哪些？ ->->-> `定義著callback所需要的狀態、props、其他代表互動且跟著互動而變動的資料`
<!--SR:!2023-12-08,103,230-->


#🧠 React：useEffect(callback, \[dependencies\])  的dependencies 是空陣列的話，會是指什麼？ ->->-> `若是空陣列[] 的話，就等同設定永不改變的dependency`
<!--SR:!2023-09-12,193,250-->



#🧠 React：useEffect(callback, \[dependencies\])  的dependencies 是空的話，不是指空陣列，會是指什麼？->->-> `若是沒設定任何dependency的話，就等同設定永遠改變的dependency`
<!--SR:!2024-01-08,227,230-->


#🧠 React：useEffect(callback, \[dependencies\]) 在進行mounting的時候，會判斷任一dependency是否變動而執行callback？ ->->-> `並不會，會直接執行callback`
<!--SR:!2024-10-25,432,250-->




#🧠 React：請解釋以下的useEffect案例![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1663250177/blog/react/effect/react-useeffect-example_knoaw1.png)->->-> `當App這個元件進行mounting來呈現實際DOM時，會註冊著useEffect這個hook，並於mounting階段下的componentDidMount生命週期函式觸發callback，由於是第一次執行，所以會直接先執行callback，而callback會檢查localStorage的isLoggedIn是否為1，若1就認為是合法使用者在登入，若不是就認為必須要進行登入來寫入isLoggedIn='1'至localStorage 在這裡會沒這筆資料，所以就透過登入的成功來將isLoggedIn='1'寫入至localStorage，之後每一次只要重新進行App的mounting階段： - 畫面A 切換成 畫面B (畫面AB都可以一樣和不一樣)，就會直接被系統認定為合法使用者，而引領使用者登入成功的畫面`
<!--SR:!2023-07-06,182,250-->

#🧠 React：useEffect(callback, deps) 中的callback回傳的是什麼？會由誰處理？ ->->-> `主要會回傳cleanup function，由React來執行`
<!--SR:!2023-09-12,193,250-->


#🧠  React：useEffect(callback, deps) 中的callback若是asynchronous 的話，會有什麼問題？ ->->-> `會無法正常執行cleanup`
<!--SR:!2024-03-15,255,248-->

#🧠 React：useEffect(callback, deps) 中的callback若是asynchronous 的話，會有無法正常執行cleanup，主因會是什麼？ ->->-> `由於async function會將回傳內容以promise object來包裝，但useEffect並不支援提取promise object回傳的function來執行`
<!--SR:!2023-07-07,104,248-->

#🧠 React：useEffect(callback, deps) 中的callback得是sync？還是async?  為什麼？->->-> `由於async function會將回傳內容以promise object來包裝，但useEffect並不支援提取promise object回傳的function來執行`
<!--SR:!2024-06-11,299,248-->

#🧠 React：useEffect(callback, deps) 若要求callback能夠使用async/await語法，但callback本身不能是async，其替代方案為何 ->->-> `在callback內部定義另一個async function來使用`
<!--SR:!2023-11-05,62,228-->


---
Status: #🌱 
Tags:
[[React]] - [[useEffect]]
Links:
[[side effect 是指調用者執行特定操作或表達式或函式而得到除了回傳值給調用者這個主要效果以外的額外效果，side effect 通常會是影響主調用者所使用的共享資源之效果]]
[[React：Effect 等同於 Side Effect，effect 本身是指執行主要處理(結果)所帶來的任意額外處理(結果)，主要處理(結果)會是指元件渲染(render)任務。任意額外處理(結果)指useEffect所定義的執行處理]]
[[React：useEffect cleanup 技術主要是停止當前side effect所產生的非同步任務]]
[[React：當元件上註冊了useEffect並觸發unmount，無論dependency是什麼，都會執行cleanup，而非side effect]]
References:
[[@HowUseAsync]]
[[@ReactUseEffect]]
[[@ithomeDay21UseEffect]]