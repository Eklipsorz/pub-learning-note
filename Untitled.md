


事件處理器 命名法則：field 是指 發生事件的元件、event是指事件名稱、Handler是指處理器

- field + event + Handler ，比如titleChangeHandler

- event + Handler ，比如clickHandler


由於React的事件綁定是由原生JS的事件綁定來實現的，所以可以直接調用原生JS的事件綁定會有的東西來在React上實現。  
- event 物件：存放事件發生資訊的物件，會於事件發生時就會產生
- event.target ：會以實際DOM節點來表示哪個節點發生該事件
- event.target.value：會以該節點物件中的value屬性取值

  
```
const titleChangeHandler = (event) => {
	console.log(event.target.value);
};
```


在這裡要實現表格發生提交時，就把目前的輸入欄位值發送至特定地方，有兩個解法：

- 該輸入欄位發生value 變動事件時就先以狀態來儲存對應value，然後等到使用者按下提交時，就把這些狀態值以物件的形式來儲存，並發送

  

that will always happen when you update the state but i'm doing it to enure that we're storing this in some variable, which is kind of detached from the life cycle of this component function.

So that no matter how often this component function might execute again, this state is stored and survives

除了狀態系統來儲存以外，
1. 還能以component function的區域變數和GC間的關係來儲存每一次所輸入的內容，只是GC是根據其記憶體是否還繼續參照使用才會保留，若之後都沒在使用區域變數或者輸入內容的話，其記憶體就會被GC被判定不被使用就直接被釋放掉

使用狀態來儲存是
- 為了確保不受到component的對應函式因被執行而變更到內容 
- 不被GC釋放


there would be other ways of solving this as well but that works just fine

adv:
1. we'll need that state for updating and for re-rendering that component later anyways




maybe a problem you also encountered, how can you manage more than one state。

解法1:
1. 替每個狀態都使用useState來註冊

  

舉例來說假設要以標題、價錢、日期作為三個狀態來儲存，那麼就是在同一個component的對應函式增加三個useState：(狀態變數=>儲存狀態的變數)
   - 這個元件具有三個獨立的狀態變數
   - 每個狀態對應的更新用函式並不會影響其他狀態變數，只會影響他們各自設定的對應狀態變數

```
function Component(props) {
    const [title, setTitle] = useState('');
    const [amount, setAmount] = useState('');
    const [date, setDate] = useState('');
    //..
}
```

event.target.value 皆以字串來表示，而非數字