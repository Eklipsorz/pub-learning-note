## 描述



### 過度使用wrapper element的解法思路
為了解決以下問題
[[React：過度使用wrapper element來解決JSX侷限問題，會產生兩大問題，第一會破壞CSS選擇器所選擇的節點、第二瀏覽器會渲染出不必要出現的HTML元素，甚至會重複渲染]]

可行的解決思路為：
1. 建立一個empty wrapper component，該component會對應著不存在的Virtual DOM結構，亦即為不會產生對應實際DOM 結構
2. 由empty wrapper component來包含原有要用真的wrapper包起來的子節點

### Wrapper.js 打造一個empty wrapper component

empty wrapper component實際上會只內含著它所包含的子節點內容，不會有額外的元件來包含子節點內容，只要使用wrapper，就只會回傳它的子節點。

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
製作empty wrapper component是：
1. 憑藉著wrapper轉換語法是合法而對應不到DOM節點
2. wrapper單純包含子節點來回傳所有子節點
3. [[特定元件A的 props.children 會是以placeholder的形式來表示元件A所包含的內容，並等到內容確定就將內容覆蓋至placeholder，並不會以react element 或者JSX看待它們]]


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

使用empty parent element來充當wrapper component，並不會讓section和card元件多一個div元件
![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1662745520/blog/frontend/conditional-rendering/after-wrapper_qieupz.png)

## 複習

#🧠 React：為了解決過度使用wrapper element來解決JSX 侷限問題，在這裡的解法思路是什麼？ ->->-> `1. 建立一個empty wrapper component，該component會對應著不存在的Virtual DOM結構，亦即為不會產生對應實際DOM 結構 2. 由empty wrapper component來包含原有要用真的wrapper包起來的子節點`
<!--SR:!2023-07-16,194,250-->


#🧠 React：請寫程式碼來說明如何製作empty wrapper component和使用他們，使該component本身會對應不存在的Virtaul DOM結構以及對應不到實際DOM結構，但可以夾帶著其他內容 ->->-> ![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1662815861/blog/react/react-element/wrapper-for-div-hell/fake-wrapper-component-constructor_hlbw9x.png) ![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1662815861/blog/react/react-element/wrapper-for-div-hell/fake-wrapper-component-usage_gb9sqf.png)
<!--SR:!2024-05-05,244,230-->

#🧠 React：下面是定義如何製作empty wrapper component，請問為何行得通？![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1662815861/blog/react/react-element/wrapper-for-div-hell/fake-wrapper-component-constructor_hlbw9x.png) ![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1662815861/blog/react/react-element/wrapper-for-div-hell/fake-wrapper-component-usage_gb9sqf.png) ->->-> `因為return 那邊的Wrapper 元件和它包含的子元件可以看作為return (React.createElement(Wrapper,{}, React.createElemennt('div',{}....)))`
<!--SR:!2023-12-23,283,250-->

#🧠 React：下面是定義如何製作empty wrapper component，請問為何行得通？盡可能以簡短兩句來說明。![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1662815861/blog/react/react-element/wrapper-for-div-hell/fake-wrapper-component-constructor_hlbw9x.png) ![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1662815861/blog/react/react-element/wrapper-for-div-hell/fake-wrapper-component-usage_gb9sqf.png) ->->-> `1. 憑藉著wrapper轉換語法是合法而對應不到DOM節點 2. wrapper單純包含子節點來回傳所有子節點`
<!--SR:!2023-07-06,187,250-->



#🧠 以下是使用empty wrapper component來解決JSX侷限問題，wrapper component本身並沒有實際的元件，只包含子節點，並且由section來包含以下內容，請問最後的DOM節點會是什麼？![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1662816315/blog/react/react-element/wrapper-for-div-hell/div-hell-solution-with-fake-component_ghxk5y.png) ->->-> `使用empty parent element來充當wrapper component，並不會讓section和card元件多一個div元件![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1662745521/blog/frontend/conditional-rendering/before-wrapper_fbmo12.png)`
<!--SR:!2025-02-01,531,250-->


#🧠 以下是繼續使用真的wrapper component來解決JSX侷限問題，並且由section來包含以下內容，請問最後的DOM節點會是什麼？![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1662816316/blog/react/react-element/wrapper-for-div-hell/div-hell-origin_mcd2hk.png) ->->-> `使用div元件繼續當wrapper component，會在section和card元件之間多一個div![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1662745521/blog/frontend/conditional-rendering/before-wrapper_fbmo12.png)`
<!--SR:!2025-01-19,523,250-->

#🧠 React：製作empty wrapper component 的成功原因為何？ ->->-> `： 1. 憑藉著wrapper轉換語法是合法而對應不到DOM節點 2. wrapper單純包含子節點來回傳所有子節點 3. 特定元件A的 props.children 會是以placeholder的形式來表示元件A所包含的內容，並等到內容確定就將內容覆蓋至placeholder，並不會以react element 或者JSX看待它們`
<!--SR:!2023-06-17,66,250-->





---
Status: #🌱 
Tags:
[[React]]
Links:
[[特定元件A的 props.children 會是以placeholder的形式來表示元件A所包含的內容，並等到內容確定就將內容覆蓋至placeholder，並不會以react element 或者JSX看待它們]]
[[empty wrapper component實質上不會有任何對應Virtual DOM和對應實際DOM節點，憑藉著滿足JSX語法上的侷限-要有一個JSX parent 元件來包含子元件來包含(wrap)多個子元件來一次性回傳多個子元件]]
[[JSX 侷限一定要有parent element包覆其他元素和最外圍的parent element只能有一個，解法有wrapper element、array]]
[[React：過度使用wrapper element來解決JSX侷限問題，會產生兩大問題，第一會破壞CSS選擇器所選擇的節點、第二瀏覽器會渲染出不必要出現的HTML元素，甚至會重複渲染]]
References: