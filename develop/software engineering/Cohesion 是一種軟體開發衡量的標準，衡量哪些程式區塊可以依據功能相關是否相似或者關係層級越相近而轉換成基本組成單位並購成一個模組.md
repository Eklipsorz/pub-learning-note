




## 描述
[[@wikidataCohesionComputerScience2021]] 所描述的：
> In computer programming, cohesion refers to the degree to which the elements inside a module belong together.
> 
> In one sense, it is a measure of the strength of relationship between the methods and data of a class and some unifying purpose or concept served by that class.
> 
> In another sense, it is a measure of the strength of relationship between the class's methods and data themselves.


> 內聚性（Cohesion）也稱為內聚力，是一軟體度量，是指機能相關的程式組合成一模組的程度，或是各機能凝聚的狀態或程度。

高內聚性的評估目的為：
> 在一個高內聚性的系統中，代碼可讀性及復用的可能性都會提高，程式雖然複雜，但可被管理。


重點：
- cohesion 是一種軟體開發衡量的標準，衡量哪些程式區塊可以依據功能相關程度是否相近而轉換成基本組成單位並購成一個模組，具體來說cohesion是程式區塊間的功能相關程度
- 程式區塊間的cohesion越高，代表這些程式區塊可以組合成一個模組來管理/使用，程式區塊間的cohesion越低，代表這些程式區塊很難可以組合成一個模組來管理/使用
- cohesion 主要目的為藉由功能關係相近來將程式區塊轉化基本組成單位來匯聚成一個模組進行管理，並且在模組下，轉化後的程式區塊在開發上的易讀性和重複使用率會提高





### Cohesion 原意

> the situation when the members of a group or society are united

重點：
- 一個群體下的成員能夠凝聚成群體的程度，該程度主要會是成員間的相關性程度，關係層級越接近，就代表著越能與其他成員匯聚成一個群體

## 複習
#🧠 Cohesion 原意 是什麼？ ->->-> `一個群體下的成員能夠凝聚成群體的程度，該程度主要會是成員間的相關性程度，關係層級越接近，就代表著越能與其他成員匯聚成一個群體`
<!--SR:!2022-07-21,3,250-->

#🧠 電腦科學裡的cohesion是什麼意思？ ->->-> `cohesion 是一種軟體開發衡量的標準，衡量哪些程式區塊可以依據功能相關程度是否相近而轉換成基本組成單位並購成一個模組，具體來說cohesion是程式區塊間的功能相關程度`
<!--SR:!2022-07-29,8,250-->

#🧠 電腦科學裡的cohesion程度越高代表著？->->-> `程式區塊間的cohesion越高，代表這些程式區塊可以組合成一個模組來管理/使用`
<!--SR:!2022-07-29,8,250-->

#🧠 電腦科學裡的cohesion程度越低代表著？ ->->-> `程式區塊間的cohesion越低，代表這些程式區塊很難可以組合成一個模組來管理/使用`
<!--SR:!2022-07-30,9,250-->

#🧠 當多個程式區塊的功能較相關的話，可以將多個程式區塊做些什麼處理來管理？->->-> `將程式區塊轉化基本組成單位來匯聚成一個模組進行管理，並且在模組下，轉化後的程式區塊在開發上的易讀性和重複使用率會提高`
<!--SR:!2022-07-23,2,230-->

#🧠 電腦科學裡的cohesion 提出目的是什麼？->->-> `cohesion 主要目的為藉由功能關係相近來將程式區塊轉化基本組成單位來匯聚成一個模組進行管理，並且在模組下，轉化後的程式區塊在開發上的易讀性和重複使用率會提高`
<!--SR:!2022-07-27,6,250-->

---
Status: #🌱 
Tags:
[[Software Engineering]]
Links:
[[Coupling 是一種衡量多個模組間的相互存取程度，以此衡量其存取程度是否會影響模組的預期結果不如預期以及其影響範疇為何]]
References:
[[@wikidataCohesionComputerScience2021]]