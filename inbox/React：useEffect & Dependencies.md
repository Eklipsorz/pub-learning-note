## 描述



### callback 常見目的


在常見的開發中，useEffect 通常會是產生出觸發元件狀態和渲染的side effect，而callback則是定義side effect的內容。

[[瀏覽器發送後端請求，回應之前，會先有預設畫面瀏覽給客戶端來增加使用體驗，而非等到回應才渲染，隨後等到回應到來後，就重新渲染]]
### dependency 設定目的
```
useEffect(callback, dependency)
```

1. 定義callback 會用來觸發狀態的變數、狀態、props
2. 給予一個手段來防止effect的觸發執行於每次元件的渲染週期內不會產生出無限循環

### dependency 設定的注意事項
[[@academindReactcompleteguidecodeButtonModule]]
> You learned, that you should add "everything" you use in the effect function as a dependency - i.e. all state variables and functions you use in there.
>
> That is correct, but there are a **few exceptions** you should be aware of:

> -   You **DON'T need to add state updating functions** (as we did in the last lecture with `setFormIsValid`): React guarantees that those functions never change, hence you don't need to add them as dependencies (you could though)
    
> -   You also **DON'T need to add "built-in" APIs or functions** like `fetch()`, `localStorage` etc (functions and features built-into the browser and hence available globally): These browser APIs / global functions are not related to the React component render cycle and they also never change
    
> -   You also **DON'T need to add variables or functions** you might've **defined OUTSIDE of your components** (e.g. if you create a new helper function in a separate file): Such functions or variables also are not created inside of a component function and hence changing them won't affect your components (components won't be re-evaluated if such variables or functions change and vice-versa)


> So long story short: You must add all "things" you use in your effect function **if those "things" could change because your component (or some parent component) re-rendered.** That's why variables or state defined in component functions, props or functions defined in component functions have to be added as dependencies!




重點：
- 若useEffect 開發目的是產生出觸發元件狀態和渲染的side effect，那麼dependency 不需要添加的部分：
	- dependency 不需要添加更新狀態用的函式：因為React本身和使用者本身就不會變動該函式本身，所以函式不會被改變
	- dependency 不要添加其他非React能夠支援的API 或者對應函式：因為他們本身就不會改變和跟元件渲染週期無關
	- dependency 不要添加屬於其他元件或者元件以外的變數/函式，因為它們本身就屬於其他元件或者非元件，它們一改變就無法對目前元件觸發渲染，也就不會觸發useEffect。
- 若useEffect 開發目的是產生出觸發元件狀態和渲染的side effect，那麼dependency 就需要添加的部分：
	- dependency 本身一改變就會觸發目前元件下的狀態和渲染：因為他們可透過渲染週期來觸發useEffect

```
    import { useEffect, useState } from 'react';
     
    let myTimer;
     
    const MyComponent = (props) => {
      const [timerIsActive, setTimerIsActive] = useState(false);
	  // using destructuring to pull out specific props values
      const { timerDuration } = props; 
     
      useEffect(() => {
        if (!timerIsActive) {
          setTimerIsActive(true);
          myTimer = setTimeout(() => {
            setTimerIsActive(false);
          }, timerDuration);
        }
      }, [timerIsActive, timerDuration]);
    };
```



## 複習

---
Status: #🌱 #📓 
Tags:
[[React]]
Links:
[[React：effect 使用方式]]
[[React：effect 是指除了元件本身所要做的主要功能-渲染元件、與使用者互動來管理狀態以外的額外效果，額外效果會是指脫離渲染週期的任意功能]]
[[瀏覽器發送後端請求，回應之前，會先有預設畫面瀏覽給客戶端來增加使用體驗，而非等到回應才渲染，隨後等到回應到來後，就重新渲染]]
References:
[[@academindReactcompleteguidecodeButtonModule]]