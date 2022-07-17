



## 描述

[[@wikidataCouplingComputerProgramming]] 所描述：
> 耦合性（英語：Coupling，Dependency）或稱耦合力或耦合度，是一種軟體度量，是指一程式中，模組及模組之間資訊或參數依賴的程度。

> In software engineering, coupling is the degree of interdependence between software modules; a measure of how closely connected two routines or modules are;[1] the strength of the relationships between modules

重點：
- Coupling 是一種衡量模組間在模組內部的相互依賴程度
- 每一個模組會由許多程式區塊所組成
- 若Coupling程度越高，就代表著模組內的依賴於其他模組的程式區塊的程式區塊數就越多，反之，若Coupling程度越低，就代表著模組內的依賴於其他模組的程式區塊的程式區塊數就越少


![](https://media.geeksforgeeks.org/wp-content/uploads/Untitled-28.png)
### coupling & couple 原意
couple
> to join or combine

重點：
- 動詞，主要是描述組合/連接，將事物A組合/連接至另一個事物B

### 耦合性帶來的缺失


[[@wikidataCouplingComputerProgramming]] 所描述：

> 緊密耦合的系統在開發階段有以下的缺點：
> 1.  一個模組的修改會產生漣漪效應，其他模組也需隨之修改。
> 2. 由於模組之間的相依性，模組的組合會需要更多的精力及時間。
> 3. 由於一個模組有許多的相依模組，模組的可復用性低。


> Tightly coupled systems tend to exhibit the following developmental characteristics, which are often seen as disadvantages:
>
> 1.  A change in one module usually forces a ripple effect of changes in other modules.
> 2.  Assembly of modules might require more effort and/or time due to the increased inter-module dependency.
> 3.  A particular module might be harder to reuse and/or test because dependent modules must be included.


重點：
- 程式模組的小改變總是會跟著改變

## 複習
#🧠 Question :: ->->-> ``

---
Status: #🌱 
Tags:
[[Software Engineering]]
Links:
References:
[[@wikidataCouplingComputerProgramming]]
