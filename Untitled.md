## 描述
[[@wikidataLuaWeiJiBaiKeZiYouDeBaiKeQuanShu]] 所描述的是Lua本身編譯和如何執行：
>  Lua程式不是從文字式的Lua檔案直接解釋的，而是編譯成位元組碼，接著把它執行在Lua虛擬機器上。編譯過程典型的對於使用者是不可見並且是在執行時間進行的，但是它可以離線完成用來增加裝載效能或通過排除編譯器來減少對宿主環境的記憶體占用。Lua位元組碼還可以在Lua之內產生和執行

[[@wikidataLuaProgrammingLanguage2022]] 描述
> **Lua** (/ˈluːə/ _LOO__-ə_; from Portuguese: _lua_ [ˈlu.(w)ɐ] meaning _moon_) is a lightweight, high-level, multi-paradigm programming language designed primarily for embedded use in applications.[3] Lua is cross-platform, since the interpreter of compiled bytecode is written in ANSI C,[4] and Lua has a relatively simple C API to embed it into applications.[5]


[[@LuaShiZenYangYiMenYuYanZhiHu]] 所描述的是Lua 本身是個膠水語言：
> 但是Lua可以很容易地被擴充：由宿主語言（通常是C或C++）提供這些功能，Lua可以使用它們，就像是本來就內建的功能一樣。事實上，現在已經有很多成熟的擴充模組可供選用。

> Lua天生的定位就是做为一门"胶水语言"出现的.它没有自己独立的环境,必须依附在宿主语言的环境中才能起作用.所以从一开始,Lua就非常清楚自己的定位:它不想自己做大,而是做的够精简够小,嵌入在宿主语言中,帮忙提供一些动态特性.

> 明白了这一点,就明白了Lua的许多设计思路--小,自提供库少,天生的胶水语言---因此任何C\C++能出现的地方,Lua就能轻松的嵌入其中.除了C\C++之外,其他语言也开始意识到了Lua的价值,开始支持它了.obj-C,as等.

> Lua是一種輕量語言，它的官方版本只包括一個精簡的核心和最基本的庫。這使得Lua體積小、啟動速度快。它用ANSI C語言編寫[8]，並以原始碼形式開放，編譯後的完整參考直譯器只有大約247kB[8]，到5.4.3版本，該體積變成283kB（Linux,amd64），依然非常小巧，可以很方便的嵌入別的程式裡。和許多「大而全」的語言不一樣，網路通訊、圖形介面等都沒有預設提供。但是Lua可以很容易地被擴充：由宿主語言（通常是C或C++）提供這些功能，Lua可以使用它們，就像是本來就內建的功能一樣。事實上，現在已經有很多成熟的擴充模組可供選用。

重點：
- Lua 是膠水語言的一種，以自製的語法和語言來包裝C語言為主的功能模組，其C語言版本為ANSI C語言
[[膠水語言(Glue Language)  是以自製的語言和語法來黏貼特定語言A的函式功能至特定語言B的產品下的 語言]]
- Lua 不是傳統的直譯語言，擁有編譯、直譯特性的語言，主要有：
	- 先將Lua語法轉換成ByteCode，接著從ByteCode解析執行
	- 執行前先將Lua語法轉換成ByteCode，然後執行時丟進Lua 虛擬機邊解析邊執行
	- 直接以Lua語法來解析
	- 先將Lua語法轉換成ByteCode，接著再透過compiler從ByteCode轉換成機械碼來執行




### 先將Lua語法轉換至ByteCode，接著從ByteCode解析執行

首先當Lua 語法放置另一個程式語言B的環境下，且沒事先編譯Lua語法為ByteCode，那麼根據時機來編譯：
	- 程式語言B要開始呼叫Lua語法時：Lua就會被編譯成ByteCode並存放在宿主環境的記憶體或者快取中，並將ByteCode丟進Lua 虛擬機，由它負責邊解析ByteCode邊執行對應的C語言代碼
	- 只要宿主程式一開始執行且沒遇到Lua時：Lua就會被編譯成ByteCode並存放在宿主環境的記憶體，接著等宿主程式一執行到Lua就把ByteCode丟進虛擬機邊解析邊執行

![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1657555608/blog/compilation/LuaCode-ByteCode-Execute_znwxg0.png)

細節：
1. 每一次從Lua編譯成ByteCode時，會將對應的ByteCode放置宿主的記憶體或者快取，並不另外存放在硬碟
2. 若下一次執行的Lua是一樣的話，就不會做多餘的編譯，直接以現存在記憶體的ByteCode執行
3. Lua 虛擬機主要是負責邊解析ByteCode邊執行的解析器
4. ByteCode是獨立於Lua、任何程式語言、機械碼、組合語言的代碼形式，只有Lua虛擬機能解析


### 直接以Lua語法來解析

![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1657555105/blog/compilation/Offline-ByteCode-Execute_ig1wxn.png)


###  先將Lua語法轉換至ByteCode，接著再透過compiler從ByteCode轉換成機械碼來執行




## 複習
#🧠 Question :: ->->-> ``


---
Status: 
Tags:
[[Lua]] - [[Redis]]
Links:
[[Redis 需要Lua指令是由於想透過從伺服器內部直接執行腳本來提昇指令被執行的效率以及替多個指令轉換成原子化操作]] 
[[膠水語言(Glue Language)  是以自製的語言和語法來黏貼特定語言A的函式功能至特定語言B的產品下的 語言]]
References:
[[@LuaShiZenYangYiMenYuYanZhiHu]]
[[@wikidataLuaProgrammingLanguage2022]]
[[@wikidataLuaWeiJiBaiKeZiYouDeBaiKeQuanShu]]