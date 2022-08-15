



why use a const

`const [title, setTitle] = useState(props.title)`

  

useState function：

1. register some state or some value as a state for the component in which it is being called

2. it registers it for a specific component instance

  


  

e.g.,  在這裡有四個ExpenseItem，每一個會呼叫元件對應函式來渲染並各自生成特定特殊變數來註冊在目前所建立的元件實例，換言之會有四個特殊變數各自綁定第一項ExpenseItem、第二項ExpenseItem、....、第四項ExpenseItem，特殊變數會以狀態值來控制著每一項的內容。

```
<ExpenseItem></ExpenseItem>
<ExpenseItem></ExpenseItem>
<ExpenseItem></ExpenseItem>
<ExpenseItem></ExpenseItem>
```
  


多個相同元件的事件綁定處理，處理不好的問題：

- 當一個元件發生事件，全部元件就引發對應事件處理



now, in addition, whenever State changes because we click a button in this case.

it only this component function and only that specific instance where this component is being used where React will re-evalate 

  

that state really is separated on a per component instance basis

每一個元件都各有一個狀態


- [ ] why am i using const here

  

useState：

3. 獲取目前綁定的最新狀態、狀態更新用的函式

  

setTitle('updated'); 和 title = 'updated' 是不一樣的

setTitle('updated') 的更新是更新其特殊變數的狀態，該特殊變數會由React管理，本身也不會更新title這變數