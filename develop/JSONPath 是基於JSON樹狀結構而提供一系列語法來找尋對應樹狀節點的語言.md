## 描述

> JSONPath expressions always refer to a JSON structure in the same way as XPath expression are used in combination with an XML document. Since a JSON structure is usually anonymous and doesn't necessarily have a "root member object" JSONPath assumes the abstract name `$` assigned to the outer level object.

重點：
- JSONPath 如XPath 一樣，也是一種Expression Language
- JSONPath 受到XPath啟發，也是基於JSON結構上也可以如同樹狀結構而提供一系列語法能夠對應特定樹狀節點
- 不過由於JSON 本身並沒有declaration 來定義其文件內容以及沒有主要的root節點，所以在JSONPath上的root節點會是以整個JSON object 作為代表，並以**$** 來表示
[[JSON 和 XML 差別在於XML擁有declaration區塊以及用root元素包含所有元素]]
## 複習

#🧠 JSONPath 是什麼樣的語言？ ->->-> `是一種Expression Language，受到XPath啟發，也是基於JSON結構上也可以如同樹狀結構而提供一系列語法能夠對應特定樹狀節點`
<!--SR:!2022-06-12,11,250-->

#🧠 JSONPath 的 root 節點會是什麼？ 為什麼？->->-> `由於JSON 本身並沒有declaration 來定義其文件內容以及沒有主要的root節點，所以在JSONPath上的root節點會是以整個JSON object 作為代表，並以**$** 來表示`
<!--SR:!2022-06-12,11,250-->


---
Status: #🌱 
Tags:
[[JSON]] - [[Expression Language]]
Links:
[[Expression Language 是建立電腦可解析(解釋)成特定資訊的表示語法來從大量資訊找到特定資訊內容]]
[[JSON 和 XML 差別在於XML擁有declaration區塊以及用root元素包含所有元素]]
References:
[[@stefangossnerJSONPathXPathJSON]]