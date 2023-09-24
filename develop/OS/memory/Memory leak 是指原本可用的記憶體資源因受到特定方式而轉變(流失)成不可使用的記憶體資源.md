

## 描述




### leak 意義

>  to allow liquid or gas to get in or out through a small hole or crack

重點: 
- 在探討物體是還能使用的情況下，特定事物透過特定方式來減少自身的數量和品質以漸漸無法使用特定事物 之 行為或者動作
### Memory leak 
[[@WhatMemoryLeak2010]]
> Memory leak occurs when programmers create a memory in a heap and forget to delete it.

> The consequence of the memory leak is that it reduces the performance of the computer by reducing the amount of available memory. Eventually, in the worst case, too much of the available memory may become allocated and all or part of the system or device stops working correctly, the application fails, or the system slows down vastly.

> Memory leaks are particularly serious issues for programs like daemons and servers which by definition never terminate.

[[@MemoryLeak2023]]
> In computer science, a memory leak is a type of resource leak that occurs when a computer program incorrectly manages memory allocations in a way that memory which is no longer needed is not released. A memory leak may also happen when an object is stored in memory but cannot be accessed by the running code (i.e. unreachable memory). A memory leak has symptoms similar to a number of other problems and generally can only be diagnosed by a programmer with access to the program's source code.

重點:
- Memory leak 中文為 記憶體資源流失
- Memory leak 的 leak 是指系統資源層面的流失
- Memory leak 是指原本可用的記憶體資源因受到特定方式而轉變(流失)成不可使用的記憶體資源
	- 特定方式為: 不當的作業系統本身之記憶體管理、不當的應用程式之記憶體管理
	- 其最終結果會是系統會誤判記憶體資源而導致部分程式無法正常執行或者無法有效率地執行。
## 複習
#🧠 leak 是甚麼意思 ->->-> `在探討物體是還能使用的情況下，特定事物透過特定方式來減少自身的數量和品質以漸漸無法使用特定事物 之 行為或者動作`
<!--SR:!2023-11-21,58,230-->

#🧠 Memory leak 是甚麼意思 ->->-> `原本可用的記憶體資源因受到特定方式而轉變(流失)成不可使用的記憶體資源`
<!--SR:!2023-10-14,44,250-->

#🧠  Memory leak 是指原本可用的記憶體資源因受到特定方式而轉變(流失)成不可使用的記憶體資源，請問特定方式為何?  ->->-> `不當的作業系統本身之記憶體管理、不當的應用程式之記憶體管理`
<!--SR:!2023-10-28,55,250-->

#🧠 Memory leak 是指原本可用的記憶體資源因受到特定方式而轉變(流失)成不可使用的記憶體資源，最後這會導致甚麼樣的結果? ->->-> `其最終結果會是系統會誤判記憶體資源而導致部分程式無法正常執行或者無法有效率地執行`
<!--SR:!2023-09-25,26,230-->

#🧠 Memory leak是屬於哪種流失 ->->-> `系統資源可不可用的層面`
<!--SR:!2023-10-27,54,250-->

---
Status: #🌱 
Tags:
Links:
References:

[[@WhatMemoryLeak2010]]
[[@MemoryLeak2023]]