## 描述
[[@ithomeDay26ReactJinJie]]
這是因為我們先前說過，`useEffect`的執行時間點是這樣:
```
1.  建立、呼叫function component
2.  真正更新DOM
3.  渲染畫面
4.  **呼叫useEffect**
5.  「某個時間點」，偵測到state、props被改變
6.  重新呼叫function component
7.  在virtual DOM比較所有和原始DOM不一樣的地方
8.  真正更新DOM
9.  渲染畫面
10.  **呼叫useEffect**
11.  「某個時間點」，元件被移除
12.  **呼叫useEffect**
```


[[@ithomeDay26ReactJinJie]]
`useLayoutEffect`的執行時間點是這樣:
```
1.  建立、呼叫function component
2.  真正更新DOM
3.  **呼叫useLayoutEffect**
4.  渲染畫面
5.  「某個時間點」，偵測到state、props被改變
6.  重新呼叫function component
7.  在virtual DOM比較所有和原始DOM不一樣的地方
8.  真正更新DOM
9.  **呼叫useLayoutEffect**
10.  渲染畫面
11.  「某個時間點」，元件被移除
12.  **呼叫useLayoutEffect**
```

> ## 同步、畫面渲染前執行的useLayoutEffect

> 雖然這種需求很少，但React提供了一個解決上述問題的hook-`useLayoutEffect`。它和`useEffect`的語法、使用上一模一樣。唯一的差別是`useLayoutEffect`被提升到了渲染畫面前、更新DOM後執行。

重點：
- useEffect 在class-based component中對應觸發執行的時機點為：
	- mounting 階段下的componentDidMount
	- updating 階段下的componentDidUpdate
	- unmounting 階段下的componentWillUnmount

- useLayoutEffect 在class-based component中，本身是負責定義在實際DOM節點進行渲染過程中的Layout階段所觸發的處理，所以都會在都會在渲染畫面前觸發：
	- mounting 階段下的React Update DOM & refs(在實際DOM節點進行渲染過程中的Layout階段)
	- updating 階段下的React Update DOM & refs(在實際DOM節點進行渲染過程中的Layout階段)
	- unmount 階段下的componentWillUnmount


### 以functional component來說


#### useEffect vs. useLayoutEffect 時機點的差異

## 複習

#🧠 useEffect 在class-based component中觸發執行的時機點為 ->->-> `	- mounting 階段下的componentDidMount - updating 階段下的componentDidUpdate - unmounting 階段下的componentWillUnmount`


#🧠 useLayoutEffect 在class-based component中觸發執行的時機點為？ ->->-> `在實際DOM節點進行渲染過程中的Layout階段`


#🧠 useLayoutEffect 在class-based component中觸發執行的時機點是在實際DOM節點進行渲染過程中的Layout階段，具體是什麼？ ->->-> `	- mounting 階段下的React Update DOM & refs(在實際DOM節點進行渲染過程中的Layout階段) - updating 階段下的React Update DOM & refs(在實際DOM節點進行渲染過程中的Layout階段) - unmount 階段下的componentWillUnmount`





---
Status: #🌱 
Tags:
[[React]]
Links:
[[side effect 是指調用者執行特定操作或表達式或函式而得到除了回傳值給調用者這個主要效果以外的額外效果，side effect 通常會是影響主調用者所使用的共享資源之效果]]
[[React：Effect 等同於 Side Effect，effect 本身是指執行主要處理(結果)所帶來的任意額外處理(結果)，主要處理(結果)會是指元件渲染(render)任務。任意額外處理(結果)指useEffect所定義的執行處理]]
References:
[[@ithomeDay26ReactJinJie]]