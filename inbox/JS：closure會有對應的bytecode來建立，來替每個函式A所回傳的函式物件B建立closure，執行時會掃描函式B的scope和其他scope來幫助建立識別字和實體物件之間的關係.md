## 描述


### closure 有對應的bytecode 建立指令？？

編譯時：
- 會產生負責建立Closure的對應bytecode
- 替誰編譯：每個函式A所回傳的函式物件B建立closure
- 用途：好讓函式物件擁有closure結構，能透過closure來對應到其他scope下的實體物件。

執行到該bytecode時：
- 時機點：開始回傳該函式物件至物件傳遞至需求方之間的時間
- 該bytecode會替函式物件B進行掃描來確定物件B所用的識別字都能找得到對應的實體物件
- 對應順序：會優先從物件B內的scope來找，接著再來利用scope chain來往上找對應的實體物件。

[[@ithomeITBangBangMangYiQiBangMangJieJueNanTi]]
![](https://i.imgur.com/kQHviiR.png)




## 複習


#🧠 JS：closure 有對應的bytecode 建立指令？？ ->->-> `有`
<!--SR:!2022-10-26,28,250-->

#🧠 JS：編譯到執行之間如何讓每個函式A所回傳的函式物件B得到closure？ ->->-> `首先先在編譯時期產生負責建立Closure的對應bytecode，等到開始回傳該函式物件B的時候，就執行bytecode來對函式物件B進行掃描來確定物件B所用的識別字都能找得到對應的實體物件`
<!--SR:!2022-10-16,20,250-->


#🧠 JS：closure是給哪個函式來擁有？ ->->-> `讓函式A所回傳的函式物件B所擁有`
<!--SR:!2022-10-22,25,250-->

#🧠 JS：讓函式A所回傳的函式物件B擁有closure結構是為了什麼用途？(對應其他scope)->->-> `好讓函式物件擁有closure結構，能透過closure來對應到其他scope下的實體物件`


#🧠 JS：讓函式A所回傳的函式物件B擁有closure結構是為了什麼用途？->->-> `好讓函式物件擁有closure結構，能透過closure來對應到其他scope下的實體物件`


#🧠 JS：當替函式物件B執行到建立對應closure的bytecode時，是如何執行？ ->->-> `該bytecode會替函式物件B進行掃描來確定物件B所用的識別字都能找得到對應的實體物件，會優先從物件B內的scope來找，接著再來利用scope chain來往上找對應的實體物件。`
<!--SR:!2022-10-15,19,250-->


#🧠 JS：什麼時候會執行建立closure的bytecode?  ->->-> `開始回傳該函式物件至物件傳遞至需求方之間的時間`
<!--SR:!2022-10-23,26,250-->

---
Status: #🌱 
Tags:
[[JavaScript]]
Links:
[[Closure 是一種封閉空間的結構體，該結構體會定義著特定scopeA下的識別字對應著特定scopeB下的實體物件，scopeA和scopeB 可能會是一樣或者不一樣]]
References:
[[@ithomeITBangBangMangYiQiBangMangJieJueNanTi]]