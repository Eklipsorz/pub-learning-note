

## 描述

JSON 設計本身為了能夠讓JavaScript快速解析，而將自己的資料表示方法以JavaScript所現有的表示語法來進行延伸和使用-也就是以成為，只要JavaScript引擎使用現有與分解析規則來解析，便能快速解析


其中JSON有部分資料表示方法會和JavaScript 資料表示法有些不同，關於這點，只需要呼叫對應轉換方法就能解決


### JSON 能夠表示的資料型別有

1. 數字：最前面不能是0，比如：0123，但可以是負號，比如-123
2. 字串：以雙引號為主的字串表示法，一個字元在JSON形式來看會是以一個字元的字串來看待
[[@jsonJSON]] 所描述：
> A _string_ is a sequence of zero or more Unicode characters, wrapped in double quotes, using backslash escapes. A character is represented as a single character string. A string is very much like a C or Java string.
3. 布林值：true 或者 false
4. 陣列：如同JavaScript 是用一樣的陣列表示法，如[\1, \2, \3]
5. 物件：如同JavaScript 是用一樣的物件表示法，屬性和屬性值是用key-value pair，其中key只能是字串
6. 空值：null




### JSON 語法本身是JavaScript 資料表示語法中的子集合，這表示？

1. JSON紀錄資料的語法可以透過語法關係而很(輕易地轉換)直接在JavaScript 解析成相對應的資料表示方法，這使得它的資料解析在JS程式語言會非常快速。
2. 以支援類似於JavaScript資料表示法的程式語言，也能從中得到語法優勢而快速解析，如Java


### 補充：  XML

1. XML為一種標籤式語言，每個內容都會有兩個同種標籤來包含，且標籤們可構成巢狀結果，但需要有程式模組來負責解析其巢狀才能正常取出資料

2. JSON vs. XML :
- 同樣的內容需求描述，JSON 比起 XML 來得輕
- JSON可以直接被程式解析，XML得另外載入模組



## 複習
#🧠 JSON 是什麼樣的語言？ 和JavaScript是什麼關係？->->-> `JSON 設計本身為了能夠讓JavaScript快速解析，而將自己的資料表示方法以JavaScript所現有的表示語法來進行延伸和使用-也就是以成為，只要JavaScript引擎使用現有與分解析規則來解析，便能快速解析`
<!--SR:!2024-09-04,482,250-->


#🧠 JSON 語法本身是以成為JavaScript 資料表示語法中的子集合為目標，這表示？ (輕易在語言使用？其他語言表示？) ->->-> `1. JSON紀錄資料的語法可以透過語法關係而很(輕易地轉換)直接在JavaScript 解析成相對應的資料表示方法，這使得它的資料解析在JS程式語言會非常快速。 2. 以支援類似於JavaScript資料表示法的程式語言，也能從中得到語法優勢而快速解析，如Java`
<!--SR:!2024-09-16,490,250-->


#🧠 XML 是什麼樣的語言？需要什麼東西解析？ ->->-> `XML為一種標籤式語言，每個內容都會有兩個同種標籤來包含，且標籤們可構成巢狀結果，但需要有程式模組來負責解析其巢狀才能正常取出資料`
<!--SR:!2024-06-13,434,250-->

#🧠 JSON vs. XML  ->->-> `- 同樣的內容需求描述，JSON 比起 XML 來得輕 - JSON可以直接被程式解析，XML得另外載入模組`
<!--SR:!2024-07-17,453,250-->

#🧠 JSON 能夠表示undefined、NULL嗎 ->->-> `能表示NULL，但不能表示undefined`
<!--SR:!2023-10-08,16,166-->



#🧠 JSON 能夠表示的資料型別有啥？ ->->-> `1. 數字：最前面不能是0，比如：0123，但可以是負號，比如-123 2. 字串：以雙引號為主的字串表示法 3. 布林值：true 或者 false 4. 陣列：如同JavaScript 是用一樣的陣列表示法，如[\1, \2, \3] 5. 物件：如同JavaScript 是用一樣的物件表示法，屬性和屬性值是用key-value pair，其中key只能是字串 6. 空值：null`
<!--SR:!2023-09-26,70,150-->

#🧠 JSON 要能表示字串得用什麼符號 ->->-> `雙引號`
<!--SR:!2024-03-04,301,249-->


#🧠 JSON 能使用單引號來表示字串嗎？ ->->-> `不能`
<!--SR:!2023-11-01,40,169-->


#🧠 一個字元在JSON算是什麼？->->-> `擁有一個字元的字串`
<!--SR:!2024-10-08,501,250-->

#🧠 JSON能夠正常表示正負數嗎 ->->-> `能正常表示`
<!--SR:!2024-03-12,371,250-->

#🧠 JSON 要能表示物件得用什麼符號？key-value又是什麼樣的型別 ->->-> `key 一定是字串型別，value則是JSON能夠支援的`
<!--SR:!2023-11-17,300,250-->


---
Status: #🌱 
Tags:
[[JSON]] - [[Language]]
Links:
References:
[[@jsonJSON]]
[[@java3yJSONRuMenKanZheYiPianJiuGouLiaoZhiHu]]




