## 描述

### 文獻
[[@reactUsingEffectHook]]
> **When exactly does React clean up an effect?** React performs the cleanup when the component unmounts

> If you want to run an effect and clean it up only once (on mount and unmount), you can pass an empty array (`[]`) as a second argument. This tells React that your effect doesn’t depend on _any_ values from props or state, so it never needs to re-run. This isn’t handled as a special case — it follows directly from how the dependencies array always works.

[[@heidi-liuWeek21Reacta]]
> Hook 執行流程可分為三個部分：
>
> -   Mount：把 component 放到畫面上
> -   Update：更新 state 流程
>-   Unmount：清除 effect


> ### cleanup function 執行時機
> 結合上述範例，cleanup function 執行的時間點有兩個：
> 
> -   要執行下一個 useEffect 的時候，要先清除上一個 effect
> -   component unmount 的時候，會清除 effect


重點：
- 從片面可得知，每當元件發生unmount就會執行cleanup：但不能夠確定只是執行cleanup
- 從片面可得知，unmount會和mount不管dependency是什麼，都會執行
- useEffect：cleanup function執行時機：
	- 執行下一個useEffect之前，會執行effect cleanup
	- component 被 unmount前，會執行effect cleanup
### 實驗 (不建議參考)

Container.js：分為Container和Child這兩個元件，前者是用class component來撰寫，後者則是用function component，Container元件包含著Child元件，當對Container元件上的按鈕進行點擊時，就會unmount Child元件，這時就會觸發Child 元件的componentWillUnmount週期函式，或者由useEffect來幫忙處理，在這裡還特定替useEffect 添加空陣列做為dependency，來觀察說是不是只有mount才會直接執行
```
import React, { useEffect } from 'react';
import ReactDOM from 'react-dom/client';

class Container extends React.Component {
  constructor(props) {
    super(props);
    this.state = { show: true };
  }
  delHeader = () => {
    this.setState({ show: false });
  };
  render() {
    let myheader;
    if (this.state.show) {
      myheader = <Child />;
    }
    return (
      <div>
        {myheader}
        <button type='button' onClick={this.delHeader}>
          Delete Header
        </button>
      </div>
    );
  }
}

function Child(props) {
  let test = 1
  useEffect(() => {
	alert('trigger effect');
    return () => {
      console.log('cleanup');
    };
  }, []);
  
  return <h1>Hello World!</h1>;
}

export default Container;
```

以及將dependency去掉：
```
function Child(props) {
  let test = 1
  useEffect(() => {
	alert('trigger effect');
    return () => {
      console.log('cleanup');
    };
  });
```

結果：
- 理論上，當Child元件發生unmount就會觸發effect，並檢查dependency是否變動，有變動才會執行useEffect(callback)中的callback，在這裡分別設定[]和去掉dependency，所以預期的話，[]不會執行，去掉dependency的話則是會執行
- 實際上，無論dependency是什麼，它都不是執行useEffect(callback)的callback，而是去執行useEffect的cleanup 函式


### 總結
當元件上註冊了useEffect並觸發unmount時，無論dependency是什麼，都會執行cleanup，而非side effect，目的是為了移除上一次side effect所造成的影響



## 複習

#🧠 React：useEffect cleanup function 執行時機是什麼？ ->->-> `updating：執行下一個useEffect前，會執行cleanup。unmounting：component被unmount前，會執行effect cleanup`
<!--SR:!2024-05-28,341,250-->

#🧠 React：useEffect 在unmount 時真是會執行componentWillUnmount?  ->->-> `並沒有，只是單方面會額外執行cleanup`
<!--SR:!2023-09-13,194,250-->

#🧠 當元件上註冊了useEffect並觸發unmount時，只會執行useEffect的什麼？為什麼？ ->->-> `會在元件完全被unmount前執行cleanup來清除掉多餘的side effect`
<!--SR:!2023-11-10,87,230-->


#🧠 若設定dependency為空陣列的話，當元件上註冊了useEffect並觸發unmount上時，只會執行useEffect的什麼？ 為什麼？->->-> `它不會管dependency是什麼，都會在元件完全被unmount前執行cleanup來清除掉多餘的side effect`
<!--SR:!2023-06-29,144,250-->


#🧠 若設定dependency為空陣列的話，當元件上註冊了useEffect並觸發unmount上時，會執行useEffect的side effect實現代碼嗎？為什麼？ ->->-> `不會，因為只會無條件執行cleanup function`
<!--SR:!2023-11-21,86,230-->



#🧠 若設定dependency為空陣列的話，元件上註冊了useEffect並觸發unmount上時，還是會執行useEffect的cleanup，為什麼？ ->->-> `它不會管dependency是什麼，都會在元件完全被unmount前執行cleanup`
<!--SR:!2023-09-13,194,250-->


#🧠 若設定dependency為沒東西的話，當元件上註冊了useEffect並觸發unmount時，只會執行useEffect的什麼？ 為什麼？ ->->-> `它不會管dependency是什麼，都會在元件完全被unmount前執行cleanup來清除掉多餘的side effect`
<!--SR:!2023-09-11,192,250-->


#🧠 若設定dependency為狀態的話，當元件上註冊了useEffect並觸發unmount上時，只會執行useEffect的什麼？ 為什麼？ ->->-> `它不會管dependency是什麼，都會在元件完全被unmount前執行cleanup來清除掉多餘的side effect`
<!--SR:!2023-09-13,194,250-->


---
Status: #🌱 
Tags:
[[React]] - [[useEffect]]
Links:
[[React：Effect 等同於 Side Effect，effect 本身是指執行主要處理(結果)所帶來的任意額外處理(結果)，主要處理(結果)會是指元件渲染(render)任務。任意額外處理(結果)指useEffect所定義的執行處理]]
[[side effect 是指調用者執行特定操作或表達式或函式而得到除了回傳值給調用者這個主要效果以外的額外效果，side effect 通常會是影響主調用者所使用的共享資源之效果]]

[[React：useEffect cleanup 技術主要是停止當前side effect所產生的非同步任務]]
[[React：useEffect 使用方式是替當前元件註冊effect這個hook並於每個渲染階段下來判定是否能執行side effect]]
[[React：useEffect & Dependencies 之間關係就在於每一次在updating階段時effect被觸發時會檢查是否有任一dependency有改變而執行對應的callback]]
References:
[[@reactUsingEffectHook]]
[[@heidi-liuWeek21Reacta]]