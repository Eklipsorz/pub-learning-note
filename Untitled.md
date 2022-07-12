





## 描述
[[@cidadeAnswerWhatDoes2008]] 所描述的
> A JIT compiler runs **after** the program has started and compiles the code (usually bytecode or some kind of VM instructions) on the fly (or just-in-time, as it's called) into a form that's usually faster, typically the host CPU's native instruction set. A JIT has access to dynamic runtime information whereas a standard compiler doesn't and can make better optimizations like inlining functions that are used frequently.

> This is in contrast to a traditional compiler that compiles **all** the code to machine language **before** the program is first run.

> To paraphrase, conventional compilers build the whole program as an EXE file BEFORE the first time you run it. For newer style programs, an assembly is generated with [pseudocode](https://www.zhihu.com/search?q=pseudocode&search_source=Entity&hybrid_search_source=Entity&hybrid_search_extra=%7B%22sourceType%22%3A%22answer%22%2C%22sourceId%22%3A112968115%7D) (p-code). Only AFTER you execute the program on the OS (e.g., by double-clicking on its icon) will the (JIT) compiler kick in and generate machine code (m-code) that the Intel-based processor or whatever will understand.


![](https://pic2.zhimg.com/80/fc2d6adee7cfd35cd691b0a419dcd1a2_720w.jpg?source=1940ef5c)


1. Just-In-Time compilation 是指在即將執行時就進行編譯，然後編譯完畢後，就存在快取，無需重新編譯，除非編譯前的程式碼是不同
2. Just-In-Time compilation 並不局限於執行之前，而是指特定程式碼在被執行前，



## 複習
#🧠 Question :: ->->-> ``

---
Status: #🌱 
Tags:
[[Operating System]]
Links:
References:
[[@cidadeAnswerWhatDoes2008]]
[[@wikidataJustintimeCompilation2022]]