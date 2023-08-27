






## 描述



### 預設下，每個component 檔案所import的css並不會只限定於component才能使用



> even though we're importing it into the core skull list component is not scoped to that component. It would affect any element on the entire page

在1個component為1個檔案的情況下，預設每個component載入css (如下)，css 的作用域並不會只限定於component上，比如component1 要載入example.css，那麼該css的作用域並不會限定於component

`import './example.css';`

其css的作用域最後會是由webpack來決定：
1. 代表所有component的JS模組會合併成一個JS檔案並加載至HTML DOM文件A
2. 每個component所載入的CSS會分別合併成一個CSS檔案並加載至HTML DOM文件A


當瀏覽器解析HTML DOM文件A：
1. CSS-> CSSOM：會將合併後的CSS檔案轉換成CSSOM
2. HTML -> DOM：將HTML DOM文件A轉換成DOM Tree，過程中會執行合併後的JS來增加DOM或者移除DOM
3. 以HTML DOM文件所擁有的CSSOM 和 DOM來構建Rendering Tree、渲染(layout & paint)

在同個DOM的情況下，每個經由JS模組產生出來的DOM節點都會共享著同一個CSSOM的內容來渲染，換言之，每個component都會因為js模組和css模組都合併在HTML DOM文件而共享著每個component的CSS



### 預設下，css在webpack上的處理方式
在webpack處理上，多個CSS檔案會是合併成一個CSS檔案，接著自動加載至指定HTML DOM文件 或者手動加載至指定HTML DOM文件



### 證明：預設下，元件所載入的css會是以全域來進行載入

CourseGoalItem這元件實際載入的css是CourseGoalItem/CourseGoalItem.css並使用裡頭名為 ".goal-item" class selector
```
// CourseGoalItem/CourseGoalItem.css：
.goal-item {
  margin: 1rem 0;
  background: #8b005d;
  box-shadow: 0 2px 8px rgba(0, 0, 0, 0.26);
  color: white;
  padding: 1rem 2rem;
  cursor: pointer;
}
```

但實際上，CourseGoalItem/CourseGoalItem.css會與其他的CSS合併並加載，其中有個CourseInput/CourseInput.css 剛好也使用".goal-item" class selector來定義，這時會因為該css是後來且與另一個goal-item權重相同，所以以後來得到的樣式屬性為數。


CourseInput/CourseInput.css：
```
.goal-item {
  margin: 1rem 0;
  background: #000000;
  box-shadow: 0 2px 8px rgba(0, 0, 0, 0.26);
  color: white;
  padding: 1rem 2rem;
  cursor: pointer;
}
```



實際上另一個CourseInput.css卻因為跟entry 文件有關係而跟著和CourseGoalItem.css合併在一塊，這使得它有機會可以間接改變CourseGoalItem元件的CSS




具體是由webpack來確定css載入順序或者決定css樣式對應內容的先後順序
順序
 App.js -> CourseInput.css -> CourseGoalItem.css
## 複習

#🧠 React：預設下，每個對應component 的JS檔案所import 的css 會不會限定於該component才能存取？ ->->-> `不會`
<!--SR:!2025-01-25,529,250-->

#🧠 React：預設下，每個對應component 的JS檔案所import 的css 不會限定於該component才能存取，為什麼？ ->->-> `其css的作用域最後會是由webpack來決定，預設下，代表所有component的JS模組會合併成一個JS檔案並加載至HTML DOM文件A、每個component所載入的CSS會分別合併成一個CSS檔案並加載至HTML DOM文件A，當瀏覽器解析HTML文件A時，就會將CSS轉換成CSSOM、HTML轉換成DOM、將CSSOM和DOM合併成Rendering Tree、渲染(layout & paint)。在同個DOM的情況下，每個經由JS模組產生出來的DOM節點都會共享著同一個CSSOM的內容來渲染，換言之，每個component都會因為js模組和css模組都合併在HTML DOM文件而共享著每個component的CSS`
<!--SR:!2025-03-16,567,250-->

#🧠 React：預設下，每個對應component 的JS檔案所import 的css 不會限定於該component才能存取，為什麼？(簡答) ->->-> `其css的作用域最後會是由webpack來決定，預設下，所有component 和 所有css 會因爲處於同一個HTML DOM下而使得所有component都共享著所有CSS`
<!--SR:!2024-10-21,475,250-->


#🧠 React：預設下，假如有兩個css檔案分別為css1、css2，並同時定義名為.goal-item的selector，請問在css1被特定component載入並使用goal-item，其component會是使用css1的.goal-item嗎？ (記住webpack)->->-> `不一定，主要看webpack如何對CSS、JS、加載如何處理`
<!--SR:!2023-08-21,185,210-->

#🧠 React：預設下，假如有兩個css檔案分別為css1、css2，並同時定義名為.goal-item的selector，請問在css1被特定component載入並使用goal-item，其component會是使用css1的.goal-item嗎？ ->->-> `不一定，主要看webpack如何對CSS、JS、加載如何處理`
<!--SR:!2023-08-24,211,246-->


---
Status: #🌱 
Tags:
[[React]]- [[CSS]]
Links:
References:





