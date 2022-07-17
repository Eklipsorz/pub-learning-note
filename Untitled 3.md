



## 描述

[[@wikidataCouplingComputerProgramming]] 所描述：
> 耦合性（英語：Coupling，Dependency）或稱耦合力或耦合度，是一種軟體度量，是指一程式中，模組及模組之間資訊或參數依賴的程度。

> In software engineering, coupling is the degree of interdependence between software modules; a measure of how closely connected two routines or modules are;[1] the strength of the relationships between modules

重點：
- Coupling 是一種衡量模組間在模組間的**相互**依賴程度，以此衡量其依賴程度是否會影響模組的預期結果不如預期以及其影響範疇為何？
- 依賴是指存取、使用：
	- 模組A 和 模組B 任一個模組都沒存取另一個，那麼代表著A和B並不會彼此影響各自的預期結果
	![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1658066921/blog/SoftwareEngineering/AB-NoCoupling_wrtd6f.png)
	- 模組A 單方面存取 模組B 意旨為 模組A 單方面依賴 模組B，當A去存取B時有可能改變著B的預期結果，因A有可能改變著決定結果的因素，而因素就在B裡頭
	![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1658066921/blog/SoftwareEngineering/A-to-B-Coupling_uvdngb.png)

	-  模組B 單方面存取 模組A 意旨為 模組B 單方面依賴 模組A，當B去存取A時有可能改變著A的預期結果，因B有可能改變著決定結果的因素，而因素就在A裡頭
	![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1658066921/blog/SoftwareEngineering/B-to-A-Coupling_kyjuju.png)
	- 模組A 單方面存取 模組B 以及 模組B 單方面存取 模組B ，當A去存取B時有可能改變著B的預期結果，而B可能會因預期結果的改變而變更存取 A的方式，使B可能使用錯誤的存取方式來改變著A，甚至A下次執行時存取B會使情況更加惡化。
	![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1658066921/blog/SoftwareEngineering/AB-Coupling_t2ncqi.png)
- 由於每一個模組會由許多程式區塊所組成，每個程式區塊都有可能使用另一個模組下的程式區塊或者同一個模組下的程式區塊：
	- Coupling 就不存在：若所有模組下的所有程式區塊都沒使用其他模組下的任一程式區塊(如第一張圖)
	- Coupling 存在：若只要模組的程式區塊去存取另一個模組的任一區塊(如第二張圖)
	- Coupling 存在且Coupling 程度較高：若模組間的彼此使用頻繁，就增加改變模組預期結果的可能性，如同模組A和模組C原本就只有A使用C、C和A，但隨著後續開發而使得C多使用A的程式區塊，而這使得A和C之間的Coupling 程度增加

![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1658067459/blog/SoftwareEngineering/coupling-degree_kktjsk.png)
- 若Coupling程度越高，就代表著模組內的依賴於其他模組的程式區塊的程式區塊數就越多，反之，若Coupling程度越低，就代表著模組內的依賴於其他模組的程式區塊的程式區塊數就越少


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
