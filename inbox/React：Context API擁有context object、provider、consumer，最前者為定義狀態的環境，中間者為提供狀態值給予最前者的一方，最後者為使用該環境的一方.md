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

![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1663695226/blog/react/context/context-provider-consumer_samqom.png)

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
	- 是一個wrapper component
	- 由於Context Object的具體內容會由Provider component所提供的狀態值，所以它本身可以代表著Context object的component
	- 被它包覆著的Component都允許存取對Context Object(PS. 只是允許，而非真的存取)或者Context Object對於這些子節點是可見的
	- 沒被它包覆著子節點不被允許存取其Context Object
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
	- 每個 擁有provider component的元件都會

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
	- 是一個wrapper component
	- 訂閱/監聽對應context
	- 提供特定方法讓被包含的子節點能夠存取對應的context所擁有的值：
		- 以callback + 第一個引數為context object本身，callback函式內容會是原本JSX元件，context object本身屬性值會是代表著狀態、更新用狀態函式
	```
	<Context.Consumer>
		{(context) => .....}
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
		<AuthContext.Consumer>
			{callback}
		</AuthContext.Consumer>
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
- createContext 建立一個context 物件，會回傳對應context 物件。
- defaultValue 是定義初始狀態為何，形式可以是數字、字串、物件，通常為物件
- 當React 開始渲染一個元件時，而該元件訂閱該context object，則會以讀取離它(Virtual DOM)較近的Provider元件來獲取目前context 內容
- 當如果沒有任何Provider Component，才會將createContext(defaultValue)中的defaultValue設定為目前context object的狀態值


## 複習

#🧠 React：Context 本身是什麼？ ->->-> `目前是定義狀態的環境，具體會是以物件來表示`

#🧠 React：Context 內容是由誰提供？ ->->-> `具體會是以物件來表示，其內容主要會由Provider或者預設狀態來提供`

#🧠 React：Context中的Provider 是什麼？ ->->-> `是一個Component，負責提供特定狀態值至Context Object`

#🧠 React：Context中的Provider 是負責提供特定狀態值至Context Object的Component，請問該Component會更新Context嗎？ 為什麼？->->-> `不會，因為Provider Component本身只是單方面提供值來設定對應Context`

#🧠 React：Context中的Consumer 是什麼？  ->->-> `是一個Component 負責向Context Object訂閱/監聽並存取Context Object上的狀態值`

#🧠 React：Context Object的屬性與provider、consumer有什麼關聯？ ->->-> `每個Context object都擁有對應的Provider、Consumer屬性`

#🧠 React：Context、provider component、consumer component 三者間的關係為何？(誰擁有誰)->->-> `每種Context 都各有provider component 來設定自己的Context當前內容以及consumer component來給特定元件存取Context`

#🧠 React：Context、provider component、consumer component 三者間的關係為何？->->-> `每種Context 都各有provider component 來設定自己的Context當前內容以及consumer component來給特定元件存取Context`

#🧠 React：Context中的Provider 具體是什麼Component？->->-> `wrapper component`


#🧠 React：Context中的Provider 具體是wrapper component，那麼被它包覆著的Component會擁有什麼特性？ 還是就只是包覆而已？ ->->-> `被它包覆著的Component都允許存取其Context Object(PS. 只是允許，而非真的存取)或者Context Object對於這些子節點是可見的`

#🧠 React：Context中的Provider 具體是wrapper component，那麼被它包覆著的Component會擁有允許存取對Context Object？允許可以代表可直接存取嗎 ->->-> `並不能`


#🧠 React：Context中的Provider Component 用途是什麼？ ->->-> `將自己所提供的狀態值設定在對應的Context上`

#🧠 React：Context中的Provider Component 用途是將自己所提供的狀態值設定在對應的Context上，那麼具體設定流程為何？ ->->-> `1. 載入想存取狀態的Context import XXXContext from '....' 2. 利用XXXContext的Provider屬性來獲取對應Context之provider component包裹的元件，並指定value來設定目前Context的內容為一個裝載有state1屬性的物件，並讓後面的子節點可存取目前狀態值的Context <XXXContext.Provider value={{ state1: value1 }}> ... </XXXContext.Provider>`

#🧠 React：Context中的Provider Component 所擁有的value props是做什麼用的？ ->->-> `用以設定對應Context的狀態值`

#🧠 React：Context中的Provider Component 所擁有的value props是用以設定對應Context的狀態值，那麼value會填入什麼內容 ->->-> `內容會由useState或者useReducer所回傳的狀態值snapshot以及更新狀態用的函式`


#🧠 React：Context中的Provider Component 所擁有的value props是用以設定對應Context的狀態值，那麼value會填入useState或者useReducer所回傳的狀態值snapshot以及更新狀態用的函式，為什麼是這些？ ->->-> `保證每次渲染都依照互動狀態而得到不同的渲染畫面`


#🧠 Question :: ->->-> ``

#🧠 Question :: ->->-> ``

#🧠 Question :: ->->-> ``

#🧠 Question :: ->->-> ``

#🧠 Question :: ->->-> ``

#🧠 Question :: ->->-> ``

#🧠 Question :: ->->-> ``

#🧠 Question :: ->->-> ``



---
Status: #🌱 #📓 
Tags:
[[React]]
Links:
References: