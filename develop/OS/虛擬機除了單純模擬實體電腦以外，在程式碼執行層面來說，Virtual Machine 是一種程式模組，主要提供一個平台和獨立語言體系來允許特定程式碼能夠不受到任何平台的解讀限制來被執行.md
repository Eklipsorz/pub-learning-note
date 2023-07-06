## 描述


[[@VmImplementationInterpreters]]
> Virtual Machine can refer to several things, the two I am aware of:

> - Hypervisor-related virtual machine, such as Hyper-V, Xen. These allow you to run several OS on a single piece of hardware
> 
> - Software run time, like Java Virtual Machine, Common Language Runtime. This piece of software allow one to run platform independent intermediate language (IL code, byte code) and execute machine-specific instructions (just-in-time compilation). Usually, such VM is responsible for other satellite tasks: resource management, memory clean up, threading, security etc

重點：
- 除了單純模擬實體電腦以外，在程式碼執行層面來說，Virtual Machine 是一種程式模組，主要為
	- 允許production code擁有跨平台執行的功能
- 允許之前，每個production code在執行前都會受限於 **本機端和其作業系統是否能夠解析並執行**，而做出將code編譯成該機台能夠執行成功的代碼形式
- 允許production code擁有跨平台執行的功能，具體會是：
	- 主要提供一個模擬實體機行為的平台和其平台能解析並執行的語言體系A，並藉著安裝其平台至特定作業系統上以及將語言體系轉換成其作業系統上能夠解析執行的方式，就能所有以語言體系A包裝的production code 丟給其平台來執行，平台執行時會將其code轉換成自己所在的作業系統所能解讀的形式來執行，進而不受到**本機端和其作業系統是否能夠解析並執行** ，並且省去將code編譯成該機台能夠執行成功的代碼形式
- 用途：一個模擬實體機行為的平台和其平台能解析並執行的語言體系A 
	- 前者是以語言體系A來解讀和執行，並轉換成宿主環境能夠解讀的形式來調用對應資源給需求方
	- 後者則是被定調成該平台能夠解讀的機械碼形式(對他認為的)
- 舉例：
![](https://pic2.zhimg.com/80/fc2d6adee7cfd35cd691b0a419dcd1a2_720w.jpg?source=1940ef5c)
## 複習

#🧠 除了單純模擬實體電腦以外，在程式碼執行層面來說，Virtual Machine會是什麼？主要做啥？ ->->-> `- 在程式碼執行層面來說，Virtual Machine 是一種程式模組，主要為 - 允許production code擁有跨平台執行的功能`
<!--SR:!2023-06-24,67,250-->

#🧠 在程式碼執行層面來說，Virtual Machine 是一種程式模組，主要為 - 允許production code擁有跨平台執行的功能，具體會是什麼？->->-> `主要提供一個平台和其平台能解析並執行的語言體系A，並藉著安裝其平台至特定作業系統上以及將語言體系轉換成其作業系統上能夠解析執行的方式，就能所有以語言體系A包裝的production code 丟給其平台來執行，平台執行時會將其code轉換成自己所在的作業系統所能解讀的形式來執行，進而不受到**本機端和其作業系統是否能夠解析並執行** ，並且省去將code編譯成該機台能夠執行成功的代碼形式`
<!--SR:!2023-11-04,135,230-->

#🧠 在程式碼執行層面來說，Virtual Machine 是一種程式模組，主要為 - 允許production code擁有跨平台執行的功能，那麼在允許之前，程式碼和平台執行會是如何？ ->->-> `允許之前，每個production code在執行前都會受限於 **本機端和其作業系統是否能夠解析並執行**，而做出將code編譯成該機台能夠執行成功的代碼形式`
<!--SR:!2024-01-03,180,250-->


#🧠 請用下面圖來說明Virtual Machine 做了什麼![](https://pic2.zhimg.com/80/fc2d6adee7cfd35cd691b0a419dcd1a2_720w.jpg?source=1940ef5c) ->->-> ``
<!--SR:!2024-01-11,188,250-->


#🧠 在程式碼執行層面來說，Virtual Machine 是一種程式模組，主要為 - 允許production code擁有跨平台執行的功能，其跨平台的好處是什麼？ ->->-> `主要省去將code編譯成該機台能夠執行成功的代碼形式`
<!--SR:!2024-01-12,189,250-->

#🧠 在程式碼執行層面來說，Virtual Machine 是一種程式模組，主要為 - 允許production code擁有跨平台執行的功能，通常會是由什麼元件組成？其元件是用作什麼 ->->-> `主要提供一個模擬實體機行為的平台和其平台能解析並執行的語言體系A。前者是以語言體系A來解讀和執行，並轉換成宿主環境能夠解讀的形式來調用對應資源給需求方、後者則是被定調成該平台能夠解讀的機械碼形式(對他認為的)`
<!--SR:!2023-06-13,54,230-->




---
Status: #🌱 
Tags:
[[Operating System]]
Links:
References:
[[@VmImplementationInterpreters]]