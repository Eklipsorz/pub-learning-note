## 描述


[[React：表格提交非法輸入欄內容時會有的處理]]
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

提出額外的狀態來解決 無法透過validity 和 value來全然表示元件的所有狀態

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
	- untouched 狀態為該元件



## 複習


---
Status: #🌱 
Tags:
[[React]]
Links:
[[React：表格提交非法輸入欄內容時會有的處理]]
[[React：表格下的輸入欄內容存取方式有兩種：第一種使用React體系的事件＋state；第二種為使用ref]]
[[React：表格製作的難點為格本身具有較多狀態要管理，主要有validity和value以及validity得要考量什麼時候驗證以及如何驗證]]
References:
[[@codecraftModelDrivenFormValidation]]