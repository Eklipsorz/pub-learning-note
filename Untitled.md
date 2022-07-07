## 描述
[[@wikidataLuaWeiJiBaiKeZiYouDeBaiKeQuanShu]] 所描述
>  Lua程式不是從文字式的Lua檔案直接解釋的，而是編譯成位元組碼，接著把它執行在Lua虛擬機器上。編譯過程典型的對於使用者是不可見並且是在執行時間進行的，但是它可以離線完成用來增加裝載效能或通過排除編譯器來減少對宿主環境的記憶體占用。Lua位元組碼還可以在Lua之內產生和執行

[[@wikidataLuaProgrammingLanguage2022]] 描述
> **Lua** (/ˈluːə/ _LOO__-ə_; from Portuguese: _lua_ [ˈlu.(w)ɐ] meaning _moon_) is a lightweight, high-level, multi-paradigm programming language designed primarily for embedded use in applications.[3] Lua is cross-platform, since the interpreter of compiled bytecode is written in ANSI C,[4] and Lua has a relatively simple C API to embed it into applications.[5]

重點：
- lua 不是傳統的直譯語言，而是先編譯成以Lua虛擬機器能理解的位元組碼，接著再把位元組碼丟到虛擬機器執行，由虛擬機器邊轉換機械碼邊執行
- 編譯

![](http://blog.gitdns.org/2016/08/10/lua/jit.png)


> Lua是一種輕量語言，它的官方版本只包括一個精簡的核心和最基本的庫。這使得Lua體積小、啟動速度快。它用ANSI C語言編寫[8]，並以原始碼形式開放，編譯後的完整參考直譯器只有大約247kB[8]，到5.4.3版本，該體積變成283kB（Linux,amd64），依然非常小巧，可以很方便的嵌入別的程式裡。和許多「大而全」的語言不一樣，網路通訊、圖形介面等都沒有預設提供。但是Lua可以很容易地被擴充：由宿主語言（通常是C或C++）提供這些功能，Lua可以使用它們，就像是本來就內建的功能一樣。事實上，現在已經有很多成熟的擴充模組可供選用。




> 说说我的理解吧。

> 用C/C++开发的大型程序，拥有了可靠性和速度，但是其灵活性不够。

> 比如我要增加某项附加功能，用C/C++当然还能做，但众所周知C这类语言的开发速度远远比不上lua这类解释型语言，lua光是一个不用定义数据类型，就节省了成吨的功夫，而且某些数据结构用C来表示是很麻烦的，例如你要用C的数据结构去描述json string，如果不用第三方库，你知道凌晨四点的洛杉矶是什么样子的吗( •̀∀•́ )？

> 所以就有lua的用武之地了，lua速率可以接受，lua嵌入C容易得就像一个妈生的一样，注意是嵌入而不是简单的调用啊？试想如果有很多主流功能之外的额外用lua开发，用这省下来的成吨的时间，去研究怎样拿到前台小妹的电话不好吗？

  
  
作者：肃之  
链接：https://www.zhihu.com/question/20296452/answer/77309793  
来源：知乎  
著作权归作者所有。商业转载请联系作者获得授权，非商业转载请注明出处。


> 正在阅读lua的web框架lapis的源码， 我觉得完全可以用来做web开发，好处就是效率高呀，针对web而言：比golang都强，你说为嘛不用。
> cache层面直接用sharedict和worker缓存，比传统的redis+mysql又往前加速了几个量级。
> 不爽了直接c来实现，用lua调用。

  


## 複習
#🧠 Question :: ->->-> ``

---
Status: 
Tags:
[[Lua]] - [[Redis]]
Links:
[[Redis 需要Lua指令是由於想透過從伺服器內部直接執行腳本來提昇指令被執行的效率以及替多個指令轉換成原子化操作]] 
References:
[[@wikidataLuaProgrammingLanguage2022]]
[[@wikidataLuaWeiJiBaiKeZiYouDeBaiKeQuanShu]]