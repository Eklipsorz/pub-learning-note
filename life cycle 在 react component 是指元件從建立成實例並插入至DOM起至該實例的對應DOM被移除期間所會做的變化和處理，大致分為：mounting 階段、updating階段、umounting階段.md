## 描述


### react： life cycle
[[@w3schoolReactLifecycle]]
> ## Lifecycle of Components
> Each component in React has a lifecycle which you can monitor and manipulate during its three main phases.

重點：
- life cycle 在 react component 是指元件從建立成實例並插入至DOM起至該實例的對應DOM被移除期間所會做的變化和處理，大致分為：
	- mounting 階段
	- updating 階段
	- umounting 階段

#### Mounting
[[@w3schoolReactLifecycle]]
> Mounting means putting elements into the DOM.

mount：
> to fix something to a wall, in a frame, etc., so that it can be looked at or used

> In computers, to mount is to make a group of files in a file system structure accessible to a user or user group

重點：
- mount 命名緣由為將某個東西固定在牆上，以便能夠觀察(讀取/存取)
- 在電腦科學裡，mount 通常是將特定檔案系統上的檔案內容安裝至使用者可方便存取的介面，並讓使用者可透過介面來存取。
- 當元件實例要加入至目前實際DOM結構時，就會進入的階段：
- 概念為：試著將元件轉換成實際DOM節點來插入至目前DOM結構，以便能讓瀏覽器存取該元件。



#### Updating
[[@w3schoolReactLifecycle]]
> The next phase in the lifecycle is when a component is _updated_.
> A component is updated whenever there is a change in the component's `state` or `props`.

[[@reactReactComponentReact]]
> 當 prop 或 state 有變化時，就會產生更新

重點：
- Updating 是 **在歷經Mounting之後，當元件實例因props或者state而引起的畫面渲染** 的階段

#### Unmounting
[[@w3schoolReactLifecycle]]
> The next phase in the lifecycle is when a component is removed from the DOM, or _unmounting_ as React likes to call it.

在電腦科學裡，mount 通常是將特定檔案系統上的檔案安裝至使用者可方便存取的介面，並讓使用者可透過介面來存取

重點：
- umount 是與mount相反的意思
- 在電腦科學裡，umount 通常是將已安裝至使用者可方便存取介面上的檔案內容藉由從介面上移除來讓使用者無法再透過介面來存取檔案內容
- Unmounting 是元件實例要從實際DOM結構中移除對應DOM結構時的階段
- 概念：試著將元件對應的DOM節點從目前DOM結構移除，以便恢復mount之前的狀態

### life cycle 命名緣由

> the series of changes that a living thing goes through from the beginning of its life until death


重點：
- 特定事物從生命開端至生命結尾之間所歷經的一系列改變/處理



## 複習
#🧠 Mount 命名緣由為何？ ->->-> `將某個東西固定在牆上，以便能夠觀察(讀取/存取)`

#🧠 life cycle 命名緣由 ->->-> `特定事物從生命開端至生命結尾之間所歷經的一系列改變/處理`

#🧠 在電腦科學裡，mount 通常是指什麼？ ->->-> `在電腦科學裡，mount 通常是將特定檔案系統上的檔案轉換成可供使用者存取的狀態。`

---
Status: #🌱 
Tags:
[[React]] - [[JavaScript]]
Links:
References:
[[@w3schoolReactLifecycle]]
[[@reactReactComponentReact]]