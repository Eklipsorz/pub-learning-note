## 描述


### REST Intro

全名為REpresentational State Transfer，較完整的說法是Resource Representation State Transfer

是一種 **以資源為中心，用HTTP方法操作資源，並且最終目標為打造出滿足於HATEOAS之產品的網路軟體開發風格**

- 背景：當時軟體開發和網路發展皆分別以單機環境下進行以及制定/實現某些系統之間的通信協定，兩者很少有交集
- 目的：方便讓不同軟體或者程式模組在網路上能夠互相傳遞資訊
- 應用於：REST 的狀態轉換是基於HTTP/HTTPS協議。
- 最終目標：當存取到特定資源X時，回應就會包含動態產生出來的一組與特定資源X相關連的API連結，而非以寫死的方式來表達能對特定資源做哪些進一步的操作
- 備註：此為風格，並非需要嚴格遵守的標準。

#### 名詞說明

在這裡選擇完整說法來解釋名詞：

##### Resource
1. 會是指網路上的實體、資源，實體/資源可以是指某組資料、服務、圖片、歌曲，但實際上該字本質上仍停留在用文字概念去描述該實體、資源的存在
2. 在網路上難以用具體的形式去呈現資源(如看、摸、聽)，在這裡會是以 **以URI** 這文字概念來 **描述其實體資源**。

簡短來說，Resource會是指任意形式的實體；在網路上會以Resource所在的URI來表達Resource

##### Representation
1. 是指以某種形式來呈現某人事物，**在這裏會以某種形式來呈現Resource這概念**，換言之就是以某種形式來具體化資源，比如用HTML格式、JSON格式等等

簡短來說，Representation 本身以某種形式來呈現，而Resource Representation 是將Resource概念轉換成更為具體的形式呈現，形式會有HTML格式、JSON格式等等

##### State
1. 由於客戶端和伺服器之間的互動勢必會涉及到不同時間點的資源內容，或許是在某段時間的同份資源A內容會變更，或許是某段時間點的同份資源A內容會移除，這些將會是資源A在不同時間點的內容或者說狀態，最後在這裡會以狀態來描述同份資源在不同時間點下的資源內容。

> 狀態是指某物件在特定時間所會有的情況、資訊。 The particular condition that something is in at a specific time

且由於**該概念是建立在無狀態的HTTP協議上，所以所有的資源都會永久性保留在伺服器，客戶端只會拿到某一個時間點的資源然後就被移除。**


簡短來說，State 是特定時間點下之特定事物所擁有的內容，Resource Representation State 則是指狀態會以特定時間點下的具體資源(所在)所擁有的內容

##### Transfer
1. Transfer 是指某事物在某方面從A轉換至B，而經由前面三個字的形容會是指這些具體化資源之間的狀態切換，每當客戶端向伺服器端發出資源相關請求時，勢必會轉換伺服器的資源目前狀態(如URI->明確清單JSON)，來讓伺服器傳遞資訊給客戶端：從狀態A轉換至轉換B
2. 在這裡為了統一將請求轉換以資源為中心的請求，客戶端所發出的請求得必須透過現有且較明確的HTTP方法來發出，比如GET、POST、PUT、DELETE等HTTP方，而這種轉換會是在Resource Representation的基礎上進行轉換。 換言之，客戶端會發出HTTP動詞＋資源名稱 請求來讓目前在伺服器的資源進行狀態切換，以達到目的。

簡短來說：
- Transfer 是指事物在某方面從A轉換至B，Resource Representation State Transfer 則是指以特定時間點下之Resource Representation 對應的內容為單位來從A轉移至B
- 轉移方法會是HTTP方法


#### REpresentational 是指著Resource Representation 
- 簡化後的REpresentational State Transfer 的 REpresentational 是指著Resource Representation 這件事


### REST
整體概念是描述著如何對在網路上的任意具體化資源進行轉移或者獲取，在這裡會有兩大課題：
- 定義每個具體化資源在網路上的位置
- 定義如何對網路上的具體化資源進行轉換

Resource Representation State：
- 通常應用於HTTP/HTTPS協定的網頁服務
- 對應的具體化資源會是以PDF、HTML、CSS、JS、圖片檔、影片檔等能在網頁服務呈現的具體內容。

#### 定義每個具體化資源在網路上的位置
關於第三點所提到的兩大課題在網頁服務上所要做的實現：
- 定義每個具體化資源在網路上的位置：透過URI來標明具體化資源在網路上所在的位置，而URI會包含著URL和URN(以序號來區分每個具體化資源)、換言之，URI只會是在網路上的每一個具體化資源本身。

#### 定義如何對網路上的具體化資源進行轉換
- 如何對網路上的具體化資源進行切換、獲取：定義明確的HTTP/HTTPS協定標準方法來做狀態切換(如何獲取該狀態或者該具體化資源)，而標準方法會是GET、POST、PATCH、DELETE等方法。


### REST -> RESTful
若符合REST對於網頁服務的實作風格之軟體架構可以用RESTful來形容。


