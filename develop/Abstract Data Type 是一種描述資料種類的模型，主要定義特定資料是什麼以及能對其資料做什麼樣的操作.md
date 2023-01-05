
## 描述

引用[[@AbstractDataType2022]]所描述的ADT會是：
> In computer science, an **abstract data type** (**ADT**) is a mathematical model for data types. An abstract data type is defined by its behavior (semantics) from the point of view of a _user_, of the data, specifically in terms of possible values, possible operations on data of this type, and the behavior of these operations.

重點：
- Abstract Data Type 的 Abstract 是強調Data Type會是以概念來描述，而非以實際的實現來描述
- Abstract data type 是一種對於資料種類的描述模型
- 其模型主要描述特定資料，描述特定資料的具體形式是什麼以及能對它做些什麼樣的操作
- 操作會是以函式來表示，主要會是表達函式回傳什麼、處理什麼、輸入是什麼
### 好處

> **Features of ADT:**
> -   **Abstraction:** The user does not need to know the implementation of the data structure.
> -   **Better Conceptualization:** ADT gives us a better conceptualization of the real world.
> -   **Robust:** The program is robust and has the ability to catch errors.

主要帶來的好處是：
- 由於ADT等同於設計特定資料模型的草圖，可以以不呈現實現細節來設計程式如何實現
- 透過ADT可以更快發現錯誤，更專注目標

### 案例

引用[[@anujchauhanAbstractDataTypes]]的案例：
> -   **List ADT**
>  -   The data is generally stored in key sequence in a list which has a head structure consisting of _count_, _pointers_ and _address of compare function_ needed to compare the data in the list.
>  -   The data node contains the _pointer_ to a data structure and a _self-referential pointer_ which points to the next node in the list.
>  -   The **List ADT Functions** is given below:
>  -   get() – Return an element from the list at any given position.
>  -   insert() – Insert an element at any position of the list.
>  -   remove() – Remove the first occurrence of any element from a non-empty list.
>  -   removeAt() – Remove the element at a specified location from a non-empty list.
>  -   replace() – Replace an element at any position by another element.
>  -   size() – Return the number of elements in the list.
>  -   isEmpty() – Return true if the list is empty, otherwise return false.
>  -   isFull() – Return true if the list is full, otherwise return false.

在這裡個案例中以List 作為ADT來說明，會說明List是什麼樣的資料以及具有什麼樣的操作，其操作會是以能對List操作的函式

```
get()
insert()
remove()
removeAt()
replace()
size()
isEmplty()
isFull()
```

## 複習

#🧠 Abstract Data Type 的 Abstract 是指什麼？ ->->-> `是強調Data Type會是以概念來描述，而非以實際的實現來描述`


#🧠 Abstract Data Type 是什麼？ ->->-> `是一種對於資料種類的描述模型，其模型主要描述特定資料，描述特定資料的具體形式是什麼以及能對它做些什麼樣的操作，操作會是以函式來表示，主要會是表達函式回傳什麼、處理什麼、輸入是什麼`


#🧠 Abstract Data Type 帶來的好處是？->->-> `1. 由於ADT等同於設計特定資料模型的草圖，可以以不呈現實現細節來設計程式如何實現、2. 透過ADT可以更快發現錯誤，更專注目標`
<!--SR:!2023-01-10,138,250-->

#🧠 以下是描述List的ADT，請說明哪些是ADT所描述的資料描述和操作？![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1653732192/blog/algorithm/adt/listADT_nizmww.png) ->->-> ``
<!--SR:!2023-03-05,172,250-->

---
Status: #🌱 
Tags:
[[ADT]] - [[Data Structure]]
Links:
References:
[[@AbstractDataType2022]]
[[@anujchauhanAbstractDataTypes]]