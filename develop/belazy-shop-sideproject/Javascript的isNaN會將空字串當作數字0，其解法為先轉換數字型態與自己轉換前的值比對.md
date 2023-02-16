
## 描述
引用[[@mdnIsNaNJavaScriptMDN]]所描述
> 從最早的 `isNaN` 函式版本規範始，其針對非數值之行為，不斷教人困惑至極。當 `isNaN` 函式的參數並非[數字](http://es5.github.com/#x8.5 "http://es5.github.com/#x8.5")型別時，此值會先強制轉換到數字。該值接著會測定此值是否為 [`NaN`](https://developer.mozilla.org/zh-TW/docs/Web/JavaScript/Reference/Global_Objects/NaN)。因此，當被強制轉換的非數字，給出了有效的非 NaN 值（經典案例為空的字串與布林原始值：它們在強制轉換時，會給予數字結果 0 或 1）時，會回傳不如預期的「false」值：以空的字串為例，它很明顯地「非數字」。這段教人糾結的點，乃出於「非數字」術語的「數字」一詞、由 IEEE-754 浮點值定義之事實而來。這個函式要解釋為「當這個值，被強制轉換為數值時，它還是 IEEE-754 的『非數字』值嗎？」的答案。

> 最新的 ECMAScript（ES2015）版本導入了 [`Number.isNaN()`](https://developer.mozilla.org/zh-TW/docs/Web/JavaScript/Reference/Global_Objects/Number/isNaN) 函式。儘管 `Number.isNaN` 的 `NaN` 依舊維持了數字上的意義、而不是簡單的「非數字」，`Number.isNaN(x)` 在偵測 `x` 為 `NaN` 與否時比較可靠。另外，如果在缺少 `Number.isNaN` 的情況下，通過表達式`(x != x)` 來檢測變量`x`是否是NaN會更加的可靠。

引用[[@avengerWhyDoesIsNaN2019]]所描述
> JavaScript interprets an empty string as a 0, which then fails the isNAN test. You can use parseInt on the string first which won't convert the empty string to 0. The result should then fail isNAN.

> You may find this surprising or maybe not, but here is some test code to show you the wackyness of the JavaScript engine.


重點：
- JavaScript isNaN會先做：
	- 轉換成數字型態
	- 比對轉換後的型別是否為數字，若是就回傳false；否則就回傳true
- JavaScript 會對原本判定為字串的值會誤判成數字，
	- 比如空字串會被視為數字，這是由於空字串轉換數字型態會是0
	- 這類型的問題是出自於 IEEE-754規範，並非實際isNaN實現上的錯誤，而是規範上的解釋

### 解法
> 一個 `isNaN` 的 polyfill 可以理解為（這個 polyfill 利用了 `NaN` 自身永不等於自身這一特性）：

```
static isNaN(value) {
	const number = Number(value)
	return number !== value
}
```

重點：
- 該解法是憑藉著 
	- **若value真是數字的話，經過Number重複轉換肯定也會是數字；否則會因不是數字而不會與轉換前的數值相同** 
	- **若value本身是NaN，會因為NaN不等於NaN而不產生例外**
- 那麼將比對值丟入Number進行轉換，再和原本轉換前的比對值比對的話，若假如比對值是數字，那麼勢必是一樣的；若比對值是非數字，那麼勢必是不一樣。
## 複習
#🧠 JavaScript 的 isNaN有什麼樣的特殊狀況(比如遇到空字串，也請說明整體問題點是什麼) ->->-> `可能會將原本判定為字串的值誤判成數字，比如空字串會被視為數字，這是由於空字串轉換數字型態會是0`
<!--SR:!2023-02-17,3,250-->


#🧠 JavaScript 的 isNaN 會將字串誤判數字是出於本身問題？->->-> `這類型的問題是出自於 IEEE-754規範，並非實際isNaN實現上的錯誤，而是規範上的解釋`
<!--SR:!2023-04-11,191,250-->

#🧠 由於JavaScript 的 isNaN 會將字串誤判數字，請試著撰寫能夠解決這樣問題的isNaN 函式->->-> `![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1654768947/blog/javascript/Number/isNaN-solution_mzj0ym.png)`
<!--SR:!2023-03-29,180,250-->

#🧠 由於JavaScript 的 isNaN 會將字串誤判數字，其解法會是如圖![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1654768947/blog/javascript/Number/isNaN-solution_mzj0ym.png)，請說明解法是怎麼樣的思路(提示 NaN、Number回傳) ->->-> `若value真是數字的話，經過Number重複轉換肯定也會是數字；否則會因不是數字而不會與轉換前的數值相同 以及 **若value本身是NaN，會因為NaN不等於NaN而不產生例外**`
<!--SR:!2024-03-04,382,250-->

#🧠 JavaScript 原生的isNaN會如何實現？ ->->-> `	- 轉換成數字型態 - 比對轉換後的型別是否為數字，若是就回傳false；否則就回傳true`
<!--SR:!2023-02-17,3,250-->


---
Status: #🌱 
Tags:
[[JavaScript]] - [[Side Project]]
Links:
References:
[[@avengerWhyDoesIsNaN2019]]
[[@mdnIsNaNJavaScriptMDN]]