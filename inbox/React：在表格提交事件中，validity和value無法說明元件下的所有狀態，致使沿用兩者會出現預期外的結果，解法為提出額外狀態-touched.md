## 描述


[[React：在表格提交事件中，表格提交非法輸入欄內容時會有的處理]]
```
const [enteredNameIsValid, setEnteredNameIsValid] = useState(true);
```
根據以上案例，若在一開始將輸入欄的validity設為true的話，會有以下潛在問題：
	- 在mount階段時期，系統會認為enteredName為合法來執行對應的處理，但實際上由於輸入欄一開始不會有任何值，理論上會是要設定false為初始值。


### 一開始將輸入欄的validity設為true的原因

主要是為了使渲染部分能夠正確按照情況下來印出對應畫面，而非是印出非法內容，換言之，若一開始將validity設定為false，就會讓畫面印出非法的樣式。

```
const formControlCSS = enteredNameIsValid
    ? 'form-control'
    : 'form-control invalid';

  return (
    <form onSubmit={submitHandler}>
      <div className={formControlCSS}>
        <label htmlFor='name'>Your Name</label>
        <input
          type='text'
          id='name'
          onChange={changeHandler}
          value={enteredName}
        />
      </div>
      {!enteredNameIsValid && <p className='error-text'>Name is invalid!!</p>}
      <div className='form-actions'>
        <button>Submit</button>
      </div>
    </form>
  );
```




  
### 案例：在mount階段時期會誤判的代碼

```
1.  useEffect(() => {
2.     if (enteredNameIsValid) {
3.         console.log('Name is valid');
4.     } 
5.  }, [enteredNameIsValid]);
```


### 兩難問題解法：validity設定false ? true？

validity 和 value 是無法應付表格所會有的互動表現，換言之，表格實際需要的狀態至少會是兩種以上狀態。面對上述難題，解法會是提出額外的狀態來解決 無法透過validity 和 value來代表表格所會有的互動表現

```
const [enterNameIsValid, setEnteredNameIsValid] = useState(false);
const [enteredNameTouched, setEnteredNameTouched] = useState(false);
```

  [[@codecraftModelDrivenFormValidation]]
> A controls is said to be _touched_ if the the user focused on the control and then focused on something else.

> one change definitely is the form submission. If the form is submitted, all inputs are treated as touched. Even if the user didn't type into them, the user submitted to the overall form.

> which basically means the user confirms the overall form. So we could treat all inputs as touched in this case

重點：
- touched/untouched 狀態 標明元件是否為曾經被使用者點選過或者曾經被使用者切換成active element：
	- touched 狀態為該元件曾經被切換成active element
	- untouched 狀態為該元件從未被切換成active element
- touched/untouched 狀態值具體會依據著開發者來指定或者程式來指定，比如說當表格發生提交時，表格下的所有元件都會被設定為touched，預設上就是輸入完這些輸入欄才會按下提交按鈕，雖然實際上可能會有部分輸入欄是因為可選擇不輸入而沒變成active element
- 從validity 和value 的案例來看，validity 和 value 是無法應付表格所會有的互動表現，換言之，表格實際需要的狀態至少會是兩種以上狀態

#### 具體實現


- 註冊touched 狀態
```
const [enteredNameTouched, setEnterNameTouched] = useState(false);
```
- 設定可使touched為true的情況，在這裏是以表格提交事件來預設所有輸入欄皆為touched
```
 const submitHandler = (event) => {
    event.preventDefault();
    setEnterNameTouched(true);
	.
	.
}
```

- 設定條件來決定渲染部分：
```
const enteredNameIsInvalid = !enteredNameIsValid && enteredNameTouched;
const formControlCSS = enteredNameIsInvalid
    ? 'form-control invalid'
    : 'form-control';

return (
	{enteredNameIsInvalid && <p className='error-text'>Name is invalid!!</p>}
)
```


```
const SimpleInput = (props) => {
  const [enteredName, setEnteredName] = useState('');
  const [enteredNameIsValid, setEnteredNameIsValid] = useState(false);
  const [enteredNameTouched, setEnterNameTouched] = useState(false);

  const changeHandler = (event) => {
    setEnteredName(event.target.value);
  };

  const submitHandler = (event) => {
    event.preventDefault();
    setEnterNameTouched(true);

    if (enteredName.trim() === '') {
      setEnteredNameIsValid(false);
      return;
    }

    setEnteredNameIsValid(true);
    console.log(enteredName);
  };
  const enteredNameIsInvalid = !enteredNameIsValid && enteredNameTouched;
  const formControlCSS = enteredNameIsInvalid
    ? 'form-control invalid'
    : 'form-control';

  return (
    <form onSubmit={submitHandler}>
      <div className={formControlCSS}>
        <label htmlFor='name'>Your Name</label>
        <input
          type='text'
          id='name'
          onChange={changeHandler}
          value={enteredName}
        />
      </div>
      {enteredNameIsInvalid && <p className='error-text'>Name is invalid!!</p>}
      <div className='form-actions'>
        <button>Submit</button>
      </div>
    </form>
  );
};
```

> one change definitely is the form submission. If the form is submitted, all inputs are treated as touched. Even if the user didn't type into them, the user submitted to the overall form.

> which basically means the user confirms the overall form. So we could treat all inputs as touched in this case



## 複習


---
Status: #🌱 
Tags:
[[React]]
Links:
[[React：在表格提交事件中，表格提交非法輸入欄內容時會有的處理]]
[[React ：在表格提交事件中，表格下的輸入欄內容存取方式有兩種：第一種使用React體系的事件＋state；第二種為使用ref]]
[[React：表格製作的難點為格本身具有較多狀態要管理，主要有validity和value以及validity得要考量什麼時候驗證以及如何驗證]]
References:
[[@codecraftModelDrivenFormValidation]]