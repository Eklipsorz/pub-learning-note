


## 描述
### 主要實現方式
據[[@artemkirsanovZettelkastenWorkflowResearch2022]]所提到的概念：
	1. 讓Zotero 文獻管理軟體負責儲存和管理各個文獻
	2. 由Zotero 輸出對應文獻的metadata json
	3. Obsidian 引用第二步驟的json，然後安裝能夠參考該文獻json的套件
	4. 執行該套件的指令來引用對應文獻


### 所需安裝套件
1. Zotero：文獻管理軟體
2. Zotero browser plugin：用來將網頁轉換成Zotero上的文獻資料
3. Better BibTex for Zotero：安裝至Zotero的額外套件，用來提供特定形式來輸出文獻資料至指定json檔案，可讓Zotero自動根據指定文獻資料庫是否更新資料來更新指定json檔案
4. Obsidian Citations 套件：用來引用Better BibTex for Zotero 所產出的JSON檔案並轉換成Obsidian md檔案來方便給予連結，然而目前只能夠設定引用格式和如何找到JSON檔案，不能自動根據JSON是否更新而跟著更新

### 好處
1. 以後由Zotero來控管一切文獻資料，無需另外由Obsidian來另外管理
2. Obsidian 套件可額外產生出文獻資料的註解

### 目前壞處
1. Obsidian Citation 套件目前無法自動根據JSON內容是否更新而跟著更新

###  如何設定
[[安裝 Better BibTex for Zotero 來讓Zotero能夠自動輸出文獻資料JSON]]


---
Status: #🌱 
Tags:
[[Note]] - [[Zettelkasten Note]] - [[Obsidian]]
Links:
[[安裝 Better BibTex for Zotero 來讓Zotero能夠自動輸出文獻資料JSON]]
References: 
[[@artemkirsanovZettelkastenWorkflowResearch2022]]