## 複習

#🧠 REST 全名為何？ ->->-> `REpresentational State Transfer`
<!--SR:!2024-08-23,374,230-->

#🧠 RESTful API中的REST 是什麼？ ->->-> `REST是一種 以資源為中心，用HTTP方法操作資源，並且最終目標為打造出滿足於HATEOAS之產品的網路軟體開發風格`
<!--SR:!2023-09-26,55,205-->
<!--SR:!2023-01-29,67,250-->


#🧠 RESTful API中的REST 是什麼？ ->->-> `REST是一種 以資源為中心，用HTTP方法操作資源，並且最終目標為打造出滿足於HATEOAS之產品的網路軟體開發風格`
<!--SR:!2023-09-26,55,205-->


#🧠 REST 網路軟體開發風格的背景是什麼？ ->->-> `當時軟體開發和網路發展皆分別以單機環境下進行以及制定/實現某些系統之間的通信協定，兩者很少有交集`
<!--SR:!2023-12-19,102,230-->

#🧠 REST 網路軟體開發風格是基於哪個協定來發展？ ->->-> `網路協定之一 - HTTP/HTTPS協議`
<!--SR:!2023-10-18,86,230-->

#🧠 REST 網路軟體開發風格的目的是什麼？ ->->-> `方便讓不同軟體或者程式模組在網路上能夠互相傳遞資訊`
<!--SR:!2023-09-19,181,230-->

#🧠 REST是一種 以資源為中心，用HTTP方法操作資源，並且最終目標為打造出滿足於HATEOAS之產品的網路軟體開發風格，請問何謂最終目標？說明清楚那HATEOAS之產品 ->->-> `當存取到特定資源X時，回應就會包含動態產生出來的一組與特定資源X相關連的API連結，而非以寫死的方式來表達能對特定資源做哪些進一步的操作`
<!--SR:!2023-10-14,219,249-->


#🧠 REST 網路軟體開發風格 完整的全名會是什麼 ->->-> `Resource Representation State Transfer`
<!--SR:!2024-03-23,313,250-->


#🧠 Resource Representation State Transfer / REST 中的Resource是什麼？ ->->-> `簡短來說，Resource會是指任意形式的實體；在網路上會以Resource所在的URI來表達Resource`
<!--SR:!2024-05-03,238,224-->


#🧠  Resource Representation State Transfer / REST 中的Representation是什麼？->->-> `Representation 本身以某種形式來呈現，而Resource Representation 是將Resource概念轉換成更為具體的形式呈現，形式會有HTML格式、JSON格式等等`
<!--SR:!2023-12-20,103,230-->


#🧠 Resource Representation State Transfer / REST 中的State是什麼？ ->->-> `簡短來說，State 是特定時間點下之特定事物所擁有的內容，Resource Representation State 則是指狀態會以特定時間點下的具體資源(所在)所擁有的內容`
<!--SR:!2023-12-22,105,230-->


#🧠 Resource Representation State Transfer / REST 中的Transfer是什麼？->->-> `- Transfer 是指事物在某方面從A轉換至B，Resource Representation State Transfer 則是指以特定時間點下之Resource Representation 對應的內容為單位來從A轉移至B - 轉移方法會是HTTP方法`
<!--SR:!2024-03-31,266,209-->

#🧠 REST整體概念是什麼？簡答一下 ->->-> `描述著如何對在網路上的任意具體化資源進行轉移或者獲取`
<!--SR:!2024-04-23,289,210-->

#🧠 REST整體概念是描述著如何對在網路上的任意具體化資源進行轉移或者獲取，其中在網路上有哪兩大課題？ ->->-> `- 定義每個具體化資源在網路上的位置 - 定義如何對網路上的具體化資源進行轉換`
<!--SR:!2023-12-18,101,230-->


#🧠 REST：如何定義每個具體化資源在網路上的位置 ->->-> `透過URI來標明具體化資源在網路上所在的位置`
<!--SR:!2023-10-20,88,230-->

#🧠 REST：如何定義如何對網路上的具體化資源進行轉換 ->->-> `定義明確的HTTP/HTTPS協定標準方法來做狀態切換(如何獲取該狀態或者該具體化資源)，而標準方法會是GET、POST、PATCH、DELETE等方法。`
<!--SR:!2023-10-15,217,249-->



---
Status: #🌱 
Tags:
[[Representational State Transfer]]
Links:
[[HATEOAS 是以超媒體來表示整個網頁應用程式目前所存取的狀態以及可用狀態會是什麼，其狀態會是指Resource Representation State ，意指為特定時間下的特定具體資源(所在)會有的內容]]
References:
[[@262588213843476HowExplainedREST]]
[[@FengSiXin80TiaoXiaoXia]]
[[@ihowerShiMoShiRESTGenRESTful2006]]
[[@FieldingDissertationCHAPTER]]
[[@ruanyifengLiJieRESTfulJiaGouRuanYiFengDeWangLuoRiZhi]]