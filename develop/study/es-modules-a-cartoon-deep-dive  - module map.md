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
- module map 是用來確定文件上所需要引入的模組之載入狀況：是否獲取？是否被解析？是否已經確定模組內容。


### JavaScript module script

> A record - One of the following:
> - a script record, for classic scripts;
> - a Source Text Module Record, for JavaScript module scripts;
> - a Synthetic Module Record, for CSS module scripts and JSON module scripts
> - null, representing a parsing failure.



---
Status: #🌱 
Tags:
[[JavaScript]]
Links:
References:
[[@linclarkESModulesCartoon]]