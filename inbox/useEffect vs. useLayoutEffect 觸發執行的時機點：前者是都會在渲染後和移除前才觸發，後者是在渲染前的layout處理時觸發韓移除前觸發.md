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


### 產出Virtaul DOM 的 render 至以Real DOM渲染畫面的流程：

1. 呼叫function component 
2. 在virtual DOM比較所有和原始DOM不一樣的地方
3. 真正更新DOM 
4. 瀏覽器根據最新的DOM內容而渲染畫面 (layout、paint)

#### layout 會是什麼

利用現在的樹狀結構來計算網頁元件實際會在頁面上擺放的位置、大小以及如何擺放

#### paint
繪製過程會開始依據渲染樹指定的樣式來對頁面上的pixel來呈現每個元件的真實面貌


### 以functional component的產出Virtaul DOM 的 render 至以Real DOM渲染畫面的流程來說

[[@ithomeDay21UseEffect]]
> 在預設的情況下，**effects 其實會在每次 render 後都被執行**

> 在一般情況下， `useEffect` 會在每次 component render 且瀏覽器完成 DOM 的更新 & 繪製畫面**之後**才執行，以避免阻塞 component render 的過程 & 瀏覽器繪製畫面的過程

理論上useEffect 產生出的side effect 是在產生出Virtual DOM的render之後才執行，但沒有明確說之後是多久的事情，具體會是在
- 瀏覽器根據DOM更新內容而渲染畫面 (layout、paint)之後才執行

而useLayoutEffect 具體則是會在
- 瀏覽器根據DOM更新內容而渲染畫面 (layout、paint)中的layout階段才執行

#### useEffect vs. useLayoutEffect 時機點的差異
1. useEffect 在瀏覽器完成畫面渲染才執行
2. useLayoutEffect 在瀏覽器完成畫面渲染前的layout階段才執行


## 複習


#🧠 React下的產出Virtaul DOM 的 render 至以Real DOM渲染畫面的流程 會是什麼？->->-> `執行對應元件render function、比對virtual dom之間差異、以差異來轉換成real dom並更新現在的real dom tree、瀏覽器根據最新的DOM內容而渲染畫面 (layout、paint)`
<!--SR:!2023-03-28,86,248-->

#🧠 React下的產出Virtaul DOM 的 render 至以Real DOM渲染畫面的流程 會是執行對應元件render function、比對virtual dom之間差異、以差異來轉換成real dom並更新現在的real dom tree、瀏覽器根據最新的DOM內容而渲染畫面 (layout、paint)，其中layout、paint會是什麼？ ->->-> `利用現在的樹狀結構來計算網頁元件實際會在頁面上擺放的位置、大小以及如何擺放、繪製過程會開始依據渲染樹指定的樣式來對頁面上的pixel來呈現每個元件的真實面貌`
<!--SR:!2023-03-27,80,230-->


#🧠 React下的產出Virtaul DOM 的 render 至以Real DOM渲染畫面的流程 會是執行對應元件render function、比對virtual dom之間差異、以差異來轉換成real dom並更新現在的real dom tree、瀏覽器根據最新的DOM內容而渲染畫面，其中的根據最新DOM內容而渲染畫面會包含什麼動作 ->->-> `layout、paint`
<!--SR:!2023-04-12,95,248-->

#🧠 React：useEffect產生出的side effect被定調為render之後才執行，請問render會是什麼？->->-> `產生出對應元件的virtual dom之render function`
<!--SR:!2023-09-15,190,248-->


#🧠 React：理論上useEffect 產生出的side effect 是在產生出Virtual DOM的render之後才執行，但沒有明確說之後是多久的事情，具體會是在什麼時候執行？ ->->-> `瀏覽器根據最新的DOM內容而渲染畫面 (layout、paint)之後執行`
<!--SR:!2023-03-29,87,248-->

#🧠 React：useLayoutEffect 具體則是會在什麼時候執行->->-> `瀏覽器根據最新DOM內容而渲染畫面 (layout、paint)中的layout階段才執行`
<!--SR:!2023-03-26,82,247-->
<!--SR:!2022-11-22,10,250-->

#🧠 React：useLayoutEffect 具體則是會在什麼時候執行->->-> `瀏覽器根據最新DOM內容而渲染畫面 (layout、paint)中的layout階段才執行`
<!--SR:!2023-03-26,82,247-->


#🧠 React：useEffect vs. useLayoutEffect 之間的時機點差異是什麼->->-> `1. useEffect 在瀏覽器完成畫面渲染才執行 2. useLayoutEffect 在瀏覽器完成畫面渲染前的layout階段才執行`
<!--SR:!2023-07-20,155,250-->

#🧠 useEffect 在class-based component中觸發執行的時機點為 ->->-> `	- mounting 階段下的componentDidMount - updating 階段下的componentDidUpdate - unmounting 階段下的componentWillUnmount`
<!--SR:!2023-10-09,204,248-->


#🧠 useLayoutEffect 在class-based component中觸發執行的時機點為？ ->->-> `在實際DOM節點進行渲染過程中的Layout階段`
<!--SR:!2023-07-30,163,250-->


#🧠 useLayoutEffect 在class-based component中觸發執行的時機點是在實際DOM節點進行渲染過程中的Layout階段，具體是什麼？以生命週期來說 ->->-> `	- mounting 階段下的React Update DOM & refs(在實際DOM節點進行渲染過程中的Layout階段) - updating 階段下的React Update DOM & refs(在實際DOM節點進行渲染過程中的Layout階段) - unmount 階段下的componentWillUnmount`
<!--SR:!2023-04-03,83,230-->





---
Status: #🌱 
Tags:
[[React]] - [[useEffect]]
Links:
[[side effect 是指調用者執行特定操作或表達式或函式而得到除了回傳值給調用者這個主要效果以外的額外效果，side effect 通常會是影響主調用者所使用的共享資源之效果]]
[[React：Effect 等同於 Side Effect，effect 本身是指執行主要處理(結果)所帶來的任意額外處理(結果)，主要處理(結果)會是指元件渲染(render)任務。任意額外處理(結果)指useEffect所定義的執行處理]]
References:
[[@ithomeDay26ReactJinJie]]
[[@ithomeDay21UseEffect]]