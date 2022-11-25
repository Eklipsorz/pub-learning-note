
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

1. 以物件形式來匯出：其中的name為要匯出的識別名稱，在這裡會構成一個物件的屬性來匯出
```
export { name1, name2, …, nameN };						
```
											
## 複習

#🧠 ES module：在named export中可允許匯出的形式，有哪兩種形式？ ->->-> `以單一宣告語句來匯出、以物件形式來匯出`

#🧠 ES module：在named export中可允許匯出的形式，主要有以單一宣告語句來匯出、以物件形式來匯出這兩種形式，請問這兩種最後會如何將輸出內容以何種形式儲存？資料如何綁定？->->-> `皆會以夾雜結果資訊的物件來儲存，屬性綁定特定資料`

#🧠 ES module：在named export中可允許匯出的形式，有哪兩種形式？其中以單一宣告語句來匯出會是具體是什麼形式？舉一個變數和函式的語法來說明 ->->-> `export let/const variable = value、export function fn(...) {...}`

#🧠 ES module：在named export中可允許匯出的形式，其中以單一宣告語句來匯出的話，那麼`` ->->-> ``

---
Status: 
Tags:
Links:
References: