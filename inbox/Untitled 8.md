## 描述

### Router 的 Route 預設遍歷方式

假若沒使用switch 元件的話，而採取預設遍歷方式：
- 其遍歷的觸發時間是：當目前綁定Router的頁面發生URL變動時
- 遍歷：
	- 會按照現有的Route由上往下找，其path matching的實現會是由Route元件來決定，可以是fuzzy matching 或者 exact matching 來比對變動後的URL和path是否一樣。
	- 當變動後的URL滿足當前Route所指定的path，就以Route包含的後裔節點來渲染，接著再往下找下一個Route來比對，直到沒Route可遍歷
	- 當變動後的URL不滿足當前Route所指定的path，就再往下找下一個Route來比對，直到沒Route可遍歷

#### 若多個Route被滿足的話

```

```


#### 案例

假如path2、path3是滿足現在切換後的URL1，那麼當URL切換成URL1時，就會往目前頁面對應綁定的Router Route定義來往下遍歷：首先是綁定path1的Route進行path比對，結果是不滿足，接著往綁定path2的Route進行path比對，結果是滿足的，並且以Component2 來渲染

接著滿足後就往下找綁定path3的Route來比對path

```
<Route path="path1">
	<Component1 />
</Route>

<Route path="path2">
	<Component2 />
</Route>


<Route path="path3">
	<Component3 />
</Route>

<Route path="path4">
	<Component4 />
</Route>
```



## 複習
#🧠 Question :: ->->-> ``

---
Status: 
Tags:
Links:
References: