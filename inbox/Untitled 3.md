## 描述
[[@reactReactComponentReact]]
> Typically, in React constructors are only used for two purposes:
>
> - Initializing local state by assigning an object to this.state.
> - Binding event handler methods to an instance.



重點：
- 在React中的class-based component中，constructor具有兩項主要用途：
	- 建立一個屬於元件的狀態並設定初始值
	- 設定事件處理


###

class-based component 定義事件處理函式方式：

1. 在render 函式定義：可行，但會重複定義函式而浪費多餘的成本

2. 在class中以作為其類別方法來新增事件處理函式：可行，通常開發會採用

### 
在class-based component 管理狀態-useState

1. 初始化並定義元件專屬的狀態

2. updated when needed


###
初始化並定義元件專屬的狀態：

1. 在class 中的constructor下，以this.state來定義，且只能使用state這個名稱，不能依據喜歡來取名為任何名稱來代表狀態，這是因為state本身是React.Component類別下的屬性

2. state 在class-based component是React.Component的唯一能夠定義狀態的屬性，本身沒辦法像functional component那樣，每個狀態都擁有各自的定義方式和各自的更新用函式，必須得以物件形式來包含元件下的所有狀態，而每個屬性會是每個狀態：

  - 無論這些屬性是否相關與否，都會以物件來包含

  

  

在functional component，state 可以是 任意值


## 複習


---
Status: #🌱 
Tags:
[[React]]
Links:
[[import { Component } from 'react'; 的用途為方便讓特定元件繼承React的通用元件類別和react element所會需要方法和屬性]]
[[JS class 建構式是每個類別的特殊方法，用來根據資訊來建立對應類別下物件並初始化，若沒設定的話，系統會預設設定指定的constructor給開發者來執行]]
References:
[[@reactReactComponentReact]]