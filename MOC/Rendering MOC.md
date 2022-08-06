

## Imperative Rendering vs. Declarative Rendering

[[Imperative Programming 是開發者直接使用電腦解讀執行的指令來實現自己想要的目標，Declarative Programming則是開發者告訴系統目標是什麼，由系統產生對應指令來執行]]


## DOM 
- DOM
[[Document Object Model 是以樹狀結構來表達HTML內容的模型、介面]]

## BOM
- BOM
[[Browser Object Model 是早期在沒有DOM時代時，以樹狀結構來表示網頁內容的介面]]
## HTML + CSS + JS


- HTML + JS
[[HTML 的script 能夠允許瀏覽器邊解析DOM邊執行對應的程式碼，通常為JS，每個文件都會有各自的JS全域執行環境]]

[[parser blocking 是瀏覽器的HTML內容解析器因特定原因而被其他元件給停止解析，render blocking 是瀏覽器的渲染器元件因特定原因而被其他元件給停止渲染]]

- CSS
[[CSS 只是定義特定樣式名稱是會有什麼樣外觀的規格書，本身會具有語法重複、可維護性低、可讀性很差這三大開發性問題]]

[[CSS-in-JS 是種技術，主要是將CSS樣式寫在JS內容，並運用JS程式語言的執行特色來根據執行情況來更改樣式中的內容]]

#### JS 模組化
[[在還沒替JS進行模組化時，是使用檔案分離來將HTML上的CSS、JS拆成多個CSS檔案、多個JS檔案來使用，但同個HTML載入多個JS檔案會產生全域污染問題]]


## template

[[template processor 技術目的是要將網頁切分成MVC(Model、View、Controller)來開發和維護]]