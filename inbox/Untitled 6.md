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
4. 輸入完表單後並按下按鈕點擊提交時，可正常導向，不會有任何prompt來阻擋

### 確保使用者正對表單頁面下的表單進行輸入並紀錄

1. 在元件下註冊isEntering這狀態
```
const [isEntering, setIsEntering] = useState(false);
```

2. 在表單下的onFocus事件來設定該狀態為true，以此來表示表單正被輸入
```
  const formFocusHandler = () => {
    setIsEntering(true);
  };
```

```
        <form
          className={classes.form}
          onSubmit={submitFormHandler}
        />
```

[[focus事件為特定元件轉變成active element的時機點]]

### 添加Prompt元件來當作警告訊息來阻擋

根據Prompt的when是否true來啟用prompt來阻擋，若form發生focus事件就為true；反之就為false。若呈現prompt就以Are you sure這訊息來表示
```
<Prompt when={isEntering} message={(location) => 'Are you sure??'} />
```

[[navigation 是網頁用來幫助使用者在一個頁面下被該頁面下的元件導向其他頁面的區塊，具體區塊內會含有多個hyperlink給予使用者做互動來導向]]

[[prompt 是由react-router-dom 所提供的元件，主要是一個對話視窗，該元件會監聽使用者是否透過目前頁面的任意元件切換成另一個網址，若有的話，可依據情況在切換前以一個對話視窗來阻擋]]
  


### 輸入完表單後並按下按鈕點擊提交時，可正常導向
[[預設下瀏覽器會替每個表單設定該SubmitEvent ，並定義表單下的提交按鈕被點擊後才產生submit 事件信號給表單，轉遞click event的話，會是先往parent節點來進行轉遞，轉遞submit event的話，則是表格]]

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
[[focus事件為特定元件轉變成active element的時機點]]
[[prompt 是由react-router-dom 所提供的元件，主要是一個對話視窗，該元件會監聽使用者是否透過目前頁面的任意元件切換成另一個網址，若有的話，可依據情況在切換前以一個對話視窗來阻擋]]
[[navigation 是網頁用來幫助使用者在一個頁面下被該頁面下的元件導向其他頁面的區塊，具體區塊內會含有多個hyperlink給予使用者做互動來導向]]
[[預設下瀏覽器會替每個表單設定該SubmitEvent ，並定義表單下的提交按鈕被點擊後才產生submit 事件信號給表單，轉遞click event的話，會是先往parent節點來進行轉遞，轉遞submit event的話，則是表格]]
References: