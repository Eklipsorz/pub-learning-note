## 描述

#### Parsing

> Now that we have fetched this file, we need to parse it into a module record. This helps the browser understand what the different parts of the module are.

[![Diagram showing main.js file being parsed into a module record](https://2r4s9p1yi1fa2jd7j43zph8r-wpengine.netdna-ssl.com/files/2018/03/25_file_to_module_record-500x199.png)](https://2r4s9p1yi1fa2jd7j43zph8r-wpengine.netdna-ssl.com/files/2018/03/25_file_to_module_record.png)

> Once the module record is created, it is placed in the module map. This means that whenever it’s requested from here on out, the loader can pull it from that map.

一旦瀏覽器獲取到對應模組檔案就會進行解析，具體就是就會將它轉換成模組紀錄(module record)

[![The “fetching” placeholders in the module map chart being filled in with module records](https://2r4s9p1yi1fa2jd7j43zph8r-wpengine.netdna-ssl.com/files/2018/03/25_module_map-500x239.png)](https://2r4s9p1yi1fa2jd7j43zph8r-wpengine.netdna-ssl.com/files/2018/03/25_module_map.png)

> There is one detail in parsing that may seem trivial, but that actually has pretty big implications. All modules are parsed as if they had `"use strict"` at the top. There are also other slight differences. For example, the keyword `await` is reserved in a module’s top-level code, and the value of `this` is `undefined`.

瀏覽器將JS模組檔案解析成紀錄的過程中，細節：
- 當JS模組檔案上頭存在use strict：
	- 以await 被保留在module top-level code
	- 模組的this會設定為undefined

> This different way of parsing is called a “parse goal”. If you parse the same file but use different goals, you’ll end up with different results. So you want to know before you start parsing what kind of file you’re parsing — whether it’s a module or not.



> In browsers this is pretty easy. You just put `type="module"` on the script tag. This tells the browser that this file should be parsed as a module. And since only modules can be imported, the browser knows that any imports are modules, too.

[![The loader determining that main.js is a module because the type attribute on the script tag says so, and counter.js must be a module because it’s imported](https://2r4s9p1yi1fa2jd7j43zph8r-wpengine.netdna-ssl.com/files/2018/03/26_parse_goal-500x311.png)](https://2r4s9p1yi1fa2jd7j43zph8r-wpengine.netdna-ssl.com/files/2018/03/26_parse_goal.png)

> But in Node, you don’t use HTML tags, so you don’t have the option of using a `type` attribute. One way the community has tried to solve this is by using an `.mjs` extension. Using that extension tells Node, “this file is a module”. You’ll see people talking about this as the signal for the parse goal. The discussion is currently ongoing, so it’s unclear what signal the Node community will decide to use in the end.

> Either way, the loader will determine whether to parse the file as a module or not. If it is a module and there are imports, it will then start the process over again until all of the files are fetched and parsed.

當要被解析前，會於內容解析上指定解析目標來定義特定檔案被解析後的形式會是如何，接著確定之後，才會開始解析，在這裏，同種同內容檔案若各定義不同解析目標，其結果也都會是獨立且不同：
- 瀏覽器：
	- 解析目標設定方法為在script 標籤上設定type="module"，這會告知瀏覽器指定script內容會以ES模組來解析，同時該script載入的模組也會以type="module"來定義
- 伺服器：
	- 解析目標設定方法為在要成為JS模組的JS檔案設定副檔名為mjs，就能告知伺服器端得以ES模組來解析，同時當JS模組檔案要載入的模組也是以mjs的話，就以ES模組來解析
- 不論是瀏覽器或者伺服器，都會試著檢查每個要被載入的模組是否為ES模組，確定才會做後續的解析
- 最後的結果是：每個獲取到的模組都轉換成模組紀錄，並未按照模組依賴關係圖來排

> And we’re done! At the end of the loading process, you’ve gone from having just an entry point file to having a bunch of module records.

[![A JS file on the left, with 3 parsed module records on the right as a result of the construction phase](https://2r4s9p1yi1fa2jd7j43zph8r-wpengine.netdna-ssl.com/files/2018/03/27_construction-500x406.png)](https://2r4s9p1yi1fa2jd7j43zph8r-wpengine.netdna-ssl.com/files/2018/03/27_construction.png)

> The next step is to instantiate this module and link all of the instances together.



---
Status: #🌱 
Tags:
[[JavaScript]]
Links:

[[es-modules-a-cartoon-deep-dive(2) - Construction ＆ Finding the file and fetching it 筆記]]
[[es-modules-a-cartoon-deep-dive(1) - How ES modules work 筆記]]
References:
[[@linclarkESModulesCartoon]]