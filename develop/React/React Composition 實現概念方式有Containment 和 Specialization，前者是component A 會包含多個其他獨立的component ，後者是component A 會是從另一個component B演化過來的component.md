

## 描述



[[React： composition 是利用has a關係來打造元件間的關係，而inheritance則是利用is a 關係來打造元件間的關係]]

[[@ithomeWantKnowReact]]
> 特化（Specialization）代表一個 component 是另一個通用 component 的特殊型態的狀況。
> **包含（Containment）** 即代表一個 component 是另一個 component 的外框狀況。



由於composition 定義為 **類別A會擁有某個類別B的實例，進而使類別A的實例會是與類別B的實例組合在一起的組合物**

在React 的 composition 具體實現方法：
- Containment：概念為 component A 會包含多個其他獨立的component 
- Specialization：概念為 component A 會是從另一個component B演化過來的component


### Containment 實現概念
Containment 概念為 component A 會包含多個其他獨立的component ，具體會是：
-  **建立一個component A來包含其他獨立的component B** 

實現手段為：
- props 和 component 之間的關係是：props會被React視作為component 物件的屬性
- 利用 props.children 來表示其對應標籤所包含的內容
- 被包含的內容會是多個獨立的Component


#### 案例
在這裡會以Card元件來以標籤包含每一筆消費紀錄(ExpenseItem)的資訊：日期、描述


Card.js
```
1.  function Card(props) {
2.      return (
3.          <div className='card'>{props.children}</div>
4.      )
5.  }
```


ExpenseItem.js
```
1.  import Card from './Card'

3.  function ExpenseItem(props) {
4.     return (
5.        <Card className='expense-item'>
6.            <ExpenseDate date={props.date} />
7.            <div className='expense-item__description'>
8.              <h2>{props.title}</h2>
9.              <div className='expense-item__price'>{props.amount}</div>
10.            </div>
11.        </Card>
12.     )
13.  }
```
  
並且在Card Component 上使用props.children 來找到Card 所包含的多個元件

```
6.            <ExpenseDate date={props.date} />
7.            <div className='expense-item__description'>
8.              <h2>{props.title}</h2>
9.              <div className='expense-item__price'>{props.amount}</div>
10.            </div>
```

並放到另一個div 元件上
```
<div className='card'>
     <ExpenseDate date={props.date} />
     <div className='expense-item__description'>
	     <h2>{props.title}</h2>
	     <div className='expense-item__price'>{props.amount}</div>
     </div>
</div>
```

從React角度來看，會是由Card元件來擁有日期元件、描述元件，並構成混雜其元件的組合物。


### Specialization 實現概念
 Specialization 概念為 component A 會是從另一個component B演化過來的component，在這裡會以一個獨立的component 實例B來作為基礎來開發component A，具體會是：
	- **建立一個component A，其component A會透過載入來擁有一個獨立的component 實例B並以此作為基礎來開發**
	- 開發過程不會破壞component 實例B結構，但會將component 實例B當作函式呼叫，並夾雜對應資料來當參數來得到 **內容不一樣的的component 實例B**


實現手段為：
- props 和 component 之間的關係是：props會被React視作為component 物件的屬性
- 載入特定元件B來讓目前元件A擁有元件B
- 元件B 有提供props 來讓元件A以特定資訊來得到不同內容的元件B

#### 案例

在這裡會有Dialog.js 和 WelcomeDialog.js ，前者是代表通用Dialog元件，後者是經由通用Dialog元件而改造的元件。

Dialog.js：
```
function Dialog(props) {
  return (
    <FancyBorder color="blue">
      <h1 className="Dialog-title">
        {props.title}      </h1>
      <p className="Dialog-message">
        {props.message}      </p>
    </FancyBorder>
  );
}
```

WelcomeDialog.js ：
```
function WelcomeDialog() {
	return (
	    <Dialog title="Welcome" message="Thank you for visiting our spacecraft!" />  
	);
}
```


然而，在這裡並不是選擇繼承，而是打造一個WelcomDialog 這元件擁有通用Dialog 元件，並將特定資訊以attribute輸入給對應Dialog元件的函式來產生不同內容的Dialog元件，接著在不修改擁有的Dialog元件下，添加內容來開發WelcomDialog



### 兩者皆有類別A會擁有某個類別B的實例的概念
兩者皆有 **類別A會擁有某個類別B的實例** 的概念：
- Containment： component A 包含其他獨立的component B，換言之就是component A擁有多個獨立的component B 來構成component A本身
- Specialization：在不修改Component B的結構下，以Component B為基礎來開發成Component A，換言之就是Component A先擁有Component B，並在不修改其結構下來開發。


### 細節

#### HTML 元件的attributes vs. 自製元件的attributes

1. HTML 元件特有的attribute (包含用className來替代class) 只能用在HTML原生元件上才能發揮出對應的效果。
2. 若自製元件套用其屬性(attributes) 會直接被當成該元件的函式參數props這物件的屬性來看待

#### wrapper componet 

> wrapper component => component to wrap something

重點：
- 一個會包裹其他元件(component)的component
- 在使用Containment 技術下，包裹住其他元件的元件會是叫做wrapper component

