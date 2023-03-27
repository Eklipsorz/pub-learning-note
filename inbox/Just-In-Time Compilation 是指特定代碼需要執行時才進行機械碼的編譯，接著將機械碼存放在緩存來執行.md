
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
通常從ByteCode編譯成機械碼，並存放在緩存或者快取，是為了未來可以在相同程式碼的情況下直接調用緩存或者快取上的機械碼來執行，而非重複地編譯，若程式碼與先前不同的話，就重新編譯，並把對應機械碼取代存放在緩存或者快取的機械
碼

#### just-in-time 命名緣由

just
> only; simply

[[@YingWenPianYuTimeTimeYouShiMoBuTong]]
in-time
> **in time 及時地**
> 跟 “on time” 不一樣，
> in time 有**及時趕上、剛好壓線**的意思。


重點：
- just ：為只有、唯獨
- in-time：為在特定時間A之前出現特定預期結果，但通常強調在特定時間A出現特定預期結果，而非在時間A之前出現
- just-in-time：合在一起就是指定特定事物就唯獨在特定時間A出現特定結果，不會是其他時間點出現

## 複習
#🧠 Just-In-Time Compilation  是什麼樣的編譯->->-> `Just-In-Time Compilation 是指當特定代碼被需要執行時才會編譯成機械碼並存放在快取或者緩存上，接著執行，而不是泛指執行整個檔案之前才編譯，平時不需要時並不會編譯。`
<!--SR:!2023-09-19,196,247-->

#🧠 Just-In-Time Compilation  是執行整個檔案之前才編譯，平時不需要時並不會編譯嗎？為什麼？ ->->-> `並不是，主要會是特定代碼需要時才會被編譯`
<!--SR:!2023-05-05,46,227-->

#🧠 Just-In-Time Compilation 是指當特定代碼被需要執行時才會編譯成機械碼並執行，請問能夠在編譯時獲取到的資訊會是什麼？ ->->-> `執行時的狀態資訊、執行前的狀態資訊`
<!--SR:!2023-10-24,215,247-->


#🧠 Just-In-Time Compilation 是指當特定代碼被需要執行時才會編譯成機械碼並存放在快取或者緩存上，接著執行，那麼儲存在快取或者緩存的機械碼會重複使用嗎？會的話，是怎麼樣的情況下？->->-> `通常從ByteCode編譯成機械碼，並存放在緩存或者快取，是為了未來可以在相同程式碼的情況下直接調用緩存或者快取上的機械碼來執行，而非重複地編譯`
<!--SR:!2023-05-15,191,250-->

#🧠 Just-In-Time Compilation 是指當特定代碼被需要執行時才會編譯成機械碼並存放在快取或者緩存上，接著執行，那麼儲存在快取或者緩存的機械碼會重複使用嗎？不會的話，是怎麼樣的情況下？->->-> `若程式碼與先前不同的話，就重新編譯，並把對應機械碼取代存放在緩存或者快取的機械碼`
<!--SR:!2024-01-14,334,250-->

#🧠 Just-In-Time Compilation  是指程式即將要被執行時就編譯嗎？->->-> `並不完全正確，還得考慮主程式是已經以機械碼來執行的情況下，對特定代碼的編譯`
<!--SR:!2023-06-14,180,210-->


#🧠 Just-In-Time Compilation 是執行時編譯嗎？還是執行前編譯？ 具體會是什麼？ ->->-> `兩者皆會有，若需要編譯的程式碼就是出現在主程式執行之前出現的話，Just-In-Time Compilation勢必會因為定義而先編譯，當然若於主要程式執行下出現需要被編譯執行的特定代碼，就進行機械碼的編譯並且執行`
<!--SR:!2023-09-02,250,249-->


#🧠 Just-In-Time Compilation 和 傳統在執行之前編譯整個檔案為機械碼的形式來相比，有什麼樣的差別 (以執行時的資訊來說吧)  ->->-> `前者可以根據特定程式被執行的資訊來對後續編譯進行調整和優化整個程式碼的效能，後者則不能獲取執行時的資訊來獲取，只能獲取到執行前的資訊`
<!--SR:!2023-05-03,182,250-->

#🧠 Java 和JVM為例子分成兩個方向： 說明從  ByteCode -> Java Interpreter如何執行 ![](https://pic2.zhimg.com/80/fc2d6adee7cfd35cd691b0a419dcd1a2_720w.jpg?source=1940ef5c)->->-> `Java 檔案會經由Java Compiler而編譯成Java ByteCode，並丟入JVM中的Java Interpreter來邊解析邊轉換成機械碼來給OS和硬體來執行`
<!--SR:!2023-05-10,189,250-->

#🧠 Java 和JVM為例子分成兩個方向： 說明從 ByteCode -> JIT Compiler如何執行 ![](https://pic2.zhimg.com/80/fc2d6adee7cfd35cd691b0a419dcd1a2_720w.jpg?source=1940ef5c) ->->-> `ByteCode -> JIT Compiler ： Java 檔案會經由Java Compiler 而編譯成Java ByteCode，並丟入JVM中的JIT Compiler 來將ByteCode編譯成目前執行環境下的machine code，最後丟給OS和硬體來執行`
<!--SR:!2023-04-21,174,250-->


#🧠 just-in-time 的just會是什麼意思？ ->->-> `為只有、唯獨`
<!--SR:!2023-04-09,13,246-->


#🧠 just-in-time 的in-time會是什麼意思？->->-> `為在特定時間A之前出現特定預期結果，但通常強調在特定時間A出現特定預期結果，而非在時間A之前出現`
<!--SR:!2023-04-06,11,246-->

#🧠 just-in-time 的in-time 是指在特定時間A之前出現特定預期結果，還有沒有其他可能的意思？->->-> `有，但通常強調在特定時間A出現特定預期結果，而非在時間A之前出現`
<!--SR:!2023-03-27,5,246-->

#🧠 just-in-time 的just 和 in-time合併再一起會是什麼意思？ ->->-> `合在一起就是指定特定事物就唯獨在特定時間A出現特定結果，不會是其他時間點出現`
<!--SR:!2023-03-28,6,246-->

#🧠 just-in-time 的in-time為何還需要just來強調->->-> `由於會有特定時間A之前、之後、剛好這三個時段，在這裡採用just來決定僅用剛好或者之前，但在這裡會只有剛好`
<!--SR:!2023-03-26,4,246-->


---
Status: #🌱 
Tags:
[[Operating System]]
Links:
References:
[[@thakurAnswerWhatDoes2013]]
[[@cidadeAnswerWhatDoes2008]]
[[@wikidataJustintimeCompilation2022]]
[[@YingWenPianYuTimeTimeYouShiMoBuTong]]