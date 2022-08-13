

## 描述



[[React： composition 是利用has a關係來打造元件間的關係，而inheritance則是利用is a 關係來打造元件間的關係]]

[[@ithomeWantKnowReact]]
> 特化（Specialization）代表一個 component 是另一個通用 component 的特殊型態的狀況。
> **包含（Containment）** 即代表一個 component 是另一個 component 的外框狀況。



由於composition 定義為 **類別A會擁有某個類別B的實例，進而使類別A的實例會是與類別B的實例組合在一起的組合物**

在React 的 composition 具體實現方法：
- Containment：代表著 component A 會包含多個其他獨立的component
- Specialization：代表著 component A 會是從另一個component B演化過來的狀況


### Containment 實現概念
**建立一個component A來包含其他獨立的component B** 



### Specialization 實現概念
 Specialization 是 代表著 component A 會是從另一個component B演化過來的狀況，在這裡會以一個獨立的component 實例B來作為基礎來開發component A，具體會是：
	- **建立一個component A，其component A會載入一個獨立的component 實例B並以此作為基礎來開發**




兩者皆有 **類別A會擁有某個類別B的實例** 的概念：
- Containment： component A 包含其他獨立的component B，換言之就是component A擁有多個獨立的component B
- Specialization：component A 包含

###


generally, this approach of building a user interface  from smaller building blocks is called composition  
  
composition noun

the way that people or things are arranged in a painting or photograph



props.children :
- children is a reserved name (user don't set a children prop on this card)
- the value is always be the content

  

example:

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
  

Card.js
```
1.  function Card(props) {
2.      return (
3.          <div className='card'>{props.children}</div>
4.      )
5.  }
```


### 細節

HTML 元件特有的attribute (包含用className來替代class) 只能用在HTML原生元件上

若自製元件套用其屬性會直接被當成props這物件的屬性看待

wrapper component => component to wrap something

good point:

1. able to extract some code duplication from inside our CSS files into this separate wrapper component

whenever you combine components, you are using composition......

important part of composition is this props children feature which allows you to also create wrapper components which is a special type of component, you could say, which you also sometimes need




### Containment  命名緣由
 [[@collinsContainmentDefinitionMeaning]]
> a containing or being contained

重點：
- containment 是指被包含和包含的行為、過程

### Specialization 命名緣由

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
#🧠 Question :: ->->-> ``

---
Status: 
Tags:
Links:
References:
[[@ithomeWantKnowReact]]
[[@collinsSpecializeDefinitionMeaning]]
[[@collinsContainmentDefinitionMeaning]]