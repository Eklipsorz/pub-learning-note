## 描述
### module map
[[@htmlspecHTMLStandard]] 所描述：
> A module map is a map keyed by tuples consisting of a URL record and a string. The URL record is the request URL at which the module was fetched, and the string indicates the type of the module (e.g. "javascript"). 
> 
> The module map's values are either a module script, null (used to represent failed fetches), or a placeholder value "fetching". Module maps are used to ensure that imported module scripts are only fetched, parsed, and evaluated once per Document or worker.




重點：
- module map 由多個 key-value pairs所構成
- key 為 URL record 和 string：URL record  是請求索要模組的目標主機位址，string則是標明模組的類型，如javascript
- value 為 module script(表達模組獲取成功)、null(表達模組獲取失敗)、fetching(正在獲取模組)
	- module script在這裡會是module record
- module map 是用來確定文件上所需要引入的模組之載入狀況：是否獲取？是否被解析？是否已經確定模組內容。


### Module Record 屬性
1. 其中屬性有Environment 會直接連接對應模組的實例所擁有的Enironment Record，該Record會紀錄著對應實例下的識別字以及對應識別字的實體物件。
2. 該屬性是只有模組實例產生時，才會自動設定對應實例的Environment Record

![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1659108051/blog/javascript/module/Module_Record_Format_p9aoaq.png)

---
Status: #🌱 
Tags:
[[JavaScript]]
Links:
[[es-modules-a-cartoon-deep-dive(2) - Construction ＆ Finding the file and fetching it 筆記]]
[[es-modules-a-cartoon-deep-dive(1) - How ES modules work 筆記]]
References:
[[@linclarkESModulesCartoon]]