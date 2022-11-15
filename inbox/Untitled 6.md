## 描述


### 實現表單頁面離開前警告提示
> where you can enter data in a form this is prevented by a prompt which is shown to you asking you if you really wanna navigate away.

  

> So that as soon as you started working on that form, you can't accidentally leave it and that's a behavior we also might want to implement

  
功能描述為：
0. 跳轉為從目前頁面至其他頁面的行為
1. 當使用者進入表單頁面並對表單進行輸入時，只有提交按鈕點擊才能夠正常跳轉其他頁面
2. 當使用者進入表單頁面並對表單進行輸入時，若使用非提交按鈕的方式來跳轉，會跳出警告訊息來阻擋離開，警告視窗會有ok和cancel，按下ok就允許離開，而按下cancel就是取消

### 具體會用到的實現
1. 確保使用者正對表單頁面下的表單進行輸入並紀錄
2. 添加Prompt元件來當作警告訊息來阻擋，其元件會具有ok和cancel，ok會帶有允許他人離開的功能；cancel則是取消離開
3. 其Prompt元件必須要能根據使用者是否正輸入表單來阻擋，有輸入就阻止；沒輸入就不阻止

### 確保使用者正對表單頁面下的表單進行輸入並紀錄

1. 在元件下註冊isEntering這狀態



###

first, we wanna determine when the user starts working with this form e.g., when this form gains focus.

實現會是使用 form focus事件

  

  

focus事件為特定元件轉變成active element的瞬間

  

The `**focus**` event fires when an element has received focus.

###

wanna store that info that's this form was focused

1. 為表單focus事件處理添加狀態

2. 當focus時就設定狀態為true

  

prompt component

1. 由react-router-dom所提供

2. 自動監測特定規則是否滿足，若滿足就呈現warning，若不滿足就不呈現。

3. Prompt 有兩個主要的attributes：

- when：布林值，true為渲染prompt來阻止從目前頁面跳轉；false為不使用prompt來阻止

> to finding whether this prompt should be shown if the user changes the URL or not

- message：字串或者function，主要是指定prompt的主體訊息是什麼，當使用function可以根據使用者對於瀏覽紀錄的操作和位置來定義後續處理，回傳內容正是指定prompt的主體訊息

=> (location, action) => {} 中的location 是指使用者當前要跳轉的頁面位置，action是指使用者當前對於瀏覽紀錄的操作是什麼

  

> this is a component which we can render. And then this component will automatically watch if we navigate away. And if then a certain condition is met, it will show a warning before it allows use to leave

  

Used to prompt the user before navigating away from a page. When your application enters a state that should prevent the user from navigating away (like a form is half-filled out), render a `<Prompt>`.

###


當使用者按下prompt下的ok時，並不會因此而直接允許跳轉，主要會根據prompt的when是否為true，仍是true就會保持渲染prompt

為了解決這問題，必須要使prompt為false

```
const QuoteForm = (props) => {
  const authorInputRef = useRef();
  const textInputRef = useRef();
  const [isEntering, setIsEntering] = useState(false);
  console.log('render');
  function submitFormHandler(event) {
    event.preventDefault();

    const enteredAuthor = authorInputRef.current.value;
    const enteredText = textInputRef.current.value;
    console.log('submit');
    // optional: Could validate here

    props.onAddQuote({ author: enteredAuthor, text: enteredText });
  }

  const formFocusHandler = () => {
    setIsEntering(true);
  };

  const formConfirmBtnHandler = () => {
    setIsEntering(false)
    console.log('finished')
  }

  return (
    <Fragment>
      <Prompt when={isEntering} message={(location) => 'Are you sure??'} />
      <Card>
        <form
          className={classes.form}
          onSubmit={submitFormHandler}
          onFocus={formFocusHandler}
        > 
		.
		.
			<button className='btn' onClick={formConfirmBtnHandler}>
				Add Quote
			</button>
		</form>
	  </Card>
	</Fragment>
  );
}
```



```
render
finished 
render 
submit
```

#### prompt 元件本身不提供按下ok就直接跳轉的功能



## 複習


---
Status: #🌱 
Tags:
[[React]]
Links:
References: