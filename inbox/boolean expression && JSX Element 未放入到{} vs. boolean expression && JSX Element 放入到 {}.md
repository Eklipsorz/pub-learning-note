
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

後者將boolean expression && JSX Element放入JSX中的\{\}，會以JavaScript表達式來解析其error是否為true，才得到後面的JSX Element。

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





---
Status: #🌱 #📓 
Tags:
[[React]]
Links:
[[boolean expression && JSX element 只會在元件本身就是該形式才會變成JSX element，若混雜其他元件就會將boolean expression視為字串，JSX element則是無論如何都會被渲染的元件]]
References: