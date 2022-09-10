## 描述

[[React：過度使用wrapper element來解決JSX侷限問題，會產生兩大問題，第一會破壞CSS選擇器所選擇的節點、第二瀏覽器會渲染出不必要出現的HTML元素，甚至會重複渲染]]



### Wrapper.js 打造一個假的wrapper component

假的wrapper component實際上會只內含著它所包含的子節點內容，不會有額外的元件來包含子節點內容，只要使用wrapper，就只會回傳它的子節點。

```
const Wrapper = (props) => {
  return props.children;
};

export default Wrapper;
```

使用wrapper component來包含內容
```
return (
	<Wrapper>
		<div>....</div>
	</Wrapper>
)
```

等同以下語法，而這語法是合法的
```
return (React.createElement(Wrapper,{}, React.createElemennt('div',{}....)))
```

#### 總結
製作假的wrapper component是：
1. 憑藉著wrapper轉換語法是合法
2. wrapper單純回傳子節點


#### 案例

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



使用div元件繼續當wrapper component，會在section和card元件之間多一個div
![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1662745521/blog/frontend/conditional-rendering/before-wrapper_fbmo12.png)



```
return (
    <Wrapper>
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
    </Wrapper>
  );
```

使用假的parent element來充當wrapper component，並不會讓section和card元件多一個div元件
![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1662745520/blog/frontend/conditional-rendering/after-wrapper_qieupz.png)

## 複習

---
Status: #🌱 #📓 
Tags:
[[React]]
Links:
[[JSX 侷限一定要有parent element包覆其他元素和最外圍的parent element只能有一個，解法有wrapper element、array]]
[[React：過度使用wrapper element來解決JSX侷限問題，會產生兩大問題，第一會破壞CSS選擇器所選擇的節點、第二瀏覽器會渲染出不必要出現的HTML元素，甚至會重複渲染]]
References: