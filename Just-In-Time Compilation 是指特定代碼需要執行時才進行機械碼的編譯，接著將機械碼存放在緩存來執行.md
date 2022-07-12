
## 描述
[[@cidadeAnswerWhatDoes2008]] 所描述的：
> A JIT compiler runs **after** the program has started and compiles the code (usually bytecode or some kind of VM instructions) on the fly (or just-in-time, as it's called) into a form that's usually faster, typically the host CPU's native instruction set. A JIT has access to dynamic runtime information whereas a standard compiler doesn't and can make better optimizations like inlining functions that are used frequently.

> This is in contrast to a traditional compiler that compiles **all** the code to machine language **before** the program is first run.

> To paraphrase, conventional compilers build the whole program as an EXE file BEFORE the first time you run it. For newer style programs, an assembly is generated with pseudocode (p-code). Only AFTER you execute the program on the OS (e.g., by double-clicking on its icon) will the (JIT) compiler kick in and generate machine code (m-code) that the Intel-based processor or whatever will understand.


![](https://pic2.zhimg.com/80/fc2d6adee7cfd35cd691b0a419dcd1a2_720w.jpg?source=1940ef5c)

[[@thakurAnswerWhatDoes2013]] 所描述的：
> As other have mentioned

> **JIT stands for Just-in-Time which means that code gets compiled when it is needed, not before runtime.**


重點：
- Just-In-Time Compilation 是指當特定代碼被需要執行時才會編譯成機械碼並存放在快取或者緩存上，接著執行，而不是泛指執行整個檔案之前才編譯，平時不需要時並不會編譯。
- Just-In-Time Compilation 會於主要程式執行時對需要被執行的特定代碼進行機械碼的編譯並且執行
- 在特定程式執行時來編譯還未編譯成機械碼的代碼來進行，換言之，就是執行時編譯
- Just-In-Time Compilation 與傳統在執行之前編譯整個檔案為機械碼的形式來相比，前者可以根據特定程式被執行的資訊來對後續編譯進行調整和優化整個程式碼的效能，後者則不能獲取執行時的資訊來獲取，只能獲取到執行前的資訊。
- Java 和JVM為例子分成兩個方向：
	-  ByteCode -> Java Interpreter ：Java 檔案會經由Java Compiler而編譯成Java ByteCode，並丟入JVM中的Java Interpreter來邊解析邊轉換成機械碼來給OS和硬體來執行
	-  ByteCode -> JIT Compiler ： Java 檔案會經由Java Compiler 而編譯成Java ByteCode，並丟入JVM中的JIT Compiler 來將ByteCode編譯成目前執行環境下的machine code，最後丟給OS和硬體來執行

![](https://pic2.zhimg.com/80/fc2d6adee7cfd35cd691b0a419dcd1a2_720w.jpg?source=1940ef5c)
### Just-In-Time Compilation  就一定是指程式即將要被執行時就編譯嗎？
並不完全正確，還得考慮主程式是已經以機械碼來執行的情況下，對特定代碼的編譯


### 儲存在快取或者緩存的機械碼會重複使用嗎？
通常從ByteCode編譯成機械碼，並存放在緩存或者快取，是為了未來可以在相同程式碼的情況下直接調用緩存或者快取上的機械碼來執行，而非重複地編譯，若程式碼與先前不同的話，就重新編譯，並把對應機械碼取代存放在緩存或者快取的機械碼

## 複習
#🧠 Just-In-Time Compilation  是什麼樣的編譯->->-> `Just-In-Time Compilation 是指當特定代碼被需要執行時才會編譯成機械碼並存放在快取或者緩存上，接著執行，而不是泛指執行整個檔案之前才編譯，平時不需要時並不會編譯。`

#🧠 Just-In-Time Compilation 是指當特定代碼被需要執行時才會編譯成機械碼並存放在快取或者緩存上，接著執行，那麼儲存在快取或者緩存的機械碼會重複使用嗎？會的話，是怎麼樣的情況下？->->-> `通常從ByteCode編譯成機械碼，並存放在緩存或者快取，是為了未來可以在相同程式碼的情況下直接調用緩存或者快取上的機械碼來執行，而非重複地編譯`

#🧠 Just-In-Time Compilation 是指當特定代碼被需要執行時才會編譯成機械碼並存放在快取或者緩存上，接著執行，那麼儲存在快取或者緩存的機械碼會重複使用嗎？不會的話，是怎麼樣的情況下？->->-> `若程式碼與先前不同的話，就重新編譯，並把對應機械碼取代存放在緩存或者快取的機械碼`

#🧠 Just-In-Time Compilation  是指程式即將要被執行時就編譯嗎？->->-> `並不完全正確，還得考慮主程式是已經以機械碼來執行的情況下，對特定代碼的編譯`


#🧠 Just-In-Time Compilation 是執行時編譯嗎？還是執行前編譯？ 具體會是什麼？ ->->-> `Just-In-Time Compilation 會於主要程式執行時對需要被執行的特定代碼進行機械碼的編譯並且執行`

#🧠 Just-In-Time Compilation 和 傳統在執行之前編譯整個檔案為機械碼的形式來相比，有什麼樣的差別 (以執行時的資訊來說吧)  ->->-> `前者可以根據特定程式被執行的資訊來對後續編譯進行調整和優化整個程式碼的效能，後者則不能獲取執行時的資訊來獲取，只能獲取到執行前的資訊`

#🧠 Java 和JVM為例子分成兩個方向： 說明從  ByteCode -> Java Interpreter如何執行 ![](https://pic2.zhimg.com/80/fc2d6adee7cfd35cd691b0a419dcd1a2_720w.jpg?source=1940ef5c)->->-> `Java 檔案會經由Java Compiler而編譯成Java ByteCode，並丟入JVM中的Java Interpreter來邊解析邊轉換成機械碼來給OS和硬體來執行`

#🧠 Java 和JVM為例子分成兩個方向： 說明從 ByteCode -> JIT Compiler如何執行 ![](https://pic2.zhimg.com/80/fc2d6adee7cfd35cd691b0a419dcd1a2_720w.jpg?source=1940ef5c) ->->-> `ByteCode -> JIT Compiler ： Java 檔案會經由Java Compiler 而編譯成Java ByteCode，並丟入JVM中的JIT Compiler 來將ByteCode編譯成目前執行環境下的machine code，最後丟給OS和硬體來執行`

---
Status: #🌱 
Tags:
[[Operating System]]
Links:
References:
[[@thakurAnswerWhatDoes2013]]
[[@cidadeAnswerWhatDoes2008]]
[[@wikidataJustintimeCompilation2022]]