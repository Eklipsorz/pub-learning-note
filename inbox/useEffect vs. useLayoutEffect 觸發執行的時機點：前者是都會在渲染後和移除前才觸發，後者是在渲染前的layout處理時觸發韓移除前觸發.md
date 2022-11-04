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
- useEffect 觸發執行的時機點為：
	- mounting 階段下的componentDidMount
	- updating 階段下的componentDidUpdate
	- unmounting 階段下的componentWillUnmount

- useLayoutEffect 本身是負責定義在實際DOM節點進行渲染過程中的Layout階段所觸發的處理，所以都會在都會在渲染畫面前觸發：
	- mounting 階段下的React Update DOM & refs(在實際DOM節點進行渲染過程中的Layout階段)
	- updating 階段下的React Update DOM & refs(在實際DOM節點進行渲染過程中的Layout階段)
	- unmount 階段下的componentWillUnmount

## 複習

#🧠 useEffect 觸發執行的時機點為 ->->-> `	- mounting 階段下的componentDidMount - updating 階段下的componentDidUpdate - unmounting 階段下的componentWillUnmount`
<!--SR:!2022-11-05,28,250-->

#🧠 useLayoutEffect 觸發執行的時機點為？ ->->-> `在實際DOM節點進行渲染過程中的Layout階段`
<!--SR:!2022-11-05,28,250-->

#🧠 useLayoutEffect 觸發執行的時機點是在實際DOM節點進行渲染過程中的Layout階段，具體是什麼？ ->->-> `	- mounting 階段下的React Update DOM & refs(在實際DOM節點進行渲染過程中的Layout階段) - updating 階段下的React Update DOM & refs(在實際DOM節點進行渲染過程中的Layout階段) - unmount 階段下的componentWillUnmount`
<!--SR:!2023-01-10,67,250-->




---
Status: #🌱 
Tags:
[[React]]
Links:
References:
[[@ithomeDay26ReactJinJie]]