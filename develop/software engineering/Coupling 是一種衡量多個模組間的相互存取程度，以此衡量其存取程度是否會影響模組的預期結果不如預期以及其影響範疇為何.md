
## 描述

[[@wikidataCouplingComputerProgramming]] 所描述：
> 耦合性（英語：Coupling，Dependency）或稱耦合力或耦合度，是一種軟體度量，是指一程式中，模組及模組之間資訊或參數依賴的程度。

> In software engineering, coupling is the degree of interdependence between software modules; a measure of how closely connected two routines or modules are;[1] the strength of the relationships between modules

重點：
- Coupling 是一種軟體開發衡量標準
- Coupling 是一種衡量多個模組下的程式區塊之間的連接(呼叫/使用的)密集程度，以此衡量其存取程度是否會影響模組的預期結果不如預期以及其影響範疇為何
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
- 若Coupling程度越高，就代表著模組內的使用自其他模組的程式區塊的程式區塊數就越多，反之，若Coupling程度越低，就代表著模組內的使用自其他模組的程式區塊的程式區塊數就越少
- Coupling 程度高的話，可被稱呼為tight coupling (緊密耦合)
- Coupling 程度低的話，可被稱呼為loose coupling (鬆散耦合)


### tight coupling 案例

在這裡有兩張圖，每張圖都各有兩個模組分別為模組A和模組B，每個模組都有各自的程式區塊來組成，每個程式區塊皆使用一條線來表示使用關係，上圖架構上的coupling 程度較低，下圖架構上的coupling 程度較高。

上圖：假設B的B1想要使用A的A1的話，那麼較好的情況就是只會影響模組A，最糟糕的話，是A也使用B的B1，那麼就會可能以不如預期的方式來使用B1並可能改變B

下圖：假設B的B1想要使用A的A1的話，很有可能因為使用方向的關係而把影響範疇延伸至都會影響兩個模組，至少可能影響的機率會比上圖來得高，如B1改變A1，而A1改變A2，接著A2改變B5，B5改變著B4，後面以此類推。

![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1658068933/blog/SoftwareEngineering/tight-coupling-example_iumhzq.png)

### coupling & couple 原意
couple
> to join or combine

重點：
- 動詞，主要是描述組合/連接，將事物A組合/連接至另一個事物B

coupling 
- 動名詞，主要描述著組合/連接的程度

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


重點：在tight coupling 架構下所會有的缺失
- 程式模組A的一小個改變會影響其他程式模組下的程式區塊使用A的情形
- coupling 程度越高，開發/維護成本就會提高
- 若一個模組A下的大部分程式區塊都使用著其他模組下的程式區塊，代表著模組A本身存在重複使用率低的疑慮

## 複習
#🧠 Coupling 原意是什麼？可以先描述couple，在來描述coupling ->->-> `couple 為動詞，主要是描述組合/連接，將事物A組合/連接至另一個事物B，coupling 為 動名詞，主要描述著組合/連接的程度`
<!--SR:!2023-04-03,46,190-->

#🧠 電腦科學裡的多個程式模組只要開始使用著對方模組，就會有coupling情形以及coupling帶來的缺失，為什麼？ ->->-> `因為只要有使用，就代表著程式模組單方面與另一個程式模組連接，而這樣就有可能因為使用而改變對方模組，進而讓對方模組在未來的預期結果不如預期`
<!--SR:!2023-05-15,189,250-->

#🧠 電腦科學裡的coupling  是什麼？ 其目的做啥->->-> `Coupling 是一種衡量多個模組下的程式區塊之間的連接(呼叫/使用的)密集程度，以此衡量其存取程度是否會影響模組的預期結果不如預期以及其影響範疇為何`
<!--SR:!2023-05-31,192,250-->

#🧠 電腦科學裡的coupling：依賴會是什麼意思 ->->-> `存取、使用`
<!--SR:!2023-05-17,189,250-->


#🧠 電腦科學裡的coupling：假如有模組A和模組B，其依賴狀況為如下，請問有coupling嗎？為何？ ![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1658066921/blog/SoftwareEngineering/AB-NoCoupling_wrtd6f.png)->->-> `並沒有coupling， 由於模組A 和 模組B 任一個模組都沒存取另一個，`
<!--SR:!2023-11-27,301,250-->

#🧠 電腦科學裡的coupling：假如有模組A和模組B，其依賴狀況為如下，請問有coupling嗎？為何	![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1658066921/blog/SoftwareEngineering/A-to-B-Coupling_uvdngb.png) ->->-> `有coupling 程度， 模組A 單方面存取 模組B 意旨為 模組A 單方面依賴 模組B`
<!--SR:!2023-04-28,176,250-->

#🧠 電腦科學裡的coupling：假如有模組A和模組B，其依賴狀況為如下，請問有coupling程度會影響結果嗎？ ![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1658066921/blog/SoftwareEngineering/A-to-B-Coupling_uvdngb.png) ->->-> `，當A去存取B時有可能改變著B的預期結果，因A有可能改變著決定結果的因素，而因素就在B裡頭`
<!--SR:!2024-03-30,375,250-->

#🧠  電腦科學裡的coupling：假如有模組A和模組B，其依賴狀況為如下，請問有coupling嗎？為何 	![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1658066921/blog/SoftwareEngineering/B-to-A-Coupling_kyjuju.png)->->-> `模組B 單方面存取 模組A 意旨為 模組B 單方面依賴 模組A`
<!--SR:!2024-04-30,402,250-->
#🧠 電腦科學裡的coupling：假如有模組A和模組B，其依賴狀況為如下，請問有coupling程度會影響結果嗎？![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1658066921/blog/SoftwareEngineering/B-to-A-Coupling_kyjuju.png) ->->-> `當B去存取A時有可能改變著A的預期結果，因B有可能改變著決定結果的因素，而因素就在A裡頭`
<!--SR:!2024-01-28,340,250-->
#🧠 電腦科學裡的coupling：假如有模組A和模組B，其依賴狀況為如下，請問有coupling嗎？為何	![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1658066921/blog/SoftwareEngineering/AB-Coupling_t2ncqi.png)->->-> `模組A 單方面存取 模組B 以及 模組B 單方面存取 模組B`
<!--SR:!2024-02-28,353,250-->
#🧠 電腦科學裡的coupling：假如有模組A和模組B，其依賴狀況為如下，請問有coupling程度會影響結果嗎？	![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1658066921/blog/SoftwareEngineering/AB-Coupling_t2ncqi.png)->->-> `當A去存取B時有可能改變著B的預期結果，而B可能會因預期結果的改變而變更存取 A的方式，使B可能使用錯誤的存取方式來改變著A，甚至A下次執行時存取B會使情況更加惡化。`
<!--SR:!2024-02-18,351,250-->

#🧠 請問每個模組都由什麼什麼東西來組成？會不會這些基本組成單位就會有coupling問題(提示：程式區塊) ->->-> `由於每一個模組會由許多程式區塊所組成，每個程式區塊都有可能使用另一個模組下的程式區塊或者同一個模組下的程式區塊`
<!--SR:!2023-05-06,182,250-->

#🧠 試著說明第一個下的ABCD模組的coupling情況![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1658067459/blog/SoftwareEngineering/coupling-degree_kktjsk.png)->->-> `Coupling 就不存在：若所有模組下的所有程式區塊都沒使用其他模組下的任一程式區塊`
<!--SR:!2023-04-25,175,250-->

#🧠 試著說明第二個下的ABCD模組的coupling情況，說明連接/使用關係就好 ![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1658067459/blog/SoftwareEngineering/coupling-degree_kktjsk.png) ->->-> `Coupling 存在：若只要模組的程式區塊去存取另一個模組的任一區塊`
<!--SR:!2023-04-26,175,250-->

#🧠 試著說明第三個下的ABCD模組的coupling情況，說明連接/使用關係就好![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1658067459/blog/SoftwareEngineering/coupling-degree_kktjsk.png) ->->-> `Coupling 存在且Coupling 程度較高：若模組間的彼此使用頻繁，就增加改變模組預期結果的可能性，如同模組A和模組C原本就只有A使用C、C和A，但隨著後續開發而使得C多使用A的程式區塊，而這使得A和C之間的Coupling 程度增加`
<!--SR:!2023-03-26,155,250-->


#🧠 coupling 程度高的話，可以稱作為什麼？ ->->-> `tight coupling (緊密耦合)`
<!--SR:!2023-08-15,187,210-->

#🧠 coupling 程度低的話，可以稱作為什麼？ ->->-> `loose coupling (鬆散耦合)`
<!--SR:!2023-05-18,190,250-->


#🧠 緊密耦合的系統在開發階段有以下的缺點 ->->-> ` 1.  一個模組的修改會產生漣漪效應，其他模組也需隨之修改。 2. 由於模組之間的相依性，模組的組合會需要更多的精力及時間。 3. 由於一個模組有許多的相依模組，模組的可復用性低。`
<!--SR:!2023-05-26,67,210-->


#🧠 上圖：假設B的B1想要使用A的A1的話，那麼coupling 會如何影響模組？ (請用較好、平均狀況、較糟的情況下來說明)  ![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1658068933/blog/SoftwareEngineering/tight-coupling-example_iumhzq.png) ->->-> `假設對B的B1想要使用A的A1的話，那麼較好的情況就是只會影響模組A，最糟糕的話，是A也使用B的B1，那麼就會可能以不如預期的方式來使用B1並可能改變B`
<!--SR:!2024-02-15,349,250-->


#🧠 下圖：假設B的B1想要使用A的A1的話，那麼coupling 會如何影響模組？(請用較好、平均狀況、較糟的情況下來說明) ![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1658068933/blog/SoftwareEngineering/tight-coupling-example_iumhzq.png) ->->-> `假設對B的B1想要使用A的A1的話，很有可能因為使用方向的關係而把影響範疇延伸至都會影響兩個模組，至少可能影響的機率會比上圖來得高，如B1改變A1，而A1改變A2，接著A2改變B5，B5改變著B4，後面以此類推。`
<!--SR:!2023-05-08,183,250-->


---
Status: #🌱 
Tags:
[[Software Engineering]]
Links:
[[cohesion 是一種軟體開發衡量的標準，指個多個程式區塊能夠凝聚成模組的程度，主要衡量能否以模組來管理程式區塊]]
References:
[[@wikidataCouplingComputerProgramming]]
