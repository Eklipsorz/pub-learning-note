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
2. 通常宿主語言會是C語言為主
3. 膠水語言所採用的自製語法和語言可以與宿主語言相同
4. 膠水語言黏貼的環境就叫做宿主環境



## 複習
#🧠 Glue Language 是什麼？ ->->-> `是以自製的語言和語法來黏貼特定語言A的函式功能至特定語言B的產品下的 語言`

#🧠 Glue Language是以自製的語言和語法來黏貼特定語言A的函式功能至特定語言B的產品下的 語言，具體如何做？ ->->-> `具體而言的話，Glue Language會以自製語言和語法來包裝特定語言A函式功能，也就是以自製語言和自製語法就能呼叫對應的特定語言A下的函式功能，無需再透過特定語言A的呼叫方式來調用，接著以自製語言和自製語法黏貼在另一個特定語言B的軟體產品下，讓特定語言B能夠透過自製語言和自製語法來呼叫對應的特定語言A的函式功能`

#🧠 要能構成能夠使用的膠水語言之條件有哪些 (包裝和識別) ->->-> ` 能夠使用自製語言和自製語法來包裝特定語言A、黏貼的特定語言B要能夠識別其自製語言並知道如何執行`

#🧠 膠水語言的案例語言有哪些？ ->->-> `JavaScript、Perl、PHP、Python、Lua`

#🧠 膠水語言所採用的自製語法和語言可以與宿主語言相同嗎？ ->->-> `膠水語言所採用的自製語法和語言可以與宿主語言相同`

#🧠 膠水語言黏貼的環境叫做什麼 ->->-> `宿主環境`

#🧠 Glue Language 所包裝的語言稱之為什麼？主要做了什麼？ ->->-> `膠水語言中所包裝的語言稱之為宿主語言，具體膠水語言的實際功能都源自於宿主語言所提供`

#🧠 Glue Language 主要在不同程式語言模組下做了什麼？->->-> `只負責黏貼和調用`


#🧠 Glue Language的宿主語言通常是什麼？->->-> `是C語言為主`



---
Status: #🌱 
Tags:
[[Language]]
Links:
References:
[[@techtargetWhatGlueCode]]