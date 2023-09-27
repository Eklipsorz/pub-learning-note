
## 描述



### 在named export中可允許匯出的形式
1. 以單一宣告語句來匯出：
- 匯出單個declaration
```
// export variable declaration
export let/const variable = value

// export function declaration 
export function fn(...) {...}
```
- 匯出多個declaration：若出現多個named export的話，會將每個export對應的識別字當作結果物件的屬性，對應值會是屬性值，比如以下結果會是如下結果物件
```
export let variable1 = xxxx;
export function fn(...) {...};

// result object
{
	variable1: xxxx;
	fn: function() {}
}
```

2. 以物件形式來匯出：其中的name為要匯出的識別名稱，在這裡會構成一個物件的屬性來匯出
- 匯出單個物件
```
export { name1, name2, …, nameN };						
```
- 匯出多個物件：若出現多個物件來匯出，在這裡會合併成一個結果物件
```
export { a1, a2, …, aN };
export { b1, b2, …, bN };

// result object
{
	a1,
	a2,
	.
	.
	aN,
	b1,
	b2,
	.
	.
	bN
}
```

## 複習

#🧠 ES module：在named export中可允許匯出的形式，有哪兩種形式？ ->->-> `以單一宣告語句來匯出、以物件形式來匯出`
<!--SR:!2023-09-30,190,250-->

#🧠 ES module：在named export中可允許匯出的形式，主要有以單一宣告語句來匯出、以物件形式來匯出這兩種形式，請問這兩種最後會如何將輸出內容以何種形式儲存？資料如何綁定？->->-> `皆會以夾雜結果資訊的物件來儲存，屬性綁定特定資料`
<!--SR:!2024-02-27,152,230-->

#🧠 ES module：在named export中可允許匯出的形式，有哪兩種形式？其中以單一宣告語句來匯出會是具體是什麼形式？舉一個變數和函式的語法來說明 ->->-> `export let/const variable = value、export function fn(...) {...}`
<!--SR:!2024-07-18,360,250-->

#🧠 ES module：在named export中可允許匯出的形式，其中以單一宣告語句來匯出的話，那麼`export let/const variable = value` 最後會是以什麼形式來匯出？ ->->-> `會替結果物件新增一個名為variable這屬性名稱，其對應值為value`
<!--SR:!2024-07-16,358,250-->

#🧠 ES module：在named export中可允許匯出的形式，其中以單一宣告語句來匯出的話，那麼`export function fn(...) {...}` 最後會是以什麼形式來匯出？ ->->-> `會替結果物件新增一個名為fn這屬性名稱，其對應值為對應函式內容`
<!--SR:!2023-11-20,77,210-->

#🧠 ES module：在named export中可允許匯出的形式，其中以單一宣告語句來匯出的話，那麼`export let variable1 = xxxx; export function fn(...) {...};` 最後會是以什麼形式來匯出？ ->->-> `會替結果物件新增兩個屬性分別為variable和fn，其對應值為會是value和函式內容`
<!--SR:!2024-07-08,350,250-->


#🧠 ES module：在named export中可允許匯出的形式，其中以物件形式來匯出的話，那麼`export { name1, name2, …, nameN };	` 最後會是以什麼形式來匯出？ ->->-> `結果物件的屬性分別有name1至nameN，對應值則為這些識別字對應的記憶體區塊內容`
<!--SR:!2023-12-23,92,230-->

#🧠 ES module：在named export中可允許匯出的形式，若形式為`export { name1, name2, …, nameN };	`，那麼會是什麼形式來export？->->-> `以物件形式來匯出`
<!--SR:!2024-07-01,343,250-->

#🧠 ES module：在named export中可允許匯出的形式，若形式為`export let variable1 = xxxx; export function fn(...) {...};`，那麼會是什麼形式來export？->->-> `以單一宣告語句來匯出`
<!--SR:!2023-10-28,190,230-->


#🧠 ES module：在named export中可允許匯出的形式，其中以物件形式來匯出的話，那麼`export { a1, a2, …, aN };export { b1, b2, …, bN };` 最後會是以什麼形式來匯出？->->-> `一個夾雜著a1至aN屬性和b1和bN屬性的結果物件來匯出`
<!--SR:!2024-07-17,359,250-->

#🧠 ES module：在named export中可允許匯出的形式，其中以物件形式來匯出的話，那麼出現多個export語句，且每個語句都是含著物件來匯出，請問最後會是以什麼形式來匯出 ->->-> `會將每個export語句的物件合併一個結果物件，並以結果物件來匯出`
<!--SR:!2023-11-27,84,230-->


#🧠 ES module：在named export中可允許匯出的形式，其中以單一宣告語句來匯出的話，那麼出現多個export語句，且每個語句都是含著單一宣告語句來匯出，請問最後會是以什麼形式來匯出 ->->-> `會將每個單一宣告語句對應的識別字作為結果物件的屬性來合併，最後合併成一個結果物件來匯出`
<!--SR:!2023-11-26,83,230-->


---
Status: #🌱 
Tags:
[[JavaScript]]
Links:
[[ES module：exports 有兩種方式，一種為named export來強制將輸入內容存放至空物件並強制引用方得按照識別字來取出，而default export專門定義若沒用named形式來引入所預設會輸出的模組內容]]
References: