
## 描述

[[@wikidataThisComputerProgramming2022]] 所描述：
> **this**, **self**, and **Me** are keywords used in some computer programming languages to refer to the object, class, or other entity of which the currently running code is a part. The entity referred to by these keywords thus depends on the execution context (such as which object is having its method called).


> In many object-oriented programming languages, this (also called self or Me) is a variable that is used in instance methods to refer to the object on which they are working.

重點：
- this、self、me 等關鍵字在電腦語言中是指目前執行的代碼屬於哪一個實體物件，換言之，是哪個實體物件呼叫目前執行的代碼來執行
- this、self、me 在物件導向語言裡，是指呼叫特定方法執行的呼叫者，而呼叫者本身就是一個實體物件，所以可以間接獲取其他屬性來處理，通常會應用在每個類別下的實體物件，並將this變數放在類別下的特定方法，當呼叫特定方法A時，會直接找到是哪個實體來呼叫特定方法A，並依據該實體的資訊來呼叫特定方法A

## 複習
#🧠 this 變數在電腦語言是指什麼？ ->->-> `this、self、me 等關鍵字在電腦語言中是指目前執行的代碼屬於哪一個實體物件，換言之，是哪個實體物件呼叫目前執行的代碼來執行`

#🧠 this 變數在物件導向語言是指？ 應用在哪?( 提示：this 變數會放在哪？從this獲取什麼)->->-> `呼叫特定方法執行的呼叫者，而呼叫者本身就是一個實體物件，所以可以間接獲取其他屬性來處理，通常會應用在每個類別下的實體物件，並將this變數放在類別下的特定方法，當呼叫特定方法A時，會直接找到是哪個實體來呼叫特定方法A，並依據該實體的資訊來呼叫特定方法A `

---
Status: #🌱 
Tags:
[[JavaScript]]
Links:
References:
[[@wikidataThisComputerProgramming2022]]