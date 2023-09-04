## 描述
[[@reacttaiwanReactjsTwMeetup2022]]
> Reusable state - React 18 的 useEffect 在 mount 時為何會執行兩次？
> https://codesandbox.io/s/heuristic-beaver-ufgfef?file=/src/App.js
> React 預計在未來添加需多新功能們要有一個共同前提約束
> 	- Component 必須要設計得有足夠的彈性來多次 mount & unmount 也不會壞掉

> Offscreen API
> 	 - 讓 React 可以在 UI 切換時保留component 的local state 以及對應的真實DOM elements，像是把他們暫時隱藏起來而不是真的移除它們
> 	 - 當這個component有再次顯示的需求時，就能以之前留下來的state狀態再次mount
> 	 - 舉例在不同的tab切換UI，tab A 切換至 tab B，tab A的對應畫面必須得重新獲取對應的local state和重新渲染

> strict mode + dev env 時會自動mount 兩次，是在模擬 mount => unmount => mount 的過程
> 幫助開發者檢查effect 的設計是否滿足這個彈性的需求


[[@zhuanjiabrickspertYiPianDaiGeiNiReact18]]
> # 更新`严格模式`

> 在未来，React 想要在保存 `state` 的同时可以添加和移除 UI 块。例如，一个面板上，用户使用 `tab`可以快速地从 `A` 面板切换到 `B` 面板，而我希望在切换到 `B` 面板的时候，可以保留 `A` 面板的 `state`，这样在切回来的时候，我就可以即时地去渲染之前的那个页面。为了做到这一点，React 在 `unmount` 和 `mount` 时使用的是相同的组件 `state`。

> 这样的特性可以提高 React 的性能，但是这同样要求组件对于频繁的 `mount` 和 `unmount` 产生的`effects` 有能够灵活处理的能力。大多数的 `effects` 都不会造成任何改变和影响，但是有一些 `effects` 会认为组件只会被 `mount` 和销毁一次。

> 为了解决这些问题，React 18 对于 `Strict Mode` 介绍了一种 `development-only` 这种检查机制。这种检查会自动 `mount` 或者 `unmount` 每一个组件，无论是组件第一次被 `mount`，还是组件已经被 `mount` 过一次，保存了之前的 `state`，从而第二次被 `mount`。

> 在这次改变之前，React 会 `mount` 组件并创建下面这种 `effects`。

```javascript
* React mounts the component.
    * Layout effects are created.
    * Effect effects are created.
```
  

在 React 18 的 `Strict Mode` 中，React 会在 `development mode` 中模拟 `unmount` 和 `remount`。

```javascript
* React mounts the component.
    * Layout effects are created.
    * Effect effects are created.
* React simulates unmounting the component.
    * Layout effects are destroyed.
    * Effects are destroyed.
* React simulates mounting the component with the previous state.
    * Layout effect setup code runs
    * Effect setup code runs
```


### 針對支援Offscreen API的Component所做的檢測


React 未來會朝著遵守以下規則來添加新功能：
	- Component 在面對多次的 mount => unmount => mount 的循環中仍然保有原有元件的業務邏輯功能和渲染內容
目前已知會與這規則起衝突的語法為：
	- 當使用Offscreen API開發Component時，Component上的大部分effects實現會面對同個元件的mount->unmount->mount下保留其功能，但少部份effects實現則會是認為元件只會有一次mount->unmount的，而導致同個元件只要unmount後就銷毀effect，接著再次以緩存來mount的時候就無法正常使用。
新功能預計會有：
	- Offscreen API
面對這規則會在開發階段中可以添加React.StrictMode元件進行相關檢測
	- 當在React.StrictMode元件下加入新元件 A 並做完mounting時，React.StrictMode會替該mounting的元件 A暫存其狀態和實際DOM結構，然後再自行unmounting 新元件 A，然後再以暫存內容來再次進行其元件A的mounting。
	- 過程中會檢測其元件上的effect是否正常運作


#### Offscreen API是什麼

重點：
- Offscreen API 是指在要切換另一個畫面B前，能夠暫存目前所顯示的畫面A，並將其畫面移動至人們看不到的地方，以方便渲染其他畫面B，等到要渲染畫面A時，就將以畫面A的暫存內容來快速渲染
- 具體會是
	- 在要切換另一個畫面B前，就暫存讓目前畫面A上的元件它們各自的狀態以及他們所對應的實際DOM結構
	- 從目前DOM Tree那 unmount 目前畫面A的元件所對應的實際DOM 結構
	- mount 畫面B上的元件所對應的實際DOM結構至目前DOM Tree
	- 等到下一次切回畫面A時，就透過暫存的狀態和現有對應DOM結構快速在DOM結構再mount一遍畫面A上的元件，以節省得到狀態和對應DOM結構的時間
