

## 描述

JSON 和 XML 主要差別在於：
- XML擁有著declaration 區塊和 主要內容區塊；JSON只有內容區塊
- XML以一個root元素來包含所有元素，比如[[@wikidataXML2022]]所提供的例子，在這裡是以小紙條這標籤作為root元素來包含剩下在內容區塊的所有元素，比如收件人、發件人、主題、具體內容
```
<?xml version="1.0"?>
<小纸条>
    <收件人>大元</收件人>
    <發件人>小張</發件人>
    <主題>問候</主題>
    <具體內容>早啊，飯吃了沒？ </具體內容>
</小纸条>
```
  JSON 是不具備root元素來包含所有元素，而是以JavaScript那樣描述物件的形式來定義其內容
```
{
	"小紙條":{
		"收件人":"大元",
		"發件人":"小張",
		"主題": "問候",
		"具體內容": "早啊，飯吃了沒?"
	}
}
```


### XML declaration

[[@XMLDeclaration]]
>  **XML declaration** contains details that prepare an XML processor to parse the XML document. It is optional, but when used, it must appear in the first line of the XML document.

[[@XMLProcessors]]
> The most fundamental XML processor reads an XML document and converts it into an internal representation for other programs or subroutines to use. This is called a _parser_, and it is an important component of every XML processing program.

重點：
- XML declaration 主要是告知XML processor 如何解析目前XML 文件
	- 該內容是可選填寫，並不是絕對需要(若沒填寫會以預設解析規則來進行)
	- 若是需要的話，會在XML文件的第一行
- XML processor 是一個解析器，會讀取XML文件內容，並將內部內容轉換成特定程式語言下的能夠解讀之形式

## 複習

#🧠 除了大小和容不容易解析以外，JSON 和 XML 還有沒有在內容上的主要差別在於？(提示有兩個，主要是內容上面的)->->-> `- XML擁有著declaration 區塊和 主要內容區塊；JSON只有內容區塊。 - XML以一個root元素來包含內容區塊下的所有元素，並且以起始標籤和結尾標籤夾雜，  JSON 是不具備root元素來包含所有元素，而是以JavaScript那樣描述物件的形式來定義其內容`
<!--SR:!2023-09-29,50,170-->

#🧠 除了大小和容不容易解析以外，JSON 和 XML 還有沒有在內容上的主要差別在於？(提示有兩個，主要是內容上面的，重複問題)->->-> `- XML擁有著declaration 區塊和 主要內容區塊；JSON只有內容區塊。 - XML以一個root元素來包含內容區塊下的所有元素，並且以起始標籤和結尾標籤夾雜，  JSON 是不具備root元素來包含所有元素，而是以JavaScript那樣描述物件的形式來定義其內容`
<!--SR:!2023-12-22,134,222-->


XML 的 declaration  是什麼？->->-> `告知XML processor 如何解析目前XML 文件`
<!--SR:!2026-01-02,311,241-->

#🧠 XML declaration 主要是告知XML processor 如何解析目前XML 文件，其中的XML processor會是什麼？ ->->-> `是一個解析器，會讀取XML文件內容，並將內部內容轉換成特定程式語言下的能夠解讀之形式`
<!--SR:!2024-02-04,178,241-->



---
Status: #🌱 
Tags:
[[JSON]] - [[XML]]
Links:
[[JSON 語法本身以成為JavaScript 資料表示語法中的子集合為目標而設計的資料表示法]]
References:
[[@wikidataXML2022]]
[[@XMLDeclaration]]
[[@XMLProcessors]]