#### props.children 會是什麼？
> props.children :
> 1.  children is a reserved name (user don't set a children prop on this card)
> 2.  the value is always be the content


重點：
- props 會是每個元件對應函式的參數props
- 其props.children的children是保留字，會直接指向該元件所包含的內容
- 內容會是多個獨立元件所構成的結構體

#### Containment  命名緣由
 [[@collinsContainmentDefinitionMeaning]]
> a containing or being contained

重點：
- containment 是指被包含和包含的行為、過程

#### Specialization 命名緣由

> a making or becoming specialized

[[@collinsSpecializeDefinitionMeaning]]
> to make special, specific, or particular; specify
> 
> to direct toward or concentrate on a specific end
> 
> (Biology) to adapt (parts or organs) to a special condition, use, or requirement

重點：
- specialize 是指朝著特定目標前進，在這裡會是以生物學來說明，生物 **朝著適應環境來演化身體結構**
- specialization 則是指 **朝著適應環境來演化身體結構** 的過程、行為


## 複習

#🧠 Specialization 命名緣由->->-> `specialize 是指朝著特定目標前進，在這裡會是以生物學來說明，生物 **朝著適應環境來演化身體結構**，specialization 則是指 **朝著適應環境來演化身體結構** 的過程、行為`

#🧠 Containment  命名緣由 ->->-> `containment 是指被包含和包含的行為、過程`

#🧠 在React 的 composition 具體實現方法 有哪兩種？->->-> `Containment、Specialization`

#🧠 在React 的 composition 具體實現方法有Containment、Specialization，其中Containment 實現概念是什麼？ ->->-> `component A 會包含多個其他獨立的component`

#🧠 在React 的 composition ：Containment 的 概念為component A 會包含多個其他獨立的component，具體會是？ ->->-> `**建立一個component A來包含其他獨立的component B** `

#🧠 在React 的 composition：comtainment 概念為component A 會包含多個其他獨立的component，實現手段會有什麼？ ->->-> `props 和 component 之間的關係是：props會被React視作為component 物件的屬性、利用 props.children 來表示其對應標籤所包含的內容、被包含的內容會是多個獨立的Component`


#🧠 在React 的 composition 具體實現方法有Containment、Specialization，其中Specialization 實現概念是什麼？ ->->-> `Specialization 概念為 component A 會是從另一個component B演化過來的component，在這裡會以一個獨立的component 實例B來作為基礎來開發component A`

#🧠 在React 的 composition ： Specialization 概念為 component A 會是從另一個component B演化過來的component，在這裡會以一個獨立的component 實例B來作為基礎來開發component A，具體會是？結構？ ->->-> `- **建立一個component A，其component A會透過載入來擁有一個獨立的component 實例B並以此作為基礎來開發** - 開發過程不會破壞component 實例B結構，但會將component 實例B當作函式呼叫，並夾雜對應資料來當參數來得到 **內容不一樣的的component 實例B**`


#🧠 React Specialization：當要載入來擁有component B 來當作基礎開發另一個component A，會修改到component B的結構嗎？->->-> `並不會`

#🧠 在React 的 compositio：Specialization的 實現手段會有什麼？ (關係、載入、資訊)->->-> `- props 和 component 之間的關係是：props會被React視作為component 物件的屬性 - 載入特定元件B來讓目前元件A擁有元件B - 元件B 有提供props 來讓元件A以特定資訊來得到不同內容的元件B`



#🧠 React Composition：Containment和Specialization這兩個為何會有類別A會擁有某個類別B的實例 的概念？ ->->-> `- Containment： component A 包含其他獨立的component B，換言之就是component A擁有多個獨立的component B 來構成component A本身 - Specialization：在不修改Component B的結構下，以Component B為基礎來開發成Component A，換言之就是Component A先擁有Component B，並在不修改其結構下來開發。`

#🧠 wrapper component 是什麼？ ->->-> `- 一個會包裹其他元件(component)的component
`


#🧠 React： props.children 會是什麼 ->->-> `- props 會是每個元件對應函式的參數props - 其props.children的children是保留字，會直接指向該元件所包含的內容 -  內容會是多個獨立元件所構成的結構體`

#🧠  React：請說明它使用哪個composition的技術，以及做了什麼？![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1660405942/blog/react/composition/containment-card_fajbai.png) ![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1660405942/blog/react/composition/containment-expense-item_lcxg8f.png)->->-> `使用了containment，在這裡會以Card元件來以標籤包含每一筆消費紀錄(ExpenseItem)的資訊：日期、描述、並且在Card Component 上使用props.children 來找到Card 所包含的多個元件，並放到另一個div 元件上，從React角度來看，會是由Card元件來擁有日期元件、描述元件，並構成混雜其元件的組合物。`

#🧠 React：請說明使用composition的哪個技術，以及做了什麼？![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1660405942/blog/react/composition/specialization-dialog_rx2lo0.png) ![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1660405942/blog/react/composition/specialization-welcome-dialog_q2cdwu.png)->->-> `使用了specialization，在這裡會有Dialog.js 和 WelcomeDialog.js ，前者是代表通用Dialog元件，後者是經由通用Dialog元件而改造的元件。然而，在這裡並不是選擇繼承，而是打造一個WelcomDialog 這元件擁有通用Dialog 元件，並將特定資訊以attribute輸入給對應Dialog元件的函式來產生不同內容的Dialog元件，接著在不修改擁有的Dialog元件下，添加內容來開發WelcomDialog`


---
Status: #🌱 
Tags:
[[React]] - [[JavaScript]]
Links:
[[React：props概念可以延伸至Parent Element、其Parent Element之下的Child Element]]
References:
[[@ithomeWantKnowReact]]
[[@collinsSpecializeDefinitionMeaning]]
[[@collinsContainmentDefinitionMeaning]]