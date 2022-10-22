## 描述


[[React：在表格提交事件中，表格提交非法輸入欄內容時會有的處理]]
```
const [enteredNameIsValid, setEnteredNameIsValid] = useState(true);
```
根據以上案例，若在一開始將輸入欄的validity設為true的話，會有以下潛在問題：
	- 無法在mount階段時期反映真實狀態而使結果變成預期外結果：系統會認為enteredName為合法來執行對應的處理，但實際上由於輸入欄一開始不會有任何值，理論上會是要設定false為初始值。


### validity和value來呈現是足夠呈現實際表格能夠呈現的狀態嗎

1. 並不能，最主要實際狀態種類數會是無限
2. 無限的理由為實際表格會有的狀態取決於互動種類，而互動種類數本身在通常情況下(沒限制)而會是無限

#### 若目前開發者預期的表格狀態數不夠

解法：
1. 新增狀態種類來處理

若貿然不管的話，後果會是：
1. 會在有限狀態下因為狀態種類不夠表示而產出預期外結果


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

- 渲染部分：設定條件來決定渲染部分：
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


#🧠 React：表格下只擁有兩種狀態：validity和value來呈現是足夠呈現實際表格能夠呈現的狀態嗎？ 原因為何？->->-> `並不能，最主要實際狀態種類數會是無限，所以光是兩種就是不夠`

#🧠 React：實際表格能夠呈現的狀態數為何是無限？ ->->-> `實際表格會有的狀態取決於互動種類，而互動種類數本身在通常情況下(沒限制)而會是無限`

#🧠 React： 在表格開發中，若目前開發者預期的表格狀態數不夠，其解法會是什麼？->->-> `新增狀態種類來處理`

#🧠  React： 在表格開發中，若目前開發者預期的表格狀態數不夠，但不管問題的話，其後果會是什麼？ ->->-> `會在有限狀態下因為狀態種類不夠表示而產出預期外結果`

#🧠 React：若於對應元件的函式內添加這 const \[enteredNameIsValid, setEnteredNameIsValid\] = useState(true);  會有什麼潛在問題？->->-> `在mount階段時期，系統會認為enteredName為合法來執行對應的處理，但實際上由於輸入欄一開始不會有任何值，理論上會是要設定false為初始值。`

#🧠 React：以下為一個表格的實現代碼，請問這會有什麼潛在問題？ https://res.cloudinary.com/dqfxgtyoi/image/upload/v1666410154/blog/react/form/validity-and-value-true-boolean-example_oap1fp.png ->->-> `無法在mount階段時期反映真實狀態而使結果變成預期外結果：系統會認為enteredName為合法來執行對應的處理，但實際上由於輸入欄一開始不會有任何值，理論上會是要設定false為初始值。`

#🧠 React：以下為一個表格的實現代碼，請問為什麼enteredNameIsValid一開始會是true，而不是反映目前狀態為false？ https://res.cloudinary.com/dqfxgtyoi/image/upload/v1666410154/blog/react/form/validity-and-value-true-boolean-example_oap1fp.png  ->->-> `主要是為了使渲染部分能夠正確按照情況下來印出對應畫面，而非是印出非法內容，換言之，若一開始將validity設定為false，就會讓畫面印出非法的樣式`

#🧠 React：以下為一個表格的實現代碼，validity的初始狀態值為true或者false都會出現有問題，那麼這會是代表著？  https://res.cloudinary.com/dqfxgtyoi/image/upload/v1666410154/blog/react/form/validity-and-value-true-boolean-example_oap1fp.png  ->->-> `value 和 validity 已經無法呈現表格目前的狀態`

#🧠 React：以下為一個表格的實現代碼，validity的初始狀態值為true或者false都會出現有問題，那麼這會是代表value 和 validity 已經無法呈現表格目前的狀態，那麼解法概念會是以什麼作為核心？？  https://res.cloudinary.com/dqfxgtyoi/image/upload/v1666410154/blog/react/form/validity-and-value-true-boolean-example_oap1fp.png   ->->-> `提出另一個名為touched狀態來表示`

#🧠 React：以下為一個表格的實現代碼，validity的初始狀態值為true或者false都會出現有問題，那麼這會是代表value 和 validity 已經無法呈現表格目前的狀態，那麼解法概念具體會是什麼？？  https://res.cloudinary.com/dqfxgtyoi/image/upload/v1666410154/blog/react/form/validity-and-value-true-boolean-example_oap1fp.png   ->->-> ` 註冊touched 狀態；設定可使touched為true的情況，在這裏是以表格提交事件來預設所有輸入欄皆為touched；渲染部分：設定條件來決定渲染部分`

#🧠 React：touched/untouched 狀態各代表著什麼？ ->->-> `標明元件是否為曾經被使用者點選過或者曾經被使用者切換成active element；touched 狀態為該元件曾經被切換成active element； untouched 狀態為該元件從未被切換成active element`

#🧠 React：無法在mount階段時期反映真實狀態，系統會認為enteredName為合法來執行對應的處理，請問 https://res.cloudinary.com/dqfxgtyoi/image/upload/v1666410154/blog/react/form/validity-and-value-true-boolean-example_oap1fp.png  ->->-> ``



#🧠 React：若目前元件是active element，嚴格來說算是touched嗎？為什麼 ->->-> `不能算是，基本上會因為並未從active這狀態轉移，因此不算是`


#🧠 React：touched/untouched 狀態 具體會由誰來決定？ ->->-> ``依據著開發者來指定或者程式來指定

#🧠 React：touched/untouched 狀態值具體會依據著開發者來指定或者程式來指定，請以開發者來決定為例子來說明 ->->-> `當表格發生提交時，表格下的所有元件都會被設定為touched，預設上就是輸入完這些輸入欄才會按下提交按鈕，雖然實際上可能會有部分輸入欄是因為可選擇不輸入而沒變成active element`

#🧠 React touched/untouched  ：當表格發生提交時，表格下的所有元件都會被設定為touched，即使有部分輸入欄並沒變成active element，為什麼都設定為touched？ ->->-> `預設上就是輸入完這些輸入欄才會按下提交按鈕`

---
Status: #🌱 
Tags:
[[React]]
Links:
[[React：在表格提交事件中，表格提交非法輸入欄內容時會有的處理]]
[[React ：在表格提交事件中，表格下的輸入欄內容存取方式有兩種：第一種使用React體系的事件＋state；第二種為使用ref]]
[[React：表格製作的難點為表格本身具有較多狀態要管理和控制]]
References:
[[@codecraftModelDrivenFormValidation]]