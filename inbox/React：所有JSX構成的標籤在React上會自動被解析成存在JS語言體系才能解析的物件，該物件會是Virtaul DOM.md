		
## 描述

所有JSX構成的標籤在React上會自動被解析成存在JS語言體系才能解析的物件，該物件會是Virtaul DOM，比如：
- testvdom 指向的內容會被自動解析成JS語言下的Virtaul DOM物件。
```
const testvdom = <p>hi</p>
```
- Component 屬性值若是JSX構成的標籤，會自動解析成JS語言下的Virtaul DOM物件。
```
<Component attribute1={<p>hi</p>} />
```


## 複習

#🧠 所有JSX構成的標籤在React看來會是什麼？ ->->-> `JS語言體系才能解析的物件`
<!--SR:!2023-09-07,176,250-->

#🧠 所有JSX構成的標籤在React看來會是JS語言體系才能解析的物件，其物件又會是什麼？？ ->->-> `Virtaul DOM物件`
<!--SR:!2023-03-18,68,250-->


#🧠 React：Component 屬性值若是JSX構成的標籤會解析成什麼？->->-> `JS語言下的Virtaul DOM物件`
<!--SR:!2023-04-28,82,230-->

#🧠  React：testvdom 指向的內容會解析成什麼？const testvdom = \<p\>hi\<\/p\> ->->-> `JS語言下的Virtaul DOM物件`
<!--SR:!2023-09-05,175,250-->





---
Status: #🌱 
Tags:
[[React]]
Links:
References: