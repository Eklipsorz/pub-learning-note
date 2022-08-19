## 描述
[[@reacttaiwanReactjsTwMeetup2022]]
Reusable state - React 18 的 useEffect 在 mount 時為何會執行兩次？

https://codesandbox.io/s/heuristic-beaver-ufgfef?file=/src/App.js

> React 預計在未來添加需多新功能們要有一個共同前提約束
> 	- Component 必須要設計得有足夠的彈性來多次 mount & unmount 也不會壞掉

> Offscreen API
> 	 - 讓 React 可以在 UI 切換時保留component 的local state 以及對應的真實DOM elements，像是把他們暫時隱藏起來而不是真的移除它們
> 	 - 當這個component有再次顯示的需求時，就能以之前留下來的state狀態再次mount
> 	 - 舉例在不同的tab切換UI，tab A 切換至 tab B，tab A的對應畫面必須得重新獲取對應的local state和重新渲染

> strict mode + dev env 時會自動mount 兩次，是在模擬 mount => unmount => mount 的過程
> 幫助開發者檢查effect 的設計是否滿足這個彈性的需求



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



重點：
- 從tab A切換至 tab B，此時tab A的畫面和元件都會從mounting 轉換至unmounting
- 當從tab B切換至tab A
## 複習
#🧠 Question :: ->->-> ``

---
Status: #🌱 
Tags:
[[React]] - [[JavaScript]]
Links:
References:
[[@reacttaiwanReactjsTwMeetup2022]]