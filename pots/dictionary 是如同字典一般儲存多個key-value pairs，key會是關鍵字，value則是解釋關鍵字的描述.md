## 描述
引用[[@isaaccomputerscienceDictionariesADT]]所描述的字典
> A dictionary is an abstract data type that defines an unordered collection of data as a set of key-value pairs. Each key, which must be unique, has an associated value. Typically, the keys in a dictionary must be simple types (such as integers or strings) while the values can be of any type.
> Standard dictionary operations include:
  
      retrieve a value associated with a particular key
      insert a new key-value pair into the collection
      remove a key-value pair from the collection
      update a value associated with a key 
	  
字典為一種資料模型上的概念，換言之，它只是描述字典就是描述特定形式的資料模型，沒指定特定方法來實現其概念，具體來說是如同字典一般紀錄一組由關鍵字以及對應關鍵字的解釋所組成的集合，而這個集合會是無序集合，集合中的每個元素皆為key-value pair。

特點：
 * 每個元素皆為key-value pair
 * 每一個key皆為獨特，且都能對應至特定value
 * 每一個key會是簡單型別(如字串、數字)，而value可以是任何型別

字典標準方法為：

 * 讀取：使用特定key來找到對應value
 * 新增：使用一個key-value pair來新增至字典
 * 移除：使用特定key來移除對應key-value pair
 * 更新：使用特定key來更新對應value

### 具體實現
通常會使用Hash Table 來實現字典


## 複習

#🧠 Data Structure ADT：dictionary是什麼樣的資料模型 ->->-> `字典為一種資料模型上的概念，換言之，它只是描述字典就是描述特定形式的資料模型，沒指定特定方法來實現其概念，具體來說是如同字典一般紀錄一組由關鍵字以及對應關鍵字的解釋所組成的集合，而這個集合會是無序集合，集合中的每個元素皆為key-value pair`
<!--SR:!2022-05-31,3,230-->

#🧠  Data Structure ADT：dictionary是概念嗎？還是具體實現？ ->->-> `字典為一種資料模型上的概念，實際上會是ADT，描述字典該有的特點和操作`
<!--SR:!2022-06-13,12,248-->

#🧠 Data Structure ADT：dictionary 會有哪些操作 ->->-> `讀取：使用特定key來找到對應value、新增：使用一個key-value pair來新增至字典、移除：使用特定key來移除對應key-value pair、 更新：使用特定key來更新對應value`
<!--SR:!2022-06-04,6,250-->


---
Status: #🌱 
Tags: 
[[Data Structure]]
Links:
[[Redis 的Value主要結構為 String 和 Hash]]
[[Abstract Data Type 是一種描述資料種類的模型，主要定義特定資料是什麼以及能對其資料做什麼樣的操作]]
References:
[[@isaaccomputerscienceDictionariesADT]]

