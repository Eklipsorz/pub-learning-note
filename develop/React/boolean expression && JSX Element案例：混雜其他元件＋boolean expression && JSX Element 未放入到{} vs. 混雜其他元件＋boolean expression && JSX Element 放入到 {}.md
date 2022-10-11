
## 描述


### boolean expression && JSX Element 未放入到{} vs. boolean expression && JSX Element 放入到 {}

前者使用boolean expression && JSX Element 來表示 JSX Element，雖然語法上可行，但由於 混雜其他元件，導致error && 會構成字串來看待，而JSX Element則是必定被渲染上去，且附加著著以null物件來存取屬性，這會使系統報錯
```
const [error, setError] = useState(null);
return (
    <div>
      error && (
        <ErrorModal
          title={error.title}
          text={error.text}
          onErrorModal={onErrorModalClickHandler}
        ></ErrorModal>
      )
      <Card>
        <form className={styles['form']} onSubmit={submitHandler}>
          <div className={styles['form-control']}>
            <label>Username</label>
            <input value={userName} onChange={userNameChangeHandler} />
          </div>
          <div className={styles['form-control']}>
            <label>Age(Years)</label>
            <input value={age} onChange={ageChangeHandler} />
          </div>
          <Button type='submit'>Add User</Button>
        </form>
      </Card>
    </div>
  );
```

後者將boolean expression && JSX Element放入JSX中的\{\}，會以JavaScript表達式來解析其error是否為true，若是null，會是false；若是非null，就會是true，在這裡，error在判斷結果下得到true會得到後面的JSX Element。

```
  const [error, setError] = useState(null);
  return (
    <div>
      {error && (
        <ErrorModal
          title={error.title}
          text={error.text}
          onErrorModal={onErrorModalClickHandler}
        ></ErrorModal>
      )}
      <Card>
        <form className={styles['form']} onSubmit={submitHandler}>
          <div className={styles['form-control']}>
            <label>Username</label>
            <input value={userName} onChange={userNameChangeHandler} />
          </div>
          <div className={styles['form-control']}>
            <label>Age(Years)</label>
            <input value={age} onChange={ageChangeHandler} />
          </div>
          <Button type='submit'>Add User</Button>
        </form>
      </Card>
    </div>
  );
```


## 複習

#🧠 以下是實現根據輸入欄位是否出錯而跑出對話視窗，請問這能正常執行嗎？為什麼？假如輸入欄位有誤的話會自動填寫error物件![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1662804461/blog/frontend/conditional-rendering/boolean_expression_JSX_Element%E6%A1%88%E4%BE%8B_vl9bwv.png) ->->-> `能，boolean expression && JSX Element放入JSX中的{}，會以JavaScript表達式來解析其error是否為true，若是null，會是false；若是非null，就會是true，在這裡，error在判斷結果下得到true會得到後面的JSX Element。`
<!--SR:!2022-11-13,39,250-->


#🧠  下是實現根據輸入欄位是否出錯而跑出對話視窗，請問這能正常執行嗎？為什麼？假如輸入欄位有誤的話會自動填寫error物件 ![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1662804461/blog/frontend/conditional-rendering/boolean_expression_JSX_Element%E6%A1%88%E4%BE%8B_kne0ew.png) ->->-> `boolean expression && JSX Element 來表示 JSX Element，雖然語法上可行，但由於 混雜其他元件，導致error && 會構成字串來看待，而JSX Element則是必定被渲染上去，且附加著著以null物件來存取屬性，這會使系統報錯`
<!--SR:!2022-11-30,50,250-->


---
Status: #🌱
Tags:
[[React]]
Links:
[[在渲染層面下，render 函式回傳的內容若單純添加boolean expression && JSX element 的話，會使其語法正常執行，反之在其基礎下添加其他元素的話，其語法會被視為字串和一般的React Element來看待]]
[[React 解析boolean expression && JSX element  時，若前者為true，就以後者的JSX element為主，否則就忽略該Virtual DOM]]

References: