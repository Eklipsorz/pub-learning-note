
## 描述
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
References: