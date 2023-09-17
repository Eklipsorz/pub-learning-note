
## 描述

[[@keesdijkAnswerAreTerms2012]]
> These definitions come from the ISO 9126 Standard, which divides in characteristics and sub characteristics : this [table](http://www.sqa.net/iso9126.html) , this [pdf](http://www.essi.upc.edu/~webgessi/publicacions/SMEF%2704-ISO-QualityModels.pdf) or [wikipedia](http://en.wikipedia.org/wiki/ISO/IEC_9126) or [article](http://mileiko.com/requirements-types/non-functional-requirements/)
> Reliability is a main characteristic that contains:

> -   maturity : This sub characteristic concerns frequency of failure of the software.
> -   fault tolerance : The ability of software to withstand (and recover) from component, or environmental, failure.
> -   recoverability : Ability to bring back a failed system to full operation, including data and network connections.

[[@KeKaoDuWeiJiBaiKeZiYouDeBaiKeQuanShu]]
> 可靠度（英語：Reliability），指產品在規定的條件下和規定的時間內，無差錯地完成規定任務的概率

[[@RuanTiKeKaoXingRuanTiKeKaoXingYingWenMingChengsoftware]]
> 軟體可靠性（英文名稱software reliability），計算機術語，指在規定的條件下和規定的時間內，軟體不引起系統故障的能力。軟體可靠性不但與軟體存在差錯有關，而且與系統輸入和系統使用有關。1983年美國IEEE計算機學會對“軟體可靠性”作出了明確定義，此後該定義被美國標準化研究所接受為國家標準，1989年中國也接受該定義為國家標準。



> 1983年美國IEEE計算機學會對“軟體可靠性”作出了明確定義，此後該定義被美國標準化研究所接受為國家標準，1989年中國也接受該定義為國家標準。該定義包括兩方面的含義：

> （1）在規定的條件下，在規定的時間內，軟體不引起系統失效的機率；
> （2）在規定的時間周期內，在所述條件下程式執行所要求的功能的能力；

[[@Reliability]]
> # Reliability

> Degree to which a system, product or component performs specified functions under specified conditions for a specified period of time. This characteristic is composed of the following sub-characteristics:

> -   **Maturity -** Degree to which a system, product or component meets needs for reliability under normal operation.
>-   **Availability -** Degree to which a system, product or component is operational and accessible when required for use.
>-   **Fault tolerance -** Degree to which a system, product or component operates as intended despite the presence of hardware or software faults.
>-   **Recoverability -** Degree to which, in the event of an interruption or a failure, a product or system can recover the data directly affected and re-establish the desired state of the system.




重點：
- Reliability 泛指著使用者對於特定軟體執行出預期結果所能信賴的程度，具體定義分別為如下：
	- 在規定條件下和規定的時間內，軟體不引起系統失效的機率 
	- 在規定條件下和規定的時間內，軟體能夠得到預期結果的能力或者程度
- 該Reliability會以下面的效能指標來判斷好壞
	- maturity ：是指特定應用程式在正常執行情況下所能達到預期結果的程度
	- availability：是指當使用方需要特定應用程式的結果時，使用者獲取其結果的容易程度。
	- fault tolerance：是指特定應用程式承受故障並從中恢復正常功能的能力
	- recoverability：能夠將故障的系統還原至該系統能夠完整提供功能和服務的能力
	- fault toerance vs. recoverability：前者強調面對故障還能正常服務的能力；後者則是從故障狀態恢復到提供完整正常功能的狀態
### Reliability 命名緣由

> the quality of being able to be trusted or believed because of working or behaving well 
> the quality of being able to be trusted to do what somebody wants or needs


重點：
- 特定事物能夠被信賴去達到特定結果的信賴程度

### maturity 命名緣由

> Maturity is the state of being fully developed

重點：
- Maturity 是指特定事物在特定層面下的完整發展程度

### tolerance 命名緣由

> the ability to suffer something, especially pain, difficult conditions

重點：
- tolerance 是指承受疼痛、故障、困難情況的承受能力


### recoverability 命名緣由

> The property of being able to recover or be recovered.

重點：
- recoverability 是指特定事物在面對遭遇疼痛、故障等情況時能夠恢復到遭遇前的程度或者恢復到正常執行的程度


### availability

> the fact that something is possible to get, buy or find

重點：
- 獲得特定事物的容易程度

## 複習

#🧠 maturity 命名緣由為何？->->-> `Maturity 是指特定事物在特定層面下的完整發展程度`
<!--SR:!2023-10-26,107,190-->

#🧠 tolerance 命名緣由為何？ ->->-> `tolerance 是指承受疼痛、故障、困難情況的承受能力`
<!--SR:!2024-05-01,295,250-->

#🧠 recoverability 命名緣由為何？ ->->-> `是指特定事物在面對遭遇疼痛、故障等情況時能夠恢復到遭遇前的程度或者恢復到正常執行的程度`
<!--SR:!2023-10-15,180,250-->

#🧠 Reliability 命名緣由為何 ->->-> `特定事物能夠被信賴去達到特定結果的信賴程度`
<!--SR:!2023-09-28,57,210-->

#🧠 Reliability 在電腦科學上會是指什麼？ ->->-> `使用者對於特定軟體執行出預期結果所能信賴的程度`
<!--SR:!2024-04-21,285,250-->

#🧠 availability 命名緣由為何？ ->->-> `獲得特定事物的容易程度`
<!--SR:!2024-03-13,246,230-->


#🧠 Reliability 在電腦科學上會是指使用者對於特定軟體執行出預期結果所能信賴的程度，為了很好地評估而量化，所以區分兩種，請問兩者為何？？->->-> `	- 在規定條件下和規定的時間內，軟體不引起系統失效的機率  - 在規定條件下和規定的時間內，軟體能夠得到預期結果的能力或者程度`
<!--SR:!2024-01-29,180,244-->


#🧠 Reliability 在電腦科學上會是指使用者對於特定軟體執行出預期結果所能信賴的程度，為何要額外分成	- 在規定條件下和規定的時間內，軟體不引起系統失效的機率  - 在規定條件下和規定的時間內，軟體能夠得到預期結果的能力或者程度？ ->->-> `為了很好地評估而量化`
<!--SR:!2023-12-12,211,250-->


#🧠 Reliability 在電腦科學上會是指使用者對於特定軟體執行出預期結果所能信賴的程度，具體會是在規定條件下和規定的時間內，軟體能夠得到預期結果的能力或者程度，這項準則還能切分出 ->->-> `maturity、availabilty、fault tolerance、recoverability`
<!--SR:!2023-10-01,14,170-->

#🧠 Reliability 在電腦科學上會是指使用者對於特定軟體執行出預期結果所能信賴的程度，具體會是在規定條件下和規定的時間內，軟體能夠得到預期結果的能力或者程度，這項準則還能切分出maturity、availabilty、fault tolerance、recoverability，他們各為什麼？ ->->-> `	- maturity ：是指特定應用程式在正常執行情況下所能達到預期結果的程度 - availability：是指當使用方需要特定應用程式的結果時，使用者獲取其結果的容易程度。 - fault tolerance：是指特定應用程式承受故障並從中恢復正常功能的能力 - recoverability：能夠將故障的系統還原至該系統能夠完整提供功能和服務的能力`
<!--SR:!2023-10-31,180,230-->

#🧠 fault tolerance vs. recoverability 在電腦應用程式的效能評估之不同為？->->-> `前者強調面對故障還能正常服務的能力；後者則是從故障狀態恢復到提供完整正常功能的狀態`
<!--SR:!2023-12-16,215,250-->










---
Status: #🌱 
Tags:
[[Operating System]]
Links:
References:
[[@keesdijkAnswerAreTerms2012]]
[[@KeKaoDuWeiJiBaiKeZiYouDeBaiKeQuanShu]][[@RuanTiKeKaoXingRuanTiKeKaoXingYingWenMingChengsoftware]]
[[@Reliability]]