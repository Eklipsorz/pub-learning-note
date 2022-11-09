
## 目錄位置
[[前端框架放置靜態資源的地方為public和src目錄下的assets，前者並不會受到webpack給處理，後者可能會因模組依賴關係圖而跟著被轉換和處理]]

[[html-webpack-plugin 解決了手動定義哪一份文件是要當前端框架的模板網頁以及得替模板文件手動加載webpack處理後的模組檔案]]



## render

[[React：過度使用wrapper element來解決JSX侷限問題，會產生兩大問題，第一會破壞CSS選擇器所選擇的節點、第二瀏覽器會渲染出不必要出現的HTML元素，甚至會重複渲染]]

[[JSX 侷限一定要有parent element包覆其他元素和最外圍的parent element只能有一個，解法有wrapper element、array]]

[[React：render 函式能夠回傳的JSX Element可以是一般的JSX Element、條件式、陣列形式的JSX Element]]

### debouncing
[[React：useEffect & Dependencies 之間關係就在於每一次在updating階段時effect被觸發時會檢查是否有任一dependency有改變而執行對應的callback]]
[[React：useEffect 使用方式是替當前元件註冊effect這個hook並於每個渲染階段下來判定是否能執行side effect]]
[[React：Effect 等同於 Side Effect，effect 本身是指執行主要處理(結果)所帶來的任意額外處理(結果)，主要處理(結果)會是指元件渲染(render)任務。任意額外處理(結果)指useEffect所定義的執行處理]]
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

[[React：在還沒有使用Redux或者Context之前，parent 元件傳遞資訊至child元件處理是使用props概念來實現，而child元件傳遞資訊給parent元件處理是使用props概念和callback]]

[[React：使用如Redux或者Context這種集中狀態機制是為了讓多個元件下能夠彼此共享狀態和彼此觸發渲染週期]]


## setState
[[React：setState 會試著將多個狀態更新任務合併成一個任務，進而減少因一個任務而觸發一次渲染的渲染次數]]
[[React batching 是將N個狀態更新指令合併成一個指令並只引發一次畫面渲染]]

[[setCount 問題：如何將每一次setCount的要求改變狀態設定為下一次setCount的參數]]

[[React：setState從要求更改狀態至完成狀態改變&渲染之間是有時間差，若面對大量更改狀態要求的情況下，會使得時間差加重]]

## props
[[React：在還沒有使用Redux或者Context之前，parent 元件傳遞資訊至child元件處理是使用props概念來實現，而child元件傳遞資訊給parent元件處理是使用props概念和callback]]


## React.memo

[[React.memo 效能成本取決於儲存空間成本和計算成本，前者會是props數量、對應元件的Virtual DOM結構、其descendant component的Virtual DOM結構，後者會是props比對成本]]

[[React.memo 比對方式會採用於JS的currProp === prevProp 而衍生出props對應著物件的元件a會因為渲染函式一直邊呼叫邊重建物件而無法讓元件a能夠正常使用memo]]

[[React.memo 適用場景為不常變更的元件內容、規模較大的專案，不適用場景為時常變更的元件、props為基礎來重複使用的元件、規模較小的專案]]

[[React：React.memo 將特定props之指定元件A的對應Virtual DOM儲存在緩存或者記憶體中，並比較每一次渲染觸發時的props資訊是否和儲存記憶體的資訊一致，一致就用記憶體，不一致就執行function]]



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



## useEffect
[[React：useEffect 使用方式是替當前元件註冊effect這個hook並於每個渲染階段下來判定是否能執行side effect]]

[[React：當元件上註冊了useEffect並觸發unmount，無論dependency是什麼，都會執行cleanup，而非side effect]]

[[React：useEffect在面臨連續發送事件觸發或請求的場景下是要取得最後一個請求資訊，那麼勢必得用debouncing才能在減少不必要的浪費下取得最後結果]]

[[side effect 是指調用者執行特定操作或表達式或函式而得到除了回傳值給調用者這個主要效果以外的額外效果，side effect 通常會是影響主調用者所使用的共享資源之效果]]

[[React：useEffect & Dependencies 之間關係就在於每一次在updating階段時effect被觸發時會檢查是否有任一dependency有改變而執行對應的callback]]

[[React：useEffect cleanup 技術主要是停止當前side effect所產生的非同步任務]]


## useReducer

[[React： 針對useReducer 所擁有的大狀態下的一小部分狀態來作為useEffect的depenedency，並且它們只要變動的話，就會在updating階段觸發時檢查到dependency變動而執行callback]]

[[React：useReducer 是React 內建的HOOK，最主要是以多個狀態歸納成一個大狀態 的方式來控管狀態]]
[[useState使用場景運用在狀態間並無關係且狀態更新較為單一簡單，useReducer使用場景運用在狀態間有關係且狀態更新較為複雜]]

[[React：使用useState 來管理多個狀態的潛在問題會容易衍生難以控管、維護狀態且bug眾多的代碼]]

[[(待研究)React：若component上的console在useReducer之後和之前，其印出的資訊順序皆為不同]]


## useContext

[[React：Context API擁有context object、provider、consumer，最前者為定義狀態的環境，中間者為提供狀態值給予最前者的一方，最後者為使用該環境的一方]]

[[React：Context 是定義某個事物A的環境，xxxx-wide則是定義xxxx所指的區域之範圍內]]

[[React：dynamic context 是指在執行過程根據執行狀況來更改context的當前值，方法有將更新狀態用的函式添加至對應的context object中的provider component]]

[[React：Context 侷限為目前沒有針對狀態上的高頻率變動做出較為優化的實現，目前停留在適用於狀態變動頻率較低的場景下]]

[[React：若要重構Context可以從IDE auto-completion和抽離來下手，後者是從Components抽離出專門處理Context相關狀態的Component和渲染對應畫面的Component]]

[[React：狀態、更新狀態函式的資料傳遞方式有使用props所建立的props chain和使用context，前者場景為將元件轉換成可重複使用的元件，後者場景為元件間傳遞過程要經歷過多的元件]]

[[React：使用如Redux或者Context這種集中狀態機制是為了讓多個元件下能夠彼此共享狀態和彼此觸發渲染週期]]

[[React：在還沒有使用Redux或者Context之前，parent 元件傳遞資訊至child元件處理是使用props概念來實現，而child元件傳遞資訊給parent元件處理是使用props概念和callback]]

[[React updating 階段是歷經過Mounting階段所觸發元件內上的渲染，大致分為三個部分：New props、setState、forceUpdate]]

[[consumer component 並不會主動監測，只會等到搭載consumer component的元件被觸發渲染並監測內容是否有變動，有變動就把使用該內容的元件跟著一起渲染更新，沒變動就不動]]

## ref

[[React：useImperativeHandle 是定義一組以DOM原生渲染指令為主的處理來賦予至對應ref物件的current屬性]]

[[React：forwardRef + useImperativeHandler 實現由parent元件的ref去呼叫child元件所提供的方法]]



## class-based component

[[class-based component 的狀態通常會以物件來囊括元件下的所有狀態，而functional component的狀態透過useState可以建立多個獨立的狀態，而非集中在物件上]]
[[class-based-component：Uses轉換成class-based-component的過程]]
[[functional component寫法流行是因為彈性、短小、易讀；class-based component則是個人喜好、工作團隊、建立error boundary]]
[[React componentDidUpdate 是每個元件都會有的內建生命週期函式，最主要是定義渲染內容更新後要做什麼]]
[[React Element 主要有兩種開發方法：第一個是functional component；第二個則是class-based component]]
[[React：class-based component 存取context object的方法有兩種-第一個是使用consumer；第二個是使用元件類別下的contextType屬性 + this.context.xxx 來存取]]
[[React：useEffect 對於class-based-component的轉換案例- UserFinder.js 的class-based component 實現]]
[[useEffect 在class-based component 的實現是在compoentDidMount、componentDidUpdate、componentWillUnmount來進行對應的實現]]
[[import { Component } from 'react'; 的用途為方便讓特定元件繼承React的通用元件類別和react element所會需要方法和屬性]]



### Form


#### validation：when form is submitted

[[React：在表格提交事件中，validity和value無法說明元件下的所有狀態，致使沿用兩者會出現預期外的結果，解法為提出額外狀態-touched]]

[[React：在表格提交事件中，表格提交非法輸入欄內容時會有的處理]]

[[React ：在表格提交事件中，表格下的輸入欄內容存取方式有兩種：第一種使用React體系的事件＋state；第二種為使用ref]]

