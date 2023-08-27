
## 描述


[[@fengyeJSMoKuaiHuaMaiLuo]] 所描述：
> ###幼年期：无模块化

> 1. 开始需要在页面中增加一些不同的js：动画、表单、格式化
> 2. 多种js文件被分在不同的文件中
> 3. 不同的文件又被同一个模板引用
> 4. script标签引入

> 文件分离是最基础的模块化第一步
> 
> 问题出现：
> - 污染全局作用域 => 不利于大型项目的开发以及多人团队的共建


重點：在還沒替JS進行模組化為主的開發時期
- 檔案分離：初步的模組化，將DOM Document 上的CSS、JS拆分成多個CSS檔案、多個JS檔案來讓DOM Document能夠重複使用
- 遇到問題：JS全域環境上的作用域污染問題
	- 背景：由於每個DOM Document會在首次執行JS前建立window物件而從而構成GEC，接著同一份的JS就用該GEC延續著，所以每個DOM Document 會是 每個獨立的JS全域環境，且沒有任何模組標準
	- 依賴於DOM Document 1的JS 並不會污染另一個DOM Document 2的JS 上的作用域，因兩者建立的GEC皆為不同，所以兩者全域環境也會是不同的
	- 在同一個DOM Document 的JS 中的多個程式碼區塊會彼此污染同一個作用域

在同一個DOM Document 的JS 中的多個程式碼區塊會彼此污染同一個作用域：
- 由於是一個DOM Document 來載入多個JS檔案執行，但這些JS上的程式碼會直接捏貼至它們在DOM Document 被呼叫的地方，執行起來並非會將每個檔案視為每個全域環境來獨立執行，而是它們所依附的目前Window節點所構成之全域環境上執行，換言之，他們全都在同一個全域環境下執行
	- 假設有三個JS檔案，分別叫做xxx1、xxx2、xxx3，而它們對應的程式碼分別為jscode1、jscode2、jscode3，這些JS檔案會被一個DOM Document 給載入，實際執行會是以捏貼後為主，這樣等同在同一個全域環境下執行
	- 若這些jscode會使用著共同都會有的變數名稱作為變數，很有可能會使這些jscode的預期不如預期，最後使得整份Document下的JS結果也跟著不如預期。
```
/* 捏貼前 */

// html code 1
<script src="xxx1"></script>
// html code 2 
<script src="xxx2"></script>
// html code 3 
<script src="xxx3"></script>

/* 捏貼後 */

// html code1
<script> jscode1 </script>
// html code2 
<script> jscode2 </script>
// html code3
<script> jscode3 </script>
```

### 全域污染是什麼
多個程式區塊在同一個全域環境下使用著彼此都會有的變數名稱/識別字作為變數來存取/變更，致使部分程式區塊的處理結果會是不如預期，甚至導致整個程式的最後結果也是不如預期



## 複習
#🧠 網頁開發在還沒替JS進行模組化為主的開發時期，最主要做了基本的檔案分離，請問檔案分離具體是什麼？ ->->-> `將DOM Document 上的CSS、JS拆分成多個CSS檔案、多個JS檔案`
<!--SR:!2023-12-07,309,250-->


#🧠 網頁開發在還沒替JS進行模組化為主的開發時期，最主要做了基本的檔案分離，請問為何要將內容分離出各種檔案？(提示模組) ->->-> `讓這些檔案變成基本模組來使用`
<!--SR:!2025-04-08,592,250-->



#🧠  網頁開發在還沒替JS進行模組化為主的開發時期，最主要是做了CSS、HTML、JS這三者間的檔案分離，但發生JS全域環境上的作用域污染問題，發生場景是在哪？為什麼會發生？  ->->-> `至於發生場景是在同一個DOM Document調用多個JS檔案`
<!--SR:!2024-11-23,520,250-->

#🧠 網頁開發在還沒替JS進行模組化為主的開發時期，最主要是做了CSS、HTML、JS這三者間的檔案分離，但發生JS全域環境上的作用域污染問題，請問多個DOM Document間會不會發生全域污染 ->->-> `由於每個DOM Document會在首次執行JS前建立window物件而從而構成GEC，接著同一份的JS就用該GEC延續著，所以每個DOM Document 會是 每個獨立的JS全域環境，所以多個DOM Document也就因為各有自己的GEC而不互相影響。`
<!--SR:!2024-03-01,345,250-->



#🧠 全域污染(global scope pollution)是什麼？ ->->-> `多個程式區塊在同一個全域環境下使用著彼此都會有的變數名稱/識別字作為變數來存取/變更，致使部分程式區塊的處理結果會是不如預期，甚至導致整個程式的最後結果也是不如預期`
<!--SR:!2023-10-25,279,250-->


#🧠 網頁開發在還沒替JS進行模組化為主的開發時期，最主要是做了CSS、HTML、JS這三者間的檔案分離，但發生JS全域環境上的作用域污染問題，問題發生在同一個DOM Document調用多個JS檔案，為什麼？ ->->-> `由於每個DOM Document會在首次執行JS前建立window物件而從而構成GEC，接著同一份的JS就用該GEC延續著，所以每個DOM Document 會是 每個獨立的JS全域環境，因此全域污染問題只會發生在同份DOM Document 上的多個JS檔案`
<!--SR:!2024-03-09,363,250-->


#🧠 假設有三個JS檔案，分別叫做xxx1、xxx2、xxx3，而它們對應的程式碼分別為jscode1、jscode2、jscode3，這些JS檔案會被一個DOM Document 給載入，請問實際上他們是如何被瀏覽器執行的？能否畫個圖表示 ->->-> `首先會先執行xxx1之前會先建立Window物件以及對應的GEC，接著後續的xxx2、xxx3全會以相同的GEC來執行並刷新 ![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1658155529/blog/javascript/html/before-js-module_quixaq.png)`
<!--SR:!2023-12-14,109,230-->


#🧠  假設有三個JS檔案，分別叫做xxx1、xxx2、xxx3，而它們對應的程式碼分別為jscode1、jscode2、jscode3，這些JS檔案會被一個DOM Document 給載入，若這些jscode會使用著共同都會有的變數名稱作為變數，那麼會發生什麼？ ![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1658155529/blog/javascript/html/before-js-module_quixaq.png) ->->-> `很有可能會使這些jscode的預期不如預期，最後使得整份Document下的JS結果也跟著不如預期。`
<!--SR:!2024-01-02,323,250-->



---
Status: #🌱 
Tags:
[[HTML]]  - [[JavaScript]]
Links:
[[HTML 的script 能夠允許瀏覽器邊解析DOM邊執行對應的程式碼，通常為JS，每個文件都會有各自的JS全域執行環境]]
References:
[[@fengyeJSMoKuaiHuaMaiLuo]]