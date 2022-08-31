在1個component為1個檔案的情況下，預設每個component載入css (如下)，css 的作用域並不會只限定於component上，而是以virtual dom root為中心的virtual dom來載入css，並且以對應實際root dom節點來建立對應CSSOM

`import 'xxxx.css';`

  

even though we're importing it into the core skull list component is not scoped to that component

it would affect any element on the entire page

比如component1 要載入example.css，那麼該css的作用域並不會限定於component

`import './example.css';`


### 預設下，css在webpack上的處理方式
在webpack處理上，多個CSS檔案會是合併成一個CSS檔案，合併方式為：
- 若從CSS檔案找到結果CSS檔案所不存在的樣式，就直接加入
- 若從CSS檔案找到結果CSS檔案存在的樣式，就看屬性是否存在，若不存在就加入，若存在的話，就覆蓋。

### 證明：預設下，元件所載入的css會是以全域來進行載入

實際CourseGoalItem這元件載入的css是CourseGoalItem/CourseGoalItem.css，但
實際上另一個CourseInput.css卻改變了CourseGoalItem的樣式屬性

CourseGoalItem/CourseGoalItem.css：
```
.goal-item {
  margin: 1rem 0;
  background: #8b005d;
  box-shadow: 0 2px 8px rgba(0, 0, 0, 0.26);
  color: white;
  padding: 1rem 2rem;
  cursor: pointer;
}
```


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


具體是由webpack來確定css載入順序或者決定css樣式對應內容的先後順序
順序
 App.js -> CourseInput.css -> CourseGoalItem.css