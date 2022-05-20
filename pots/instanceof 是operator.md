

## 描述
instanceof 是以與加減乘除性質相同的運算子(operator)，主要會處理兩個參數並負責檢查物件a是否為prototype b，形式如下：
```
// a 為 要檢測的物件
// b 為 比較用的prototype，在這裡會以prototype的建構式為主。
a instanceof b
```
- 若a 是屬於 prototype b，就會回傳true
- 若a 不屬於 prototype b，就會回傳false

## 總結
instanceof 主要是一種binary operator，主要檢測物件是否隸屬於特定的prototype，而參數會是分別為要檢測的物件和比對用的prototype(建構式)

## 複習

#🧠 instanceof 是什麼？->->-> `主要是一種binary operator，主要檢測物件是否隸屬於特定的prototype，而參數會是分別為要檢測的物件和比對用的prototype(建構式)`


---
Status: #🌱 
Tags:
[[JavaScript]]
Links:
References:
[[@mdnInstanceofJavaScriptMDN]]