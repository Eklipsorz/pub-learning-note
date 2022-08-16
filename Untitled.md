


事件處理器 命名法則：field 是指 發生事件的元件、event是指事件名稱、Handler是指處理器

- field + event + Handler ，比如titleChangeHandler

- event + Handler ，比如clickHandler


由於React的事件綁定是由原生JS的事件綁定來實現的，所以可以直接調用原生JS的事件綁定會有的東西來在React上實現。  
- event 物件：存放事件發生資訊的物件，會於事件發生時就會產生
- event.target ：會以實際DOM節點來表示哪個節點發生該事件
- event.target.value：會以該節點物件中的value屬性取值

  
```
const titleChangeHandler = (event) => {
	console.log(event.target.value);
};
```
