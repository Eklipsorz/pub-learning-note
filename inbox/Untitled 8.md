## 描述


ES module 若要引入named export的內容，可以替對應的識別字取一個別名，如：
	- variable1 取名成name1
	- variable2 取名成name2
```
export { variable1 as name1, variable2 as name2, /* …, */ nameN };
```
使用上就可以以別名形式來用。

## 複習


---
Status: #🌱 
Tags:
[[React]]
Links:
References: