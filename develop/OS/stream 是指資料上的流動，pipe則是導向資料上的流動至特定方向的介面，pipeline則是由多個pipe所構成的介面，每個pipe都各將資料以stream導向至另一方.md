## 描述


  

### stream

[[@wikidataStreamComputing2020]] 所描述
> In computer science, a stream is a sequence of data elements made available over time. A stream can be thought of as items on a conveyor belt being processed one at a time rather than in large batches. 





重點：
- stream 原意為某項東西的連續性流動，在這裡會是指資料上的連續性流動
- 資料上的連續性流動，具體會是將資料以二進制切分好幾個區塊，並為每個區塊標記傳輸順序，接著就會按照順序來傳輸區塊。
- stream 本身是資料的傳遞方式，根據處理程式而分成input stream 和 output stream：
	- input stream：特定程式的輸入部分會以stream方式來接收
	- output stream：特定程式會以stream方式來輸出處理結果
- 好處是：
	- 資料傳輸失敗的話，可以根據傳輸失敗的序列號碼重新傳遞，而不用整個資料傳遞過去


### pipe
[[@techtargetWhatPipeDefinition]] ：
> In computer programming, especially in [UNIX](https://www.techtarget.com/searchdatacenter/definition/Unix) operating systems, a pipe is a technique for passing information from one program [process](https://www.techtarget.com/whatis/definition/process) to another. Unlike other forms of interprocess communication (IPC), a pipe is one-way communication only. Basically, a pipe passes a parameter such as the output of one process to another process which accepts it as input. The system temporarily holds the piped information until it is read by the receiving process.

> For two-way communication between processes, two pipes can be set up, one for each direction. A limitation of pipes for interprocess communication is that the processes using pipes must have a common parent process (that is, share a common open or initiation process and exist as the result of a _fork_ system call from a parent process).


重點：
- pipe 原意為管子，管子會有液體或者氣體，並且以單個方向流動，從一個地方A流動另一個地方B
- 在電腦科學中，管子裡會有代表資料上的連續性流動(stream)，而管子會將stream以單個方向從一個process的輸出出口導向至另一個process的輸入入口，換言之，就是決定stream流動方向導向至特定方向的技術
- pipe 在實現上，只能以單方向傳輸，不能夠逆流，但可以建立另一個pipe來構成可以逆流的方向。

### stream vs pipeline vs. pipe 命名緣由

[[@WhatDifferencePiping]] ：
pipeline
> The pipeline is a series of straight pipes welded together over a long distance

pipe
> a tube inside which liquid or gas flows from one place to another

stream
> A stream can be thought of as items on a conveyor belt being processed one at a time rather than in large batches.

> a continuous flow of things or people


重點：
- stream 是某項東西的連續性流動
- pipe 會是管子，管子會有液體或者氣體，並且只能以單個方向流動，從一個地方A流動至另一個地方B
- pipeline 是多個直線狀管子所焊接而成的長距離直線管子，每一個管子都以特定的方向將內容物流動另一個管子。

### stream vs. pipeline vs. pipe

[[@maxWhatArePrimary]] 所描述的stream vs pipe ：
> Streams are an operating system abstraction to make dealing with input and output easier. Instead of needing to deal with all sorts of IO (like files, stdin and stdout, and sockets) in different ways, there is a common abstraction of a byte stream.

> The pipe in general is a way of connecting streams. a mechanism by which the output stream of one process becomes an input stream of another process. The most common example is the pipe operator in the terminal, which allows you to connect the stdout (standard output stream) of the process on the left to the stdin (standard input stream) of the process on the right.


重點：
- stream 只是一個作業系統層級的抽象傳輸概念，專門以類似stream的方式來處理特定程式的接收資料和輸出資料
- pipe 具體是將多個stream連接在一起的技術，案例：將一個程式A的輸出流轉移至另一個程式B的輸入流，這樣導向會將程式A的輸出結果以stream的方式輸出，直接導入至程式B的輸入部分，而程式B的輸入部分也是以stream來接收。

## 複習
#🧠 stream 命名緣由為何？ ->->-> `是某項東西的連續性流動`

#🧠 pipe 命名緣由為何 ->->-> `pipe 會是管子，管子會有液體或者氣體，並且只能以單個方向流動，從一個地方A流動至另一個地方B`


#🧠 pipeline 命名緣由為何 ->->-> `是多個直線狀管子所焊接而成的長距離直線管子，每一個管子都以特定的方向將內容物流動另一個管子。`

#🧠 pipeline是多個直線狀管子所焊接而成的長距離直線管子，那麼每一個管子的流動方式？ ->->-> `每一個管子都以特定的方向將內容物流動另一個管子`


#🧠 stream 原意為某項東西的連續性流動，那麼在電腦科學會是指？ ->->-> `資料上的連續性流動`


#🧠 stream 在電腦科學會是指資料上的連續性流動，那麼具體會是什麼？ ->->-> `具體會是將資料以二進制切分好幾個區塊，並為每個區塊標記傳輸順序，接著就會按照順序來傳輸區塊。`

#🧠 stream 具體會是將資料以二進制切分好幾個區塊，並為每個區塊標記傳輸順序，接著就會按照順序來傳輸區塊。 那麼input stream 會是？  ->->-> `特定程式的輸入部分會以stream方式來接收`

#🧠 stream 具體會是將資料以二進制切分好幾個區塊，並為每個區塊標記傳輸順序，接著就會按照順序來傳輸區塊。 那麼output stream 會是？ ->->-> `特定程式會以stream方式來輸出處理結果`


#🧠 stream 原意為某項東西的連續性流動，在這裡會是指資料上的連續性流動，好處是什麼？ ->->-> `資料傳輸失敗的話，可以根據傳輸失敗的序列號碼重新傳遞，而不用整個資料傳遞過去`

#🧠 pipe 在電腦科學裡，具體為？ ->->-> `在電腦科學中，管子裡會有代表資料上的連續性流動(stream)，而管子會將stream以單個方向從一個process的輸出出口導向至另一個process的輸入入口`

#🧠 pipe 在電腦科學裡替stream做什麼？ ->->-> `就是決定stream流動方向導向至特定方向的技術`

#🧠 pipe 在實現概念上能否實現特定程式的傳遞/接收 ->->-> `pipe 在實現上，只能以單方向傳輸，不能夠逆流，但可以建立另一個pipe來構成可以逆流的方向。`


#🧠 stream 套用在作業系統的話，會是如何解釋？ ->->-> `stream 只是一個作業系統層級的抽象傳輸概念，專門以類似stream的方式來處理特定程式的接收資料和輸出資料`

#🧠 stream 與pipe 相比，各是什麼意思->->-> `一個是資料上的流動，另一個則是固定流動方向導向在哪的介面`

#🧠 pipe 若以方向1傳輸資料，那麼能否以方向1的反方向來在同樣的pipe流動 ->->-> `不能`

#🧠 pipe 套用在作業系統以及stream的話，會是如何解釋？->->-> `pipe 具體是將多個stream連接在一起的技術，案例：將一個程式A的輸出流轉移至另一個程式B的輸入流，這樣導向會將程式A的輸出結果以stream的方式輸出，並且直接導入至程式B的輸入部分，而程式B的輸入部分也是以stream來接收。`

---
Status: #🌱 
Tags:
[[Operating System]]
Links:
References:
[[@WhatDifferencePiping]]
[[@techtargetWhatPipeDefinition]]
[[@maxWhatArePrimary]]
[[@wikidataStreamComputing2020]]