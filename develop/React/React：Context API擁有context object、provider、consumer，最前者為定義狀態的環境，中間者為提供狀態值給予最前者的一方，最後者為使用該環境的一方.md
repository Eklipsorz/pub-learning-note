## 描述

### provider vs. consumer vs. context 角色
[[@ithomeWantKnowReacta]]
> ### Context 角色

> React context 的使用會環繞三個角色在運作：
>
> -   Context Object
> -   Provider
> -   Consumer

> 一個 React app 中可以有多個 React context。每個 React context 的本體都是一個物件（在這邊把它稱為 context object）。其中 context object 中又會有兩個很重要的屬性：Provider（提供者）與 Consumer（消費者）。
>
> -   Provider（提供者）的功用就是用來**提供** context 值。
> -   Consumer（消費者）的功用則是用來**使用** context 值。

![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1665139517/blog/react/context/context-provider-consumer_o2zh2p.png)

重點：
- Context Object：目前是定義狀態的環境，內容主要會由Provider或者預設狀態來提供
- Provider：負責提供特定狀態值至Context Object，這裡的提供是單方面提供，並不會更新狀態值
- Consumer：負責向Context Object訂閱/監聽並存取Context Object上的狀態值


### Provider component
[[@reactContextReact]]

> ### `Context.Provider`

```
<MyContext.Provider value={/* some value */}>
```

> Every Context object comes with a Provider React component that allows consuming components to subscribe to context changes.

> The Provider component accepts a `value` prop to be passed to consuming components that are descendants of this Provider. One Provider can be connected to many consumers. Providers can be nested to override values deeper within the tree.

重點：
1. 每個 context object 都會有 provider component ：
	- 是一個wrapper component，如同正常的component擁有狀態、props、hook、生命週期函式
	- 用途：
		- 由於Context Object的具體內容會由Provider component所提供的狀態值，所以它本身可以代表著Context object的component
		- 被它包覆著的Component都允許可見到它對於Context Object的設定內容(PS. 只是允許，而非真的存取)
	- 沒被它包覆著子節點不被允許存取它對於其Context Object的設定內容，以其他Provider component設定的內容或者預設值為主
2. 使用方式
	- 載入想存取狀態的Context 
	```
	import XXXContext from '....'
	```
	- 利用XXXContext的Provider屬性來獲取對應Context之provider component包裹的元件，並指定value來設定目前Context的內容為一個裝載有state1屬性的物件，並讓後面的子節點可存取目前狀態值的Context
	```
	<XXXContext.Provider value={{ state1: value1 }}>
		.....
	</XXXContext.Provider>
	```
	- 通常value屬性(attribute)會設定的內容會由useState或者useReducer所回傳的狀態值snapshot以及更新狀態用的函式，依此來保證每次渲染都依照互動狀態而得到不同的渲染畫面
3. 細節：
	- 每個 context object 都可以擁有多個Provider component


#### 案例：Provider Component


provider component
```
  return (
    <AuthContext.Provider
      value={{
        isLoggedin: isLoggedIn,
      }}
    >
      <MainHeader isAuthenticated={isLoggedIn} onLogout={logoutHandler} />
      <main>
        {!isLoggedIn && <Login onLogin={loginHandler} />}
        {isLoggedIn && <Home onLogout={logoutHandler} />}
      </main>
    </AuthContext.Provider>
  );
```




### Consumer component
> Context.Consumer

```
<MyContext.Consumer>
  {value => /* render something based on the context value */}
</MyContext.Consumer>
```
> A React component that subscribes to context changes. Using this component lets you subscribe to a context within a function component.


> Requires a [function as a child](https://zh-hant.reactjs.org/docs/render-props.html#using-props-other-than-render). The function receives the current context value and returns a React node.

重點：
1. 每個 context object 都會有consumer component：
	- 是一個wrapper component，如同正常的component擁有狀態、props、hook、生命週期函式
	- 訂閱/監聽對應context的目前值，具體會是等到搭載consumer component的元件被觸發渲染才會去監聽context object 內容
	[[consumer component 並不會主動監測，只會等到搭載consumer component的元件被觸發渲染並監測內容是否有變動，有變動就把使用該內容的元件跟著一起渲染更新，沒變動就不動]]
	- 提供特定方法讓被包含的元件能夠存取對應的context所擁有的值：
		- 以 {}+ callback + 第一個引數為context object的value本身，callback函式內容會是原本JSX元件，context object本身屬性值會是代表著狀態、更新用狀態函式
	```
	<Context.Consumer>
		{(value) => .....}
	</Context.Consumer>
	```
2. 使用方式為：
	- 載入想存取狀態的Context 
   ```
	import XXXContext from '....'
   ```
	- 利用對應Context的consumer屬性來獲取對應Comsumer Component來包裹一個{callback}
	```
	return (
		<XXXContext.Consumer>
			{callback}
		</XXXContext.Consumer>
	);
	```
	- {callback} 形式會是(ctx) => {} ，引數為對應Context的Provider Component所提供的value數性(attribute)，並且會回傳對應React Virtual DOM
	```
	return (
		<AuthContext.Consumer>
			{(ctx) => { /*...*/ return react-element; }}
		</AuthContext.Consumer>
	);
	```
3. 細節：
	- 每個 context object 都可以擁有多個Consumer component
	- 每個 擁有consumer component 的元件都被稱之為consuming component，換言之，該元件直接存取context object的狀態值


#### 案例：Consumer component
```
const Navigation = (props) => {
  return (
    <AuthContext.Consumer>
      {(ctx) => {
        return (
          <nav className={classes.nav}>
            <ul>
              {ctx.isLoggedIn && (
                <li>
                  <a href='/'>Users</a>
                </li>
              )}
              {ctx.isLoggedIn && (
                <li>
                  <a href='/'>Admin</a>
                </li>
              )}
              {ctx.isLoggedIn && (
                <li>
                  <button onClick={props.onLogout}>Logout</button>
                </li>
              )}
            </ul>
          </nav>
        );
      }}
    </AuthContext.Consumer>
  );
};

```

### Context object


> Context is itself is not a component
  
[[@reactContextReact]]
const MyContext = React.createContext(defaultValue);

> Creates a Context object. When React renders a component that subscribes to this Context object it will read the current context value from the closest matching `Provider` above it in the tree.

> The `defaultValue` argument is **only** used when a component does not have a matching Provider above it in the tree. This default value can be helpful for testing components in isolation without wrapping them.
  
重點：
- createContext 建立一個context 物件
- 語法為：
	- defaultValue 是定義初始狀態為何，形式可以是數字、字串、物件，通常為物件
	- 回傳對應context 物件。
```
const MyContext = React.createContext(defaultValue);
```
- 當React 開始渲染一個元件時，而該元件訂閱該context object，則會以讀取離它(Virtual DOM)較近的Provider元件來獲取目前context 內容
- 當如果沒有任何Provider Component，才會將createContext(defaultValue)中的defaultValue設定為目前context object的狀態值

### 命名緣由
[[@wikidataProducerConsumerProblem2022]]
> # Producer–consumer problem
> Dijkstra wrote about the unbounded buffer case: "We consider two processes, which are called the 'producer' and the 'consumer' respectively. The producer is a cyclic process and each time it goes through its cycle it produces a certain portion of information, that has to be processed by the consumer.

> 該問題描述了共享固定大小緩衝區的兩個進程——即所謂的「生產者」和「消費者」——在實際運行時會發生的問題。生產者的主要作用是生成一定量的數據放到緩衝區中，然後重複此過程。與此同時，消費者也在緩衝區消耗這些數據。該問題的關鍵就是要保證生產者不會在緩衝區滿時加入數據，消費者也不會在緩衝區中空時消耗數據。



provider：
> a person or thing that provides


consumer：
> a person or thing that consumes

consume
> to use fuel, energy, or time, especially in large amounts

重點：
- provider 指的是提供某些東西至某處的人事物
- consumer 指的是使用特定資源並消耗掉的人事物
- 在電腦科學裡，provider 和 consumer 源自於 provider-consumer problem / producer-consumer problem 問題：
	- 背景是：兩個Process共享同一個固定大小緩存區，其中一個專門生成資料並放入緩存區的process被稱之為provider/producer，而專門從緩存中取出資料並從緩存區移除(消耗)的process被稱之為consumer
	- 這問題案例主要用作於多個process在面向同一個資源時是如何運作



## 複習

#🧠 provider 命名緣由為何？ ->->-> `是提供某些東西至某處的人事物`
<!--SR:!2025-01-30,529,250-->

#🧠 consumer 命名緣由為何？ ->->-> `是使用特定資源並消耗掉的人事物`
<!--SR:!2024-04-25,350,250-->

#🧠  React：context 的 provider component 會如同正常component擁有什麼 ->->-> `狀態、hook、props`
<!--SR:!2023-12-31,277,248-->

#🧠 React：context 的 consumer component 會如同正常component擁有什麼 ->->->  `狀態、hook、props、`
<!--SR:!2024-01-11,284,248-->



#🧠 provider-consumer problem / producer-consumer problem 套用在Context 、Provider、Consumer就會是什麼？畫張圖表示一下->->-> `![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1665139517/blog/react/context/context-provider-consumer_o2zh2p.png)`
<!--SR:!2023-07-26,193,250-->

#🧠 React：Context 本身是什麼？ ->->-> `目前是定義狀態的環境，具體會是以物件來表示`
<!--SR:!2024-03-08,252,230-->

#🧠 React：Context 內容是由誰提供？ ->->-> `具體會是以物件來表示，其內容主要會由Provider或者預設狀態來提供`
<!--SR:!2025-01-29,531,250-->

#🧠 React：Context中的Provider 是什麼？ ->->-> `是一個Component，負責提供特定狀態值至Context Object`
<!--SR:!2024-08-27,427,250-->


#🧠 React：Context中的Provider component用途是什麼？->->-> `- 由於Context Object的具體內容會由Provider component所提供的狀態值，所以它本身可以代表著Context object的component - 被它包覆著的Component都允許可見到它對於Context Object的設定內容(PS. 只是允許，而非真的存取)`
<!--SR:!2023-12-04,258,248-->

#🧠 React：若沒被任意Provider component包覆著的元件想使用context object會獲取什麼內容->->-> `會存取到context object的預設值`
<!--SR:!2023-12-05,100,228-->

#🧠  React：若沒被Provider component A包覆著但被Provider component B包覆的元件想使用context object會獲取什麼內容 ->->-> `Provider component B對於context object所設定的內容`
<!--SR:!2023-10-06,221,248-->

#🧠 React：Context中的Provider 是負責提供特定狀態值至Context Object的Component，請問該Component會更新Context嗎？ 為什麼？->->-> `不會，因為Provider Component本身只是單方面提供值來設定對應Context`
<!--SR:!2023-05-20,146,250-->

#🧠 React：Context中的Consumer 是什麼？(提示：聽一下，獲取一下)  ->->-> `是一個Component，負責向Context Object訂閱/監聽並存取Context Object上的狀態值`
<!--SR:!2024-10-24,436,230-->

#🧠 React：Context中的Consumer 是一個Component，負責向Context Object訂閱/監聽並存取Context Object上的狀態值，具體會如何監聽？會不會主動監聽？  ->->-> `不會，只會等到搭載consumer component 的元件被觸發渲染才開始讓consumer去監聽context object 內容是否有變動`
<!--SR:!2023-10-18,228,248-->


#🧠 React：Context中的Consumer 是什麼？  ->->-> `是一個Component，負責向Context Object訂閱/監聽並存取Context Object上的狀態值`
<!--SR:!2023-12-20,115,150-->

#🧠 React：Context Object的屬性與provider、consumer有什麼關聯？ ->->-> `每個Context object都擁有對應的Provider、Consumer屬性`
<!--SR:!2025-01-04,508,250-->

#🧠 React：Context、provider component、consumer component 三者間的關係為何？(誰擁有誰)->->-> `每種Context 都各有provider component 來設定自己的Context當前內容以及consumer component來給特定元件存取Context`
<!--SR:!2023-12-06,93,230-->

#🧠 React：Context、provider component、consumer component 三者間的關係為何？->->-> `每種Context 都各有provider component 來設定自己的Context當前內容以及consumer component來給特定元件存取Context`
<!--SR:!2023-07-25,192,250-->

#🧠 React：Context中的Provider 在形式上是什麼Component？->->-> `wrapper component`
<!--SR:!2023-10-18,36,249-->



#🧠 React：Context中的Provider 具體是wrapper component，那麼被它包覆著的Component會擁有什麼特性？ 還是就只是包覆而已？ ->->-> `		- 被它包覆著的Component都允許可見到它對於Context Object的設定內容(PS. 只是允許，而非真的存取)`
<!--SR:!2023-11-13,243,248-->


#🧠  React：Context中的Provider 具體是wrapper component，那麼沒被它包覆著的Component 與被包覆著的元件之間的差別是？ ->->-> `	- 沒被它包覆著子節點不被允許存取它對於其Context Object的設定內容，以其他Provider component設定的內容或者預設值為主`
<!--SR:!2023-12-28,273,248-->


#🧠 React：Context中的Provider 具體是wrapper component，那麼被它包覆著的Component會擁有允許存取對Context Object？允許可以代表可直接存取嗎 ->->-> `並不能`
<!--SR:!2025-01-21,518,250-->


#🧠 React：Context中的Provider Component 用途是什麼？ ->->-> `將自己所提供的狀態值設定在對應的Context上、讓被包覆的元件能夠看得見該provider component對於context object的內容`
<!--SR:!2023-09-25,216,248-->


#🧠 React：Context中的Provider Component 用途是將自己所提供的狀態值設定在對應的Context上，那麼具體設定流程為何？ ->->-> `1. 載入想存取狀態的Context import XXXContext from '....' 2. 利用XXXContext的Provider屬性來獲取對應Context之provider component包裹的元件，並指定value來設定目前Context的內容為一個裝載有state1屬性的物件，並讓後面的子節點可存取目前狀態值的Context <XXXContext.Provider value={{ state1: value1 }}> ... </XXXContext.Provider>`
<!--SR:!2025-01-23,527,250-->

#🧠 React：Context中的Provider Component 所擁有的value props是做什麼用的？ ->->-> `用以設定對應Context的狀態值`
<!--SR:!2023-07-20,189,250-->

#🧠 React：Context中的Provider Component 所擁有的value props是用以設定對應Context的狀態值，那麼為了能用React體系的狀態，通常value會填入什麼內容->->-> `內容會由useState或者useReducer所回傳的狀態值snapshot以及更新狀態用的函式`
<!--SR:!2023-05-25,150,250-->

#🧠 React：Context中的Provider Component 所擁有的value props是用以設定對應Context的狀態值，那麼value會填入什麼內容 ->->-> `內容會由useState或者useReducer所回傳的狀態值snapshot以及更新狀態用的函式`
<!--SR:!2025-02-14,529,248-->



#🧠 React：Context中的Provider Component 所擁有的value props是用以設定對應Context的狀態值，那麼value會填入useState或者useReducer所回傳的狀態值snapshot以及更新狀態用的函式，為什麼是這些？ ->->-> `保證每次渲染都依照互動狀態而得到不同的渲染畫面`
<!--SR:!2023-09-21,210,230-->


#🧠 React：context object 只能有一個Provider component 嗎？ ->->-> `每個 context object 都可以擁有多個Provider component`
<!--SR:!2025-02-01,524,250-->

#🧠 React：context object 的 consumer 具體是什麼component，以元件結構本來說，而非用途->->-> `wrapper component`
<!--SR:!2023-05-10,83,230-->

#🧠 React Context：consumer component用途是什麼？ ->->-> `訂閱/監聽對應context的值的值、提供特定方法讓被包含的元件能夠存取對應的context所擁有的值`
<!--SR:!2023-10-29,214,230-->

#🧠 React Context：consumer component 如何提供特定方法讓被包含的元件能夠存取對應的context所擁有的值？ ->->-> `	- 以 {}+ callback + 第一個引數為context object本身，callback函式內容會是原本JSX元件，context object本身屬性值會是代表著狀態、更新用狀態函式`
<!--SR:!2023-11-28,100,230-->

#🧠 React：consumer component 具體以 {}+ callback + 第一個引數為context object的value本身來提供特定方法讓被包含的元件能夠存取對應的context所擁有的值，那麼具體形式會是如何？ ->->-> `	<Context.Consumer>{(value) => .....}</Context.Consumer>`
<!--SR:!2023-11-17,92,230-->

#🧠  React：	\<Context.Consumer\>\{(value) => .....\}\<\/Context.Consumer\> 中的value 是從哪獲取的？->->-> `基本上會是對應context的provider 所擁有value props，若沒有的話，就是createCreate的預設值`
<!--SR:!2024-05-07,358,250-->

#🧠  React：consumer component 如何存取context的目前所擁有的值？流程和程式碼會是？ ->->-> `載入想存取狀態的Context import XXXContext from '....' 利用對應Context的consumer屬性來獲取對應Comsumer Component來包裹一個{callback} return ( <XXXContext.Consumer> {callback} </XXXContext.Consumer> );`
<!--SR:!2023-10-12,54,210-->

#🧠 React：consuming component 是什麼？具體是什麼？ ->->-> `使用對應Context對應值的component，具體是搭載consumer component來實現。`
<!--SR:!2025-01-26,518,250-->

#🧠 React：每個context object 可以擁有多少個consumer component和provider component ->->-> `可以多個`
<!--SR:!2023-12-24,105,230-->

#🧠 以下是搭載Context的consumer component的component，請問裡頭ctx是指什麼？會回傳什麼？ ![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1663773552/blog/react/context/context-consumer-callback_l1a7xv.png)->->-> `{callback} 形式會是(ctx) => {} ，引數為對應Context的Provider Component所提供的value數性(attribute)，並且會回傳對應React Virtual DOM`
<!--SR:!2023-07-28,194,250-->


#🧠 React：context 是什麼？ ->->-> `專門定義狀態的環境`
<!--SR:!2024-08-09,414,250-->

#🧠 React.createContext(defaultValue); 語法是做什麼？ ->->-> `建立一個context 物件`
<!--SR:!2025-02-15,530,250-->

#🧠 React.createContext(defaultValue); 的defaultValue是用作什麼？ ->->-> `當如果沒有任何Provider Component，才會將createContext(defaultValue)中的defaultValue設定為目前context object的狀態值`
<!--SR:!2024-08-10,415,250-->

#🧠 React：context 如何建立？->->-> `使用createContext 建立一個context 物件，並引入至其他檔案來使用`
<!--SR:!2023-07-27,194,250-->

#🧠 React：若有元件使用consumer 來存取對應context的值且有多個同個context的provider，請問具體來說它是如何存取context？ ->->-> `當React 開始渲染一個元件時，而該元件訂閱該context object，則會以讀取離它(Virtual DOM)較近的Provider元件來獲取目前context 內容`
<!--SR:!2023-07-22,188,250-->

#💻 請使用useContext來讓App的登入狀態能夠共享給MainHeader元件下的Navigation元件，而非使用props chain，檔案在/react-builder/question-review/useContext-question ->->-> `https://github.com/academind/react-complete-guide-code/tree/10-side-effects-reducers-context-api/code/11-making-context-dynamic/src`
<!--SR:!2023-09-27,224,249-->


---
Status: #🌱 
Tags:
[[React]]
Links:
[[consumer component 並不會主動監測，只會等到搭載consumer component的元件被觸發渲染並監測內容是否有變動，有變動就把使用該內容的元件跟著一起渲染更新，沒變動就不動]]
References:
[[@wikidataProducerConsumerProblem2022]]