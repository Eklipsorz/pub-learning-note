## 描述


### JSX Limitations
1. 一定要有最外圍的parent element包覆其他元素
2. 最外圍的parent element只能有一個

one element which you are allowed to have may of course have more children which then also can be adjacent to each other


### 問題描述
```
return (
	<Element1 />
	<Element2 />
)
```

由於每個JSX 元素會轉換成以下語法：
```
// 轉換前
<Element1 />
or 
<Element1>...</Element1>

// 轉換後
React.createElement(Element1, {}, ...)
```

進而讓以下語法
```
(
	<Element1 />
	<Element2 />
)
```

轉換成
```
(
	React.createElement(Element1, {}, ...)
	React.createElement(Element2, {}, ...)
)
```

最後，搭配最外面的return，就會是
```
return (
	React.createElement(Element1, {}, ...)
	React.createElement(Element2, {}, ...)
)
```

但return 只能回傳一個Element來建立，但依照現況來從Element1 和 Element2 中選擇一個來建立，甚至不選，都不會滿足JSX在表面上所提示的那樣，要一次回傳多個Element。所以才要開發者要有一個元素來包含所有元素、且最外圍的parent element只能一個


### 解法

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
```
return (
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
  );
```



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


#🧠 JSX 語法侷限有什麼？  ->->-> `一定要有最外圍的parent element包覆其他元素、最外圍的parent element只能有一個`
<!--SR:!2023-07-13,191,250-->



#🧠 以下是JSX語法，系統會自動解析成什麼？請用程式碼表示 ![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1662810542/blog/react/react-element/JSX-React-Simple-Example_irtno2.png) ->->-> `return (React.createElement(Element1, {}, ...) React.createElement(Element2, {}, ...))`
<!--SR:!2023-07-05,186,250-->


#🧠 每個JSX元素語法-\<Element1\>.... \<\/Element1\>被React看作是？以程式碼來表示 ->->-> `React.createElement(Element1, {...}, ....)`
<!--SR:!2023-12-02,270,250-->


#🧠 每個JSX元素語法-\<Element1\>.... \<\/Element1\>被React看作是？以文字來描述 ->->-> `被看作以React函式庫的createElement語法來建立對應元件。`
<!--SR:!2023-12-09,275,250-->

#🧠 請用這例子來說明JSX語法侷限會是**一定要有最外圍的parent element包覆其他元素、最外圍的parent element只能有一個** ？![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1662810542/blog/react/react-element/JSX-React-Simple-Example_irtno2.png) ->->-> `return 只能回傳一個Element來建立，但依照現況來從Element1 和 Element2 中選擇一個來建立，甚至不選，都不會滿足JSX在表面上所提示的那樣，要一次回傳多個Element。所以才要開發者要有一個元素來包含所有元素、且最外圍的parent element只能一個`
<!--SR:!2023-11-28,159,230-->


#🧠 面對JSX 局限性問題，會有什麼方法來解決？(先不論portal 和 fragment) ->->-> `使用額外的元件來當wrapper element、利用React解析陣列的特性來使用陣列表示`
<!--SR:!2023-11-17,74,210-->


#🧠 面對JSX 局限性問題，會有什麼方法來解決？其中若選擇使用利用React解析陣列的特性來使用陣列表示，還會遇到什麼潛在問題？ 遇到該如何解決->->-> `可能會遇到Each child in a list should have a unique "key" prop 這訊息，要解決的話，要對陣列的每個項目添加key屬性`
<!--SR:!2023-07-14,192,250-->

#🧠 以下程式碼能夠正常執行嗎？不能的話，會是什麼問題？解決思維為何？![https://res.cloudinary.com/dqfxgtyoi/image/upload/v1662812594/blog/react/react-element/JSX-limitations-problem_s9prey.png](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1662812594/blog/react/react-element/JSX-limitations-problem_s9prey.png) ->->-> `不能夠執行、最主要是沒有額外的parent element來包覆著ErrorModal和Card這兩個元件，解決思維則是建立一個新的parent element來包覆著、使用陣列來將他們包含`
<!--SR:!2023-12-24,127,190-->





#🧠 以下程式碼犯下了JSX 侷限問題，請用程式碼來表示如何用陣列來包含以其解決![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1662821675/blog/react/react-element/wrapper-for-div-hell/JSX-Limitations-origin-problem_i4bibx.png) ->->-> `![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1662812594/blog/react/react-element/JSX-limitations-solution2_jzylbh.png)`
<!--SR:!2023-06-03,162,250-->


#🧠 以下程式碼犯下了JSX 侷限問題，請用程式碼來表示如何用陣列來包含以其解決，為何陣列中的第一個項目可以被放進去？![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1662812594/blog/react/react-element/JSX-limitations-solution2_jzylbh.png) ->->-> `boolean expression && JSX Element 可以被當作一種JSX元素，只有前者為true，才以後者的JSX Element為主，若前者為false，就會被React給忽略。`
<!--SR:!2023-07-16,194,250-->


---
Status: #🌱 
Tags:
[[React]]
Links:
[[渲染部分{expression}中的expression是指陣列的話，React 會直接將陣列上的每個元素當成react element 來並排當作渲染內容]]
[[React：Keys概念是用特定資料的識別字去對應著特定Virtual DOM節點，以此在變更內容的情況下，好讓React能夠分辨哪個實際DOM節點是隸屬於哪個資料]]
[[Each child in a list should have a unique "key" prop. 表示開發者有使用陣列來表示多個JSX Elemenet ，在這裡系統會建議開發者替陣列的每個項目增加key屬性以確保每個項目都能對應到DOM節點]]
[[React 解析boolean expression && JSX element  時，若前者為true，就以後者的JSX element為主，否則就忽略該Virtual DOM]]
[[在渲染層面下，render 函式回傳的內容若單純添加boolean expression && JSX element 的話，會使其語法正常執行，反之在其基礎下添加其他元素的話，其語法會被視為字串和一般的React Element來看待]]
References: