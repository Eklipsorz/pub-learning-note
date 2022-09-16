
## 目錄位置
[[前端框架放置靜態資源的地方為public和src目錄下的assets，前者並不會受到webpack給處理，後者可能會因模組依賴關係圖而跟著被轉換和處理]]

[[html-webpack-plugin 解決了手動定義哪一份文件是要當前端框架的模板網頁以及得替模板文件手動加載webpack處理後的模組檔案]]



## render

[[React：過度使用wrapper element來解決JSX侷限問題，會產生兩大問題，第一會破壞CSS選擇器所選擇的節點、第二瀏覽器會渲染出不必要出現的HTML元素，甚至會重複渲染]]

[[JSX 侷限一定要有parent element包覆其他元素和最外圍的parent element只能有一個，解法有wrapper element、array]]

[[React：render 函式能夠回傳的JSX Element可以是一般的JSX Element、條件式、陣列形式的JSX Element]]

### debouncing
[[React：useEffect & Dependencies 之間關係就在於每一次effect被觸發時會檢查是否有任一dependency有改變而執行對應的callback]]
[[React：useEffect 使用方式是替當前元件註冊effect這個hook並於每個渲染階段下來判定是否能執行對應的callback]]
[[React：effect 是指除了元件本身所要做的主要功能-渲染元件、與使用者互動來管理狀態以外的額外效果，額外效果會是指脫離渲染週期的任意功能]]
[[React：useEffect cleanup 技術主要是停止當前side effect所產生的非同步任務]]
[[debouncing 在電腦開發實踐的手段，在連續發送事件觸發的場景下，以確保能取得最後的事件觸發資訊的形式來降低請求方和處理方之間的回應速度。]]

[[React：useEffect在面臨連續發送事件觸發或請求的場景下是要取得最後一個請求資訊，那麼勢必得用debouncing才能在減少不必要的浪費下取得最後結果]]

### empty wrapper component
[[empty wrapper component實質上不會有任何對應Virtual DOM和對應實際DOM節點，憑藉著滿足JSX語法上的侷限-要有一個JSX parent 元件來包含子元件來包含(wrap)多個子元件來一次性回傳多個子元件]]

[[React：製作empty wrapper component來替代原本要用div包含的子節點，該wrapper component實際上對應著不存在的Virtual DOM結構，亦即為不會產生對應實際DOM 結構]]
### boolean expression && JSX element

[[在渲染層面下，render 函式回傳的內容若單純添加boolean expression && JSX element 的話，會使其語法正常執行，反之在其基礎下添加其他元素的話，其語法會被視為字串和一般的React Element來看待]]

[[boolean expression && JSX Element案例：混雜其他元件＋boolean expression && JSX Element 未放入到{} vs. 混雜其他元件＋boolean expression && JSX Element 放入到 {}]]

[[React 解析boolean expression && JSX element  時，若前者為true，就以後者的JSX element為主，否則就忽略該Virtual DOM]]


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


## redux

[[React：在還沒有使用Redux之前，parent 元件傳遞資訊至child元件處理是使用props概念來實現，而child元件傳遞資訊給parent元件處理是使用props概念和callback]]

[[為何React要使用Redux]]


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

### CSS
[[React：預設下，每個component 檔案所import的css並不會只限定於component才能使用，而是整個頁面上的元件都能存取]]

[[React：在不使用任何能夠將樣式侷限於元件的技術下，可以使用inline style 和切換class來實現根據使用者輸入是否為空而渲染]]

#### styled-components

[[styled-components 是一個專注將特定CSS樣式綁定在特定元件的第三方套件，其調用的方法會回傳具有特定樣式的元件]]

[[styled-components：在template-literal使用&表示目前透過style.<element> 所建立的元件]]
[[styled-components：在template literal 裡頭添加callback 就能根據props的資訊和狀態更新觸發渲染來動態調整畫面]]

[[styled-components 的目標元件本身是原生HTML DOM元件的話，會把元件標籤上所設定的屬性(attributes)執行賦予至對應實際DOM節點上所擁有的屬性(attribute)]]
[[styled-components：在template literal 添加media query]]


#### CSS modules

[[CSS modules 為webpack的延伸套件，主要會在CSS 檔案 和JS檔案各自分開的情況下，實現讓每個元件都有各自屬於自己的樣式屬性內容]]

[[CSS modules：button 案例 + media query]]

#### styled-components vs. CSS modules

[[Styled-Components 和 CSS modules 之間的差別]]

### condition rendering

[[React：當元件因為conditional rendering集中於同一個元件而變得臃腫，可以試著將負責處理condition rendering的部分抽離出成一個獨立元件，並讓原本元件去載入獨立元件]]

[[React：conditional rendering 是根據執行狀態來調整渲染內容的技術]]


[[React： JSX parser 從JSX語法解析{}時，會從JSX parser換成JS引擎來以expression形式執行{}內的內容]]