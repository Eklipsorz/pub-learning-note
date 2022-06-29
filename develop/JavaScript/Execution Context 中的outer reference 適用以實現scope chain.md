## 描述
[[@sumudusiriwardanadeveloperadvocateWhatScopeScope]] 所描述

> The scope chain is how Javascript looks for variables. When looking for variables through the nested scope, the inner scope first looks at its own scope. If the variable is not assigned locally, which is inside the inner function or block scope, then JavaScript will look at the outer scope of said function or block to find the variable. If Javascript could not find the variable in any of the outer scopes on the chain, it will throw a reference error.


重點：
- scope chain 是用來幫助JavaScript 引擎在每個Execution context 找到每個識別字對應到哪
- 首先引擎會在當前所處的Execution context 來找尋識別字對應到哪，找到就以所處的Execution context為主，找不到就以呼叫該Execution context的Execution contextA 是否擁有該識別字，在找不到就以呼叫Execution context A的Execution context B來找
- 具體實現會是以Execution Context 中的 Outer reference是用來實現scope chain，每一次建立Execution Context A時，Execution Context A都會透過Outer reference來紀錄Execution Context A所處的Execution Context，這樣子往後找不到可以透過outer所指向的EC來尋找



## 複習
#🧠 JavaScript： scope chain 是用來做什麼的？ ->->-> `是用來幫助JavaScript 引擎在每個Execution context 找到每個識別字對應到哪`

#🧠 JavaScript 引擎如何運用scope chain 來找到每個識別字？ ->->-> `首先引擎會在當前所處的Execution context 來找尋識別字對應到哪，找到就以所處的Execution context為主，找不到就以呼叫該Execution context的Execution contextA 是否擁有該識別字，在找不到就以呼叫Execution context A的Execution context B來找`

#🧠  JavaScript 引擎：如何實現scope chain 來找到每個識別字？ ->->-> `具體實現會是以Execution Context 中的 Outer reference是用來實現scope chain，每一次建立Execution Context A時，Execution Context A都會透過Outer reference來紀錄Execution Context A所處的Execution Context，這樣子往後找不到可以透過outer所指向的EC來尋找`


---
Status: #🌱 
Tags:
[[JavaScript]]
Links:
[[JavaScript 的 Execution context 是指目前程式執行時的環境，該環境會包含著執行時所需的參數、狀態]]
References:
[[@sumudusiriwardanadeveloperadvocateWhatScopeScope]]

