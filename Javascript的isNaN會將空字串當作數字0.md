
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
	- 比對轉換後的形式是否為數字，若是就回傳false；否則就回傳true
- JavaScript 會對原本判定為字串的值會誤判成數字，
	- 比如空字串會被視為數字，這是由於空字串轉換數字型態會是0
	- 這類型的問題是出自於 IEEE-754規範，並非實際isNaN實現上的錯誤，而是規範上的解釋

### 解法

```
let isNaN = function(value) {
    var n = Number(value);
    return n !== n;
};
```




## 複習
#🧠 Question :: ->->-> ``

---
Status: #🌱 
Tags:
Links:
References:
[[@avengerWhyDoesIsNaN2019]]
[[@mdnIsNaNJavaScriptMDN]]