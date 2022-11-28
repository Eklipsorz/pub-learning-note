## 描述


### 當使用者提交表格並成功時，處理方會有的反應

當使用者提交成功時，會作出以下事情來回應，以下事情可能會重疊。
1. 呈現成功訊息來告知使用者
2. 導向至特定頁面
3. 以modal來告知使用者


### programmatic navigation


> we wanna trigger a navigation action and navigate the user away programmatically in our code

重點：
- 以編碼的方式來從目前頁面導向至另一個特定頁面，而非透過目前頁面的特定元件
- 手段通常會是使用history API或者操縱history的API

### useHistory 

[[@react-routerReactRouterDeclarativea]]
> The `useHistory` hook gives you access to the `history` instance that you may use to navigate.

  

useHistory：
1. 由react-router-dom所提供的hook
2. 專門回傳一個history 物件，該物件由另一個第三方而製成的history 物件，可藉由它來操縱瀏覽器的瀏覽紀錄。

#### 案例

```
import { useHistory } from 'react-router-dom';
import QuoteForm from '../components/quotes/QuoteForm';

const NewQuote = () => {

  const history = useHistory();

  const addQuote = (data) => {
    console.log('addQuote', data);
    history.push('/quotes')
  };
  // display a form for adding a quote
  return <QuoteForm onAddQuote={addQuote} />;
};

export default NewQuote;
```


### 在react-router-dom上的 history object

[[@react-routerReactRouterDeclarativea]]
>  The term “history” and "history object" in this documentation refers to the history package

[[@react-routerReactRouterDeclarativea]]
> The following terms are also used:


> The following terms are also used:
> -   “browser history” - A DOM-specific implementation, useful in web browsers that support the HTML5 history API
> -   “hash history” - A DOM-specific implementation for legacy web browsers
> -   “memory history” - An in-memory history implementation, useful in testing and non-DOM environments like React Native

> `history` objects typically have the following properties and methods:

> -   `push(path, [state])` - (function) Pushes a new entry onto the history stack
> -   `replace(path, [state])` - (function) Replaces the current entry on the history stack

重點：
- react-router-dom 上所能用的history 會是由其他第三方所提供的介面，專門操縱使用者在瀏覽器的瀏覽紀錄
- react-router-dom 所提供的 history 物件實際上是使用以下三者之一的API
	- browser history ：DOM API 提供開發者存取browser history的介面
	- hash history
	- memory history
- history 物件擁有的方法為：path 可以是網站內部的位置或者網站外部的位置
	- push：將指定頁面路徑(path)推送至page stack最上面來當作目前頁面的路徑
	```
	history.push(path)
	```
	- replace：將指定頁面取代page stack的最上面來當作目前頁面的路徑
	```
	history.replace(path)
	```
- 其中的path可以是路徑字串或者夾雜路徑資訊的物件
	- 路徑字串
	- 夾雜路徑資訊的物件：包含著代表路徑端點的pathname、代表query string的search屬性
- push vs. replace 差別：
	- 使用stack來調整瀏覽器時，是否可以回到原本的畫面：前者可以；後者不行，由於網址會被取代掉
	- 方式：前者是直接增加網址在最上面；後者則是將網址取代最上面

### browser history 是什麼？
[[@WebBrowsingHistory2022]]
> Web browsing history refers to the list of web pages a user has visited

重點：
- browser history 或者 history 在網頁上是指使用者從過去至現在瀏覽過的網頁清單，每一個網頁會以網址來代表
- history上會是以多個頁面網址所構成的stack，越上面就越是最近瀏覽過的頁面網址，最上面為目前正在瀏覽的網址


## 複習
#🧠 當使用者提交表格並成功時，處理方會做什麼來增加使用者體驗 ->->-> `1. 呈現成功訊息來告知使用者 2. 導向至特定頁面 3. 以modal來告知使用者`
<!--SR:!2022-12-18,23,250-->

#🧠 當使用者提交表格並成功時，處理方會做: 1. 呈現成功訊息來告知使用者 2. 導向至特定頁面 3. 以modal來告知使用者，為何要做？->->-> `增加使用者體驗來提醒使用者`
<!--SR:!2022-12-22,26,250-->


#🧠 programmatic navigation 是什麼？->->-> `以編碼的手段來直接將使用者在一個目前頁面下導向至另一個特定頁面`
<!--SR:!2022-12-21,23,250-->


#🧠 programmatic navigation 是以編碼的手段來直接將使用者導向至特定頁面，手段通常是什麼？ ->->-> `使用history API或者操縱history的API`
<!--SR:!2022-12-26,28,250-->


#🧠 react-router-dom ：useHistory是什麼樣的hook ->->-> `專門回傳一個history 物件，該物件由另一個第三方而製成的history 物件，可藉由它來操縱瀏覽器的瀏覽紀錄`
<!--SR:!2022-12-27,29,250-->

#🧠 useHistory是源自於誰的hook ->->-> `react-router-dom`
<!--SR:!2022-12-26,28,250-->

#🧠 browser history 或者 history 在網頁上是指什麼？ ->->-> `使用者從過去至現在的瀏覽網站清單`
<!--SR:!2022-12-11,17,250-->

#🧠 browser history 或者 history 在網頁上是指使用者從過去至現在瀏覽過的網頁清單，那麼在這清單上，網頁會如何表示 ->->-> `會以網址來表示`
<!--SR:!2022-12-17,22,250-->

#🧠 browser history 或者 history 在網頁上是指使用者從過去至現在瀏覽過的網頁清單，具體會是什麼結構？過去至現在如何表示？ ->->-> `history上會是以多個頁面網址所構成的stack，越上面就越是最近瀏覽過的頁面網址，最上面為目前正在瀏覽的網址`
<!--SR:!2022-12-15,20,250-->

#🧠 在react-router-dom上的 history object會是由誰提供 ->->-> `react-router-dom 上所能用的history 會是由其他第三方所提供的介面`
<!--SR:!2022-11-27,10,250-->

#🧠 在react-router-dom上的 history object會是用做什麼 ->->-> `專門操縱使用者在瀏覽器的瀏覽紀錄`
<!--SR:!2022-12-22,26,250-->

#🧠  react-router-dom 所提供的 history 物件實際上主要是使用哪一種API？ ->->-> `DOM API 提供開發者存取browser history的介面`
<!--SR:!2022-11-30,10,250-->


#🧠 react-router-dom 所提供的 history 物件常見方法有哪些->->-> `push、replace`
<!--SR:!2022-12-21,25,250-->

#🧠 react-router-dom 所提供的 history 物件常見方法有push和replace，其中push會是什麼？ ->->-> `將指定頁面路徑(path)推送至page stack最上面來當作目前頁面的路徑`
<!--SR:!2022-12-27,29,250-->

#🧠 react-router-dom 所提供的 history 物件常見方法有push和replace，其中push用法會是什麼？ ->->-> `history.push(path)`
<!--SR:!2022-12-09,16,250-->


#🧠 react-router-dom 所提供的 history 物件常見方法有push和replace，其中replace會是什麼？ ->->-> `將指定頁面取代page stack的最上面來當作目前頁面的路徑`
<!--SR:!2022-12-11,17,250-->


#🧠 react-router-dom 所提供的 history 物件常見方法有push和replace，其中replace用法會是什麼？ ->->-> `history.replace(path)`
<!--SR:!2022-12-21,25,250-->

#🧠 react-router-dom 所提供的 history 物件常見方法有push和replace:  push vs. replace 差別 (有兩個)->->-> `使用stack來調整瀏覽器時，是否可以回到原本的畫面：前者可以；後者不行，由於網址會被取代掉、方式：前者是直接增加網址在最上面；後者則是將網址取代最上面`
<!--SR:!2022-12-12,18,250-->


#🧠 react-router-dom 所提供的 history 物件常見方法有push和replace:  push vs. replace 差別，對於 使用stack來調整瀏覽器時，是否可以回到原本的畫面來說，會是什麼？ ->->-> `前者可以；後者不行，由於網址會被取代掉`
<!--SR:!2022-12-26,28,250-->


#🧠 react-router-dom 所提供的 history 物件常見方法有push和replace:  push vs. replace 差別，對於 使用stack的方式： ->->-> `前者是直接增加網址在最上面；後者則是將網址取代最上面`
<!--SR:!2022-12-21,25,250-->

#🧠 react-router-dom 所提供的 history 物件 對於path可以是什麼頁面？ ->->-> `path 可以是網站內部的位置或者網站外部的位置`
<!--SR:!2022-12-14,20,250-->

#💻 請到/githubRepo/react-builder/question-review/react-router-question領取題目並切換至build-programmatic-navigation分支，在那請以programmatic navigation來實作成功提交新增quote會有的導向 ->->-> `https://github.com/academind/react-complete-guide-code/tree/20-building-mpas-with-react-router/code/16-implementing-programmatic-navigation`
<!--SR:!2022-12-25,28,250-->

#🧠 react-router-dom所提供的history物件：push方法和replace方法會用到的path會是什麼型別？ ->->-> `字串、物件`
<!--SR:!2022-12-08,10,250-->

#🧠 react-router-dom所提供的history物件：push方法和replace方法會用到的path會是字串、物件型別，其中字串是什麼？具體是 ->->-> `具體會是由URL構成的字串`
<!--SR:!2022-12-06,8,250-->

#🧠 react-router-dom所提供的history物件：push方法和replace方法會用到的path會是字串、物件型別，其中物件是什麼？具體是夾雜什麼屬性的型別 ->->-> `具體會是夾雜路徑資訊的物件，包含著代表路徑端點的pathname、代表query string的search屬性`
<!--SR:!2022-12-06,8,250-->

#🧠 react-router-dom所提供的history物件：push方法和replace方法會用到的path會是字串、物件型別，其中物件夾雜著pathname和search這兩個屬性，他們各是什麼？ ->->-> `代表路徑端點的pathname、代表query string的search屬性`
<!--SR:!2022-12-09,11,250-->


---
Status: #🌱 
Tags:
[[React]]
Links:
[[navigation 是網頁用來幫助使用者在一個頁面下被該頁面下的元件導向其他頁面的區塊，具體區塊內會含有多個hyperlink給予使用者做互動來導向]]
References:
[[@WebBrowsingHistory2022]]
[[@react-routerReactRouterDeclarativea]]