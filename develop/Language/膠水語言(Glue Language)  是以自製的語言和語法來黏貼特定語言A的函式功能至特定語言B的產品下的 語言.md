## 描述
[[@techtargetWhatGlueCode]] 所描述：

> Glue code, also called binding code, is custom-written programming that connects incompatible software components.

> Glue code can be written in the same language as the code it is connecting together, but it is often written in a specialized interpreted scripting language for connecting system components called a glue language. Popular glue languages include include AppleScript, JavaScript, Perl, PHP, Python, Ruby, VBScript and PowerShell.

重點：
- Glue code 或者 Glue Language 是以自製的語言和語法來黏貼特定語言A的函式功能至特定語言B的產品下的 語言
- 具體而言的話，Glue Language會以自製語言和語法來包裝特定語言A函式功能，也就是以自製語言和自製語法就能呼叫對應的特定語言A下的函式功能，無需再透過特定語言A的呼叫方式來調用
- 接著以自製語言和自製語法黏貼在另一個特定語言B的軟體產品下，讓特定語言B能夠透過自製語言和自製語法來呼叫對應的特定語言A的函式功能

- 在這裡要能構成能夠使用的膠水語言：
	- 能夠使用自製語言和自製語法來包裝特定語言A
	- 黏貼的特定語言B要能夠識別其自製語言並知道如何執行
- 典型的膠水語言有JavaScript、Perl、PHP、Python、Lua

### 細節
1. 膠水語言中所包裝的語言稱之為宿主語言，具體膠水語言的實際功能都源自於宿主語言所提供，膠水語言本身並沒有提供具體的功能，只負責黏貼和調用
2. 宿主是指著膠水語言目前黏貼的執行環境，所有以宿主為主的事物都以該執行環境為主
3. 通常宿主語言會是宿主環境下的C語言為主或者宿主環境下所能夠識別並執行的程式語言
4. 膠水語言所採用的自製語法和語言可以與宿主語言相同
5. 膠水語言黏貼的環境就叫做宿主環境

### 宿主語言和宿主環境
[[@SuZhuYuYanBaiDuBaiKe]]  所描述：
> 軟件賴以生存的[軟件環境](https://baike.baidu.hk/item/%E8%BB%9F%E4%BB%B6%E7%92%B0%E5%A2%83)被稱作是**宿主環境**(host environment).宿主環境可以是操作系統,服務器程序,應用程序,而開發這些宿主環境的程序語言(如開發操作系統一般使用c語言,開發WebServer一般使用c或java語言,開發應用程序一般使用C++/java/c#語言)被稱作系統開發語言,或用一個更貼切的説法是---宿主語言(Host Language).

> 比方説你用VC做數據庫，那麼C++就是宿主語言，它是SQL的宿主.

重點：
- 對應目前所執行的程式而言，其程式所在的執行環境，即為宿主環境(host environment)
	- 宿主環境可以是作業系統、伺服器系統
- 宿主環境下(host environment)所能辨識並執行的語言，就叫做宿主語言(host Language)

## 複習
#🧠 Glue Language 是什麼？ ->->-> `是以自製的語言和語法來黏貼特定語言A的函式功能至特定語言B的產品下的 語言`
<!--SR:!2023-11-18,299,250-->

#🧠 膠水語言中所包裝的語言稱之為宿主語言? 請問宿主語言是什麼？->->-> `通常宿主語言會是宿主環境下所能夠識別並執行的程式語言`
<!--SR:!2024-07-04,438,250-->

#🧠 Glue Language是以自製的語言和語法來黏貼特定語言A的函式功能至特定語言B的產品下的 語言，對於特定語言A和特定語言B而言，Glue Language是什麼 ?->->-> `一個專門將特定語言A黏貼至特定語言B身上的膠水語言，並且使特定語言B下的執行環境能夠透過識別Glue language而執行它，並間接執行特定語言A的模組`
<!--SR:!2025-01-08,514,230-->

#🧠 Glue Language是以自製的語言和語法來黏貼特定語言A的函式功能至特定語言B的產品下的 語言，相當於是什麼意思？會有呼叫關係嗎？ ->->-> `Glue Language會以自製語言和語法來包裝特定語言A函式功能，也就是以自製語言和自製語法就能呼叫對應的特定語言A下的函式功能，無需再透過特定語言A的呼叫方式來調用，接著以自製語言和自製語法黏貼在另一個特定語言B的軟體產品下，讓特定語言B能夠透過自製語言和自製語法來呼叫對應的特定語言A的函式功能`
<!--SR:!2024-04-07,390,250-->

#🧠 要能構成能夠使用的膠水語言之條件有哪些 (包裝和識別) ->->-> ` 能夠使用自製語言和自製語法來包裝特定語言A、黏貼的特定語言B要能夠識別其自製語言並知道如何執行`
<!--SR:!2023-11-24,63,190-->

#🧠 膠水語言的案例語言有哪些？ ->->-> `JavaScript、Perl、PHP、Python、Lua`
<!--SR:!2024-05-02,402,250-->

#🧠 膠水語言所採用的自製語法和語言可以與宿主語言相同嗎？ ->->-> `膠水語言所採用的自製語法和語言可以與宿主語言相同`
<!--SR:!2024-04-09,240,230-->

#🧠 膠水語言黏貼的環境叫做什麼 ->->-> `宿主環境`
<!--SR:!2024-03-11,368,250-->

#🧠 Glue Language 所包裝的語言稱之為什麼？ ->->-> `膠水語言中所包裝的語言稱之為宿主語言`
<!--SR:!2024-05-19,408,250-->

#🧠 在Glue Language 、Glue Language 包裝的宿主語言的模組兩者中，誰才是最主要提供具體實際功能？ ->->-> `宿主語言下的模組`
<!--SR:!2024-03-01,360,250-->

#🧠 Glue Language 主要在不同程式語言模組下做了什麼？->->-> `只負責黏貼和調用`
<!--SR:!2024-05-12,273,230-->


#🧠 Glue Language的宿主語言通常是什麼？(請特別強調誰的語言)->->-> `通常宿主語言會是宿主環境下的C語言為主或者宿主環境下所能夠識別並執行的程式語言`
<!--SR:!2024-01-15,196,230-->


#🧠 宿主環境(host environment) 是什麼？(請試著以程式執行來想)->->-> `對應目前所執行的程式而言，其程式所在的執行環境，即為宿主環境(host environment)`
<!--SR:!2024-03-31,358,230-->

#🧠 對應目前所執行的程式而言，其程式所在的執行環境，即為宿主環境(host environment)，那麼請你舉幾個例子誰會是宿主環境？->->-> `宿主環境可以是作業系統、伺服器系統`
<!--SR:!2023-10-01,49,210-->

#🧠 宿主語言(host language) 是什麼？ ->->-> `宿主環境下(host environment)所能辨識並執行的語言，就叫做宿主語言(host Language)`
<!--SR:!2024-05-25,413,250-->


---
Status: #🌱 
Tags:
[[Language]]
Links:
References:
[[@SuZhuYuYanBaiDuBaiKe]]
[[@techtargetWhatGlueCode]]