- 適用場景為：
	- 多個tab共享同一個顯示元件，並藉由點擊特定tabA來mounting 對應元件A，然後又想點擊另一個tab B的那麼就unmounting 對應元件A以及mounting 對應元件B，接著又點回tab A就又得unmounting 對應元件B和mounting 對應元件A
	- 多個元件A共享著同一個用來顯示其元件對應畫面的元件B：每個元件A都有對應的渲染內容，但只會有一個元件A的對應渲染內容呈現在元件B上。
	- 若是實現多個元件都各有一個顯示元件，那麼就朝著優化網頁對於瀏覽器的效能
好處為：
	- 在mount=>unmount的循環場景，藉由切換前的緩存來提高畫面切換的效率
	


### offscreen 命名緣由

off-screen
> off the screen, or above, below, or at the side of the screen, so that the people who are watching cannot see 

重點：
- offscreen 是指將螢幕的畫面移動至人們看不到的地方
## 複習
#🧠 offscreen 命名緣由是什麼 ->->-> `螢幕的畫面移動至人們看不到的地方`
<!--SR:!2024-01-23,315,250-->

#🧠 React：Offscreen API是什麼樣的概念？  ->->-> `指在要切換另一個畫面B前，能夠暫存目前所顯示的畫面A，並將其畫面移動至人們看不到的地方，以方便渲染其他畫面B，等到要渲染畫面A時，就將以畫面A的暫存內容來快速渲染`
<!--SR:!2023-12-05,92,230-->

#🧠 React：Offscreen API 具體如何實現其概念？(請以畫面A的元件和畫面B的元件來舉例) ->->-> `在要切換另一個畫面B前，就暫存讓目前畫面A上的元件它們各自的狀態以及他們所對應的實際DOM結構、從目前DOM Tree那 unmount 目前畫面A的元件所對應的實際DOM 結構、mount 畫面B上的元件所對應的實際DOM結構至目前DOM Tree、等到下一次切回畫面A時，就透過暫存的狀態和現有對應DOM結構快速在DOM結構再mount一遍畫面A上的元件，以節省得到狀態和對應DOM結構的時間`
<!--SR:!2023-12-13,289,250-->

#🧠 React：Offscreen API  能帶來什麼好處？ ->->-> `在mount=>unmount的循環場景，藉由切換前的緩存來提高畫面切換的效率`
<!--SR:!2023-06-08,179,250-->

#🧠 React：Offscreen API  會應用什麼場景 ->->-> `多個tab共享同一個顯示元件，並藉由點擊特定tabA來mounting 對應元件A，然後又想點擊另一個tab B的那麼就unmounting 對應元件A以及mounting 對應元件B，接著又點回tab A就又得unmounting 對應元件B和mounting 對應元件A、多個元件A共享著同一個用來顯示其元件對應畫面的元件B：每個元件A都有對應的渲染內容，但只會有一個元件A的對應渲染內容呈現在元件B上。`
<!--SR:!2024-04-23,370,250-->

#🧠  React：Offscreen API 應用至多個元件和只有一個顯示其他元件內容用的顯示元件，那麼會帶來什麼好處？ ->->-> `那麼就朝著優化網頁對於瀏覽器的效能`
<!--SR:!2023-07-26,197,230-->

#🧠 React：為了能添加Offscreen API 來給Component支援，必須要讓Component開發上遵守什麼？  ->->-> `Component 在面對多次的 mount => unmount => mount 的循環中仍然保有原有元件的業務邏輯功能和渲染內容`
<!--SR:!2024-10-30,484,250-->



#🧠 React：為了確保預計要支援Offscreen API的Component是能夠正常運行effects實現，會做React.StrictMode元件進行相關檢測，其檢測內容為？ ->->-> `當在React.StrictMode元件下加入新元件 A 並做完mounting時，React.StrictMode會替該mounting的元件 A暫存其狀態和實際DOM結構，然後再自行unmounting 新元件 A，然後再以暫存內容來再次進行其元件A的mounting。、過程中會檢測其元件上的effect是否正常運作`
<!--SR:!2024-07-31,432,250-->


---
Status: #🌱 
Tags:
[[React]] - [[JavaScript]]
Links:
[[React.StrictMode 是以元件形式來在開發階段檢測其元件包含的內容是否有潛在問題]]
References:
[[@reacttaiwanReactjsTwMeetup2022]]
[[@zhuanjiabrickspertYiPianDaiGeiNiReact18]]