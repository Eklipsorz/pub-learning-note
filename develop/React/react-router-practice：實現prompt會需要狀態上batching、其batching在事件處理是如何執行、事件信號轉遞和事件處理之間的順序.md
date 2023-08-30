## 描述


### 實現表單頁面離開前警告提示
> where you can enter data in a form this is prevented by a prompt which is shown to you asking you if you really wanna navigate away.

  

> So that as soon as you started working on that form, you can't accidentally leave it and that's a behavior we also might want to implement

  
功能描述為：
0. 跳轉為從目前頁面至其他頁面的行為
1. 當使用者進入表單頁面並對表單進行輸入時，只有提交按鈕點擊才能夠正常跳轉其他頁面
2. 當使用者進入表單頁面並對表單進行輸入時，若使用非提交按鈕的方式來跳轉，會跳出警告訊息來阻擋離開，警告視窗會有ok和cancel，按下ok就允許離開，而按下cancel就是取消

### 具體會用到的實現
1. 確保使用者正對表單頁面下的表單進行輸入並紀錄狀態
2. 添加Prompt元件來當作警告訊息來阻擋，其元件會具有ok和cancel，ok會帶有允許他人離開的功能；cancel則是取消離開
3. 其Prompt元件必須要使用者是正輸入表單的情況下來阻擋URL Navigation
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

1. 在提交按鈕的點擊事件添加狀態更新為false
```
 const formConfirmBtnHandler = () => {
    setIsEntering(false)
}
```

2. 剩下的就利用batching 、事件信號轉遞、事件處理的順序來實現

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


在這裡按鈕發生點擊後，必須要執行完對應事件處理A才會轉遞submit信號至表格上，其中事件處理A會要求更新false的狀態，在這裡下一個會執行的事件處理會是表格的提交事件，而在這裡由於事件處理A要做完自己的處理後才傳遞submit信號才能做表格的提交事件處理，過程中的狀態更新會因為 **每個事件處理下的所有狀態更新指令，會等到最後一行執行結束後，就以目前結果狀態來更新狀態和渲染** 而先在傳遞submit信號之前就處理狀態更新和渲染

之後表格接收到submit信號並執行提交事件時，會是以最新渲染內容來執行目前事件處理，而表格提交事件處理會是從prompt所在的頁面跳轉至quotes頁面，然而prompt的when屬性是false，所以並不會以prompt來阻止，若沒在submit信號之前處理的話，那麼就會因為ture而被阻止。

主要能實現歸功於：
- 每個事件處理都各自處理自己的batching
- 每個事件處理下的所有狀態更新指令，會等到最後一行執行結束後，就以目前結果狀態來更新狀態和渲染
- submit信號傳遞要等到按鈕點擊事件完成後才轉遞

#### 每個事件處理都各自處理自己的batching

1. 每個事件處理下的所有狀態更新指令，會等到最後一行執行結束後，就以目前結果狀態來更新狀態和渲染



## 複習

#🧠 實現表單頁面離開前警告提示，所需要會用到的實現概念會是什麼？ ->->-> `確保使用者正對表單頁面下的表單進行輸入並紀錄狀態、添加Prompt元件來當作警告訊息來阻擋，其元件會具有ok和cancel，ok會帶有允許他人離開的功能；cancel則是取消離開、其Prompt元件必須要使用者是正輸入表單的情況下來阻擋URL Navigation、輸入完表單後並按下按鈕點擊提交時，可正常導向，不會有任何prompt來阻擋`
<!--SR:!2023-08-21,89,210-->


#🧠 React：實現表單頁面離開前警告提示，所需要會用到的實現概念中的確保使用者正對表單頁面下的表單進行輸入並紀錄狀態，如何做？ ->->-> `在元件下註冊isEntering這狀態、在表單下的onFocus事件來設定該狀態為true，以此來表示表單正被輸入`
<!--SR:!2023-08-09,162,250-->

#🧠 React：實現表單頁面離開前警告提示，所需要會用到的實現概念中的添加Prompt元件來當作警告訊息來阻擋和其Prompt元件必須要使用者是正輸入表單的情況下來阻擋URL Navigation，如何做？prompt程式碼會是什麼 ->->-> `使用react-router-dom所提供的prompt元件、根據Prompt的when是否true來啟用prompt來阻擋，若form發生focus事件就為true；反之就為false。若呈現prompt就以Are you sure這訊息來表示。<Prompt when={isEntering} message={(location) => 'Are you sure??'} />`
<!--SR:!2023-12-03,138,190-->

#🧠 React-router-dom：實現表單頁面離開前警告提示，所需要會用到的實現概念中的輸入完表單後並按下按鈕點擊提交時就可正常導向，如何在prompt實現？->->-> `在提交按鈕的點擊事件添加狀態更新為false`
<!--SR:!2024-04-20,277,230-->

#🧠 React：實現表單頁面離開前警告提示，所需要會用到的實現概念中的輸入完表單後並按下按鈕點擊提交時就可正常導向，以下為程式碼，請解釋為何可以實現 https://github.com/academind/react-complete-guide-code/blob/20-building-mpas-with-react-router/code/17-preventing-unwanted-route-transitions/src/components/quotes/QuoteForm.js  ->->-> `在這裡按鈕發生點擊後，必須要執行完對應事件處理A才會轉遞submit信號至表格上，其中事件處理A會要求更新false的狀態，在這裡下一個會執行的事件處理會是表格的提交事件，而在這裡由於事件處理A要做完自己的處理後才傳遞submit信號才能做表格的提交事件處理，過程中的狀態更新會因為 **每個事件處理下的所有狀態更新指令，會等到最後一行執行結束後，就以目前結果狀態來更新狀態和渲染** 而先在傳遞submit信號之前就處理狀態更新和渲染 。之後表格接收到submit信號並執行提交事件時，會是以最新渲染內容來執行目前事件處理，而表格提交事件處理會是從prompt所在的頁面跳轉至quotes頁面，然而prompt的when屬性是false，所以並不會以prompt來阻止，若沒在submit信號之前處理的話，那麼就會因為ture而被阻止。`
<!--SR:!2023-08-05,163,250-->

#🧠 React-router-dom：實現表單頁面離開前警告提示，所需要會用到的實現概念中的輸入完表單後並按下按鈕點擊提交時就可正常導向，以下為程式碼 https://github.com/academind/react-complete-guide-code/blob/20-building-mpas-with-react-router/code/17-preventing-unwanted-route-transitions/src/components/quotes/QuoteForm.js 這主要能實現歸功於?(batching、最後一行、轉遞順序) ->->-> `- 每個事件處理都各自處理自己的batching - 每個事件處理下的所有狀態更新指令，會等到最後一行執行結束後，就以目前結果狀態來更新狀態和渲染 - submit信號傳遞要等到按鈕點擊事件完成後才轉遞`
<!--SR:!2023-10-11,78,230-->

#🧠 React：實現表單頁面離開前警告提示，所需要會用到的實現概念中的輸入完表單後並按下按鈕點擊提交時就可正常導向，以下為程式碼 https://github.com/academind/react-complete-guide-code/blob/20-building-mpas-with-react-router/code/17-preventing-unwanted-route-transitions/src/components/quotes/QuoteForm.js 這主要能實現歸功於? ->->-> `- 每個事件處理都各自處理自己的batching - 每個事件處理下的所有狀態更新指令，會等到最後一行執行結束後，就以目前結果狀態來更新狀態和渲染 - submit信號傳遞要等到按鈕點擊事件完成後才轉遞`
<!--SR:!2023-08-10,167,250-->

#🧠 React：每個事件處理都有狀態更新指令或者函式，請問如何執行batching？ ->->-> `首先，每個事件處理都各自處理自己的batching、每個事件處理下的所有狀態更新指令，會等到最後一行執行結束後，就以目前結果狀態來更新狀態和渲染`
<!--SR:!2023-11-23,84,230-->

#🧠 React：事件處理A會要求將狀態true更新成false的狀態，事件處理A處理完畢才轉遞提交事件給表格，接著就執行提交事件處理，請問提交事件處理時的渲染內容會是以誰為主？以true為主？還是 false? 為何？ ->->-> `會是以false為主，由於每個事件處理下的所有狀態更新指令之batching，會是等到事件處理的最後一行結束後才執行，所以在事件處理A的最後一行執行後就會更新狀態和渲染，接著才轉遞提交事件信號給表單，執行提交事件處理，這時的執行會是以false為主`
<!--SR:!2023-08-24,174,250-->





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