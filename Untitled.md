## 描述


  

### stream


> In computer science, a stream is a sequence of data elements made available over time. A stream can be thought of as items on a conveyor belt being processed one at a time rather than in large batches. 

1. stream 原本是形容人事物的連續上流動，在電腦科學裡會是將stream運用在資料上的處理，並想像成 **每筆資料就像是輸送帶上的每一個要被處理的產品/項目，而每一次輸送帶只會一次把一個項目傳遞至指定地方處理，而一次把大量項目傳遞至指定地方處理**，或者說引申為stream是指資料處理上會依照序列的順序來處理每筆資料的處理，而非一次處理大量資料。

> a continuous flow of things or people




### pipe

> In computer programming, especially in [UNIX](https://www.techtarget.com/searchdatacenter/definition/Unix) operating systems, a pipe is a technique for passing information from one program [process](https://www.techtarget.com/whatis/definition/process) to another. Unlike other forms of interprocess communication (IPC), a pipe is one-way communication only. Basically, a pipe passes a parameter such as the output of one process to another process which accepts it as input. The system temporarily holds the piped information until it is read by the receiving process.

> For two-way communication between processes, two pipes can be set up, one for each direction. A limitation of pipes for interprocess communication is that the processes using pipes must have a common parent process (that is, share a common open or initiation process and exist as the result of a _fork_ system call from a parent process).


### stream vs pipeline vs. pipe 命名緣由

[[@WhatDifferencePiping]] ：
pipeline
> The pipeline is a series of straight pipes welded together over a long distance

pipe
> a tube inside which liquid or gas flows from one place to another

stream
> A stream can be thought of as items on a conveyor belt being processed one at a time rather than in large batches.

### stream vs. pipeline vs. pipe

> Streams are an operating system abstraction to make dealing with input and output easier. Instead of needing to deal with all sorts of IO (like files, stdin and stdout, and sockets) in different ways, there is a common abstraction of a byte stream.

> The pipe in general is a way of connecting streams. a mechanism by which the output stream of one process becomes an input stream of another process. The most common example is the pipe operator in the terminal, which allows you to connect the stdout (standard output stream) of the process on the left to the stdin (standard input stream) of the process on the right.


## 複習
#🧠 Question :: ->->-> ``

---
Status: #🌱 
Tags:
[[Operating System]]
Links:
References:
[[@WhatDifferencePiping]]