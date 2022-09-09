## 描述


### JSX Limitations
1. 一定要有parent element包覆其他元素
2. 最外圍的parent element只能有一個

one element which you are allowed to have may of course have more children which then also can be adjacent to each other


###
```
return (
	<Element1 />
	<Element2 />
)
```
  
#### 解法1：使用額外的元件來當wrapper element
通常會拿div當wrapper element ，但不會是絕對

```
return (
	<div> 
		<Element1 />
		<Element2 />
	</div>
)
```

#### 解法2：利用React解析陣列的特性來使用陣列表示
```
return (
	[
		<Element1 />,
		<Element2 />
	]
)
```


your JSX code translates into React create element

案例，如果要在裡頭添加顯示錯誤訊息的對話視窗，需要一個能夠獨立於Card元件的元件來建立，但這樣會違反不能有超過一個parent element來包覆
```
return (
	  <ErrorModal />
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
  );
```

因此解決辦法為在Card最上層增加div元素，然後再由div元素包含錯誤訊息的對話視窗和Card
```
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
Status: 
Tags:
Links:
References: