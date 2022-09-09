## 描述


### JSX Limitations
1. 一定要有parent element包覆其他元素
2. 最外圍的parent element只能有一個

one element which you are allowed to have may of course have more children which then also can be adjacent to each other


### 解法
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

##### 由於使用陣列，可能會遇到Each child in a list should have a unique "key" prop 問題

要解決的話，要對陣列的每個項目添加key屬性


##### 案例

若要將下面案例轉成陣列形式，必須要注意的是ErrorModal是boolean expression && JSX Element 所構成
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

boolean expression && JSX Element 可以被當作一種JSX元素，只有前者為true，才以後者的JSX Element為主，若前者為false，就會被React給忽略。

```
  return (
    [
      error && (
        <ErrorModal
          title={error.title}
          text={error.text}
          onErrorModal={onErrorModalClickHandler}
        ></ErrorModal>
      ),
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
    ]
  );
```



## 複習


---
Status: #🌱 #📓 
Tags:
[[React]]
Links:
[[渲染部分{expression}中的expression是指陣列的話，React 會直接將陣列上的每個元素當成react element 來並排當作渲染內容]]
[[React：Keys概念是用特定資料的識別字去對應著特定Virtual DOM節點，以此在變更內容的情況下，好讓React能夠分辨哪個實際DOM節點是隸屬於哪個資料]]
[[Each child in a list should have a unique "key" prop. 表示開發者有使用陣列來表示多個JSX Elemenet ，在這裡系統會建議開發者替陣列的每個項目增加key屬性以確保每個項目都能對應到DOM節點]]
[[React 解析boolean expression && JSX element  時，若前者為true，就以後者的JSX element為主，否則就忽略該Virtual DOM]]
References: