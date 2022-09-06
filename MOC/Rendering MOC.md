

## Imperative Rendering vs. Declarative Rendering

[[Imperative Programming 是開發者直接使用電腦解讀執行的指令來實現自己想要的目標，Declarative Programming則是開發者告訴系統目標是什麼，由系統產生對應指令來執行]]


## DOM 
- DOM
[[Document Object Model 是以樹狀結構來表達HTML內容的模型、介面]]

## BOM
- BOM
[[Browser Object Model 是早期在沒有DOM時代時，以樹狀結構來表示網頁內容的介面]]

[[Window 物件是指顯示 特定文件所渲染出來的畫面 的顯示區塊物件]]


## Box Model

[[每一個HTML 元素都是由多種盒子相互裝載而成的結構，該結構稱之為Box Model]]

## HTML + CSS + JS
- HTML + CSS + JS
[[HTML、CSS、JS隨著時代更迭而演進成需要事前轉譯來解決各自問題、根據情況來產生對應的CSS、HTML]]

- HTML + JS
[[HTML 的script 能夠允許瀏覽器邊解析DOM邊執行對應的程式碼，通常為JS，每個文件都會有各自的JS全域執行環境]]

[[inline javascript 是指會在HTML文件內部加入JavaScript語法的開發方式，而onclick=function()則是指定事件發生時要執行的指令]]

[[parser blocking 是瀏覽器的HTML內容解析器因特定原因而被其他元件給停止解析，render blocking 是瀏覽器的渲染器元件因特定原因而被其他元件給停止渲染]]


- CSS
[[CSS 只是定義特定樣式名稱是會有什麼樣外觀的規格書，本身會具有語法重複、可維護性低、可讀性很差這三大開發性問題]]

[[CSS-in-JS 是種技術，主要是將CSS樣式寫在JS內容，並運用JS程式語言的執行特色來根據執行情況來更改樣式中的內容]]


[[CSSOM 本身由於本身並不像HTML能夠邊解析邊生成DOM，只能對整份CSS檔案進行處理才能獲取CSSOM，換言之，在處理完之前是不會有CSSOM]]

[[客戶端利用link標籤或者style標籤來解析CSS檔案內容為CSSOM會是以接收完整份CSS檔案才開始解析成CSSOM，而非邊接收邊解析成CSSOM]]

[[inline style 是在HTML內容標籤形式上所夾雜的一組特定樣式組合]]

[[Specificity 是一個算法，專門在n個 selector指向同一個元件A的情況下，決定哪一個declaration要被採用至元件A，這些declaration 包含著屬性名稱上起衝突和屬性名稱沒起衝突]]
[[一個CSS rule 是由可以選擇哪個種類的HTML元素來指定樣式內容的selector和實際定義樣式內容為何的declaration block]]

[[每個CSS rule 上的selector 部分，主要可以用下面形式來描述所要選擇的DOM節點會是什麼：universal selector、type selector、id selector、class selector]]

[[media query 是定義一系列問題來向瀏覽器詢問裝置是否為指定裝置、解析度是否為指定解析度，若是的話，就會以定義好的樣式屬性來渲染]]



#### JS 模組化
[[在還沒替JS進行模組化時，是使用檔案分離來將HTML上的CSS、JS拆成多個CSS檔案、多個JS檔案來使用，但同個HTML載入多個JS檔案會產生全域污染問題]]


## template

[[template processor 技術目的是要將網頁切分成MVC(Model、View、Controller)來開發和維護]]



## 資源

[[靜態資源是資源本身並不會隨著執行、處理請求而變動，動態資源是資源本身會隨著執行、處理請求而變動]]