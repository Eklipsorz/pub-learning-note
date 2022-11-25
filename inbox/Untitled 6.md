
## 描述


### 在named export中可允許匯出的形式
1. 匯出Declaration：
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
export { name1, name2, …, nameN } from …;							
```

## 複習
#🧠 Question :: ->->-> ``

---
Status: 
Tags:
Links:
References: