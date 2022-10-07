## 描述



### 建立React Element 方法：
1. class-based component 
2. functional component



#### class-based component 

> class-based component：
> components can also be defined as JS classes where a render() method defines the to-be-rendered output


重點：
- class-based component 是以JS class語法建立而成的元件類別，最主要會有render方法並且繼承react.Component 這個基本類別所擁有的方法和屬性
- 其render 方法會



建立元件的方式，主要有兩種，兩種擇其一
class-based component (old approach)
functional component (default & most modern approach)


> functional component：
> components are regular javascript functions which return renderable result (typically JSX)

  




> Error Boundaries require class-based component to be built






> class-based component
> traditionally (React  < 16.8), you had to use class-based components to manage "state"

React 16.8 之前都使用class-based component 來建立元件
  
> 16.8 => react hooks & functional components
> hooks (useState and useEffect and so on.) =>

React 16.8 之後就改採用hooks 和 functional components 概念

> - these are functions for functional components, which bring features to functional components, which previously were reserved for class-based components

hooks 是：
- 使用在functional component
- 封裝著過去實現在class-based component的功能程式模組的語法糖，形式會是以hook function來包裝

  

> - class-based components can't use react hooks

class-based component 無法使用react hooks
  




## 複習


---
Status: #🌱 
Tags:
[[React]]
Links:
[[JS class 建構式是每個類別的特殊方法，用來根據資訊來建立對應類別下物件並初始化，若沒設定的話，系統會預設設定指定的constructor給開發者來執行]]
References: