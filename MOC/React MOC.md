
## 目錄位置
[[前端框架放置靜態資源的地方為public和src目錄下的assets，前者並不會受到webpack給處理，後者可能會因模組依賴關係圖而跟著被轉換和處理]]

[[html-webpack-plugin 解決了手動定義哪一份文件是要當前端框架的模板網頁以及得替模板文件手動加載webpack處理後的模組檔案]]





## data-view-separation

[[React：資料和畫面的切分第一步驟是用{}以及在其內部JavaScript表達式來切分]]



## Offscreen API

[[React ：Offscreen API 是允許Component 在面臨mount=>unmount循環中能夠有效率的切換，並且現在第18版中添增開發時的檢測是否元件的開發都能支援Offscreen API]]



## React.StrictMode

[[React ：Offscreen API 是允許Component 在面臨mount=>unmount循環中能夠有效率的切換，並且現在第18版中添增開發時的檢測是否元件的開發都能支援Offscreen API]]

[[React.StrictMode 是以元件形式來在開發階段檢測其元件包含的內容是否有潛在問題]]



## Component life cycle

[[life cycle 在 react component 是指元件從建立成實例並插入至DOM起至該實例的對應DOM被移除期間所會做的變化和處理，大致分為：mounting 階段、updating階段、umounting階段]]
[[React Unmounting 階段是指特定元件的實際DOM節點從實際DOM Tree被移除的階段]]
[[React Mounting 階段是對應元件轉換成對應DOM結構插入至目前DOM Tree來渲染]]
[[React Unmounting 階段是指特定元件的實際DOM節點從實際DOM Tree被移除的階段]]





## setState
[[React：setState 會試著將多個狀態更新任務合併成一個任務，進而減少因一個任務而觸發一次渲染的渲染次數]]
[[React batching 是將N個狀態更新指令合併成一個指令並只引發一次畫面渲染]]

[[setCount 問題：如何將每一次setCount的要求改變狀態設定為下一次setCount的參數]]

[[React：setState從要求更改狀態至完成狀態改變&渲染之間是有時間差，若面對大量更改狀態要求的情況下，會使得時間差加重]]

## props
[[React：在還沒有使用Redux之前，parent 元件傳遞資訊至child元件處理是使用props概念來實現，而child元件傳遞資訊給parent元件處理是使用props概念和callback]]



## component

[[React：dumb component 本身負責接收資訊來渲染內容的元件，並不負責改變其他元件的渲染內容，smart component是相對於dumb component，會負責控管child component的狀態並根據互動結果來改變child component]]

[[React：stateful component 是指本身註冊狀態以及對應狀態更新用函式，stateless component則是指本身沒有註冊狀態和沒註冊更新狀態用的函式]]

[[React： controlled component & uncontrolled component 是形容表單元件，uncontrolled component是以原生DOM節點來獲取狀態&根據狀態渲染，controlled component 是以React體系的state、setState來實現儲存狀態和根據狀態]]