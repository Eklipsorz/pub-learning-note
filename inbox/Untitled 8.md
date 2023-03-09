## 描述

[[@VmImplementationInterpreters]]
> Virtual Machine can refer to several things, the two I am aware of:

> - Hypervisor-related virtual machine, such as Hyper-V, Xen. These allow you to run several OS on a single piece of hardware
> 
> - Software run time, like Java Virtual Machine, Common Language Runtime. This piece of software allow one to run platform independent intermediate language (IL code, byte code) and execute machine-specific instructions (just-in-time compilation). Usually, such VM is responsible for other satellite tasks: resource management, memory clean up, threading, security etc

重點：
- 在程式碼執行層面來說，Virtual Machine 是一種程式模組，主要為
	- 允許production code擁有跨平台執行的功能
- 允許之前，每個production code在執行前都會受限於 **本機端和其作業系統是否能夠解析並執行**，而做出將code編譯成該機台能夠執行成功的代碼形式
- 允許production code擁有跨平台執行的功能，具體會是：
	- 主要提供一個平台和其平台能解析並執行的語言體系A，並藉著安裝其平台至特定作業系統上以及將語言體系轉換成其作業系統上能夠解析執行的方式，就能所有以語言體系A包裝的production code 不受到**本機端和其作業系統是否能夠解析並執行** ，並且省去將code編譯成該機台能夠執行成功的代碼形式
- 舉例
![](https://pic2.zhimg.com/80/fc2d6adee7cfd35cd691b0a419dcd1a2_720w.jpg?source=1940ef5c)
## 複習


---
Status: #🌱 
Tags:
[[Operating System]]
Links:
References:
[[@VmImplementationInterpreters]]