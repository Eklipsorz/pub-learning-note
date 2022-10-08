## 描述


### 每一次經由useCallback 所得到的函式物件所擁有的closure

由於useCallback 回傳的函式是函式物件，所以會擁有closure概念，每個函式物件會透過closure來對應特定執行時間點下的渲染函式所產生出來的記憶體區塊


### useCallback(baseFunction, [deps]) 的 deps 用途為何
deps 主要解決：
	- useCallback 只會回傳擁有特定時機下之closure的函式物件，而非根據實際執行情況來重新建立新的closure來賦予對應以baseFunction為主的新函式物件




#### 問題案例

首先一開始在這裡會有名為Allow Toggling和Toggle Pargraph這兩個按鈕，想透過點擊一個按鈕Allow Toggling才能啟用另外一個按鈕Toggle Pargraph的正常作用。


一開始toggleParagraphHandler會從useCallback這個Hook獲取到一個函式物件並儲存在記憶體內，其函式內容為如下，在這裡allowToggle、setShowParagraph、prevShowParagraph會因為closure而對應此時：
	- allowToggle 對應到目前用allowToggle來作為識別字的記憶體區塊
	- setShowPargraph 對應到目前用setShowPargraph來作為識別字的記憶體區塊
	- prevShowParagraph 對應到目前用 prevShowParagraph來作為識別字的記憶體區塊

```
   if (allowToggle) {
      setShowParagraph((prevShowParagraph) => !prevShowParagraph);
    }
```

接著將toggleParagraphHandler會是該函式物件，並且將它設定在Toggle Paragraph! 這按鈕的點擊事件中。接著渲染後，點擊Allow Toggling後來使allowToggle更新為true來觸發渲染，可在下一次渲染時，

```
function App() {
  const [showParagraph, setShowParagraph] = useState(false);
  const [allowToggle, setAllowToggle] = useState(false);

  console.log('APP RUNNING');

  const toggleParagraphHandler = useCallback(() => {
    if (allowToggle) {
      setShowParagraph((prevShowParagraph) => !prevShowParagraph);
    }
  }, []);

  const allowToggleHandler = () => {
    setAllowToggle(true);
  };

  return (
    <div className="app">
      <h1>Hi there!</h1>
      <DemoOutput show={showParagraph} />
      <Button onClick={allowToggleHandler}>Allow Toggling</Button>
      <Button onClick={toggleParagraphHandler}>Toggle Paragraph!</Button>
    </div>
  );
}
```

toggleParagraphHandler 會因為deps是空陣列的緣故而不更動，僅繼續使用目前記憶體儲存的函式物件來回傳，所以toggleParagraphHandler還是以下內容來執行：
	- allowToggle - 當時為false的記憶體區塊
```
   if (allowToggle) {
      setShowParagraph((prevShowParagraph) => !prevShowParagraph);
    }
```

這導致無法透過點擊一個按鈕才能啟用另外一個按鈕的正常作用。


#### 解法：問題案例
直接設定allowToggle為useCallback的deps陣列的元素一部分，就能在每次渲染函式執行時，就呼叫執行useCallback來獲得全新的函式物件，這時函式物件會以目前的記憶體區塊來參考並納入closure，

```
  const toggleParagraphHandler = useCallback(() => {
    if (allowToggle) {
      setShowParagraph((prevShowParagraph) => !prevShowParagraph);
    }
  }, [allowToggle]);
```
所以當allowToggle從false轉換至true，useCallback就發覺到allowToggle有改變，所以就直接以重建函式物件的方式來執行useCallback，此時的新函式物件的新closure會對應：
	- allowToggle - 目前內容為true的記憶體區塊
這使得每次執行函式物件時，都會以true的形式來執行該函式物件，這樣子的切換功能就實現了點擊特定按鈕才能啟用另外一個按鈕的正常作用。

## 複習


#🧠 useCallback(baseFunction, \[deps\]) 的 deps 用途為何->->-> `useCallback 只會回傳擁有特定時機下之closure的函式物件，而非根據實際執行情況來重新建立新的closure來賦予對應以baseFunction為主的新函式物件`
<!--SR:!2022-10-09,3,250-->

#🧠 由於useCallback 回傳的函式是函式物件，所以會擁有closure概念，那麼就代表著每個函式搭配closure會是？ ->->-> `每個函式物件會透過closure來對應特定執行時間點下的渲染函式所產生出來的記憶體區塊`
<!--SR:!2022-10-19,10,250-->

#🧠 首先一開始在這裡會有名為Allow Toggling和Toggle Pargraph這兩個按鈕，想透過點擊一個按鈕Allow Toggling才能啟用另外一個按鈕Toggle Pargraph的正常作用，請問以下程式碼能夠實現目標嗎？為什麼？![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1664995272/blog/react/hook/useCallback/useCallback-question-example_sebqb3.png) ->->-> `一開始toggleParagraphHandler會從useCallback這個Hook獲取到一個函式物件並儲存在記憶體內，其函式內容為如下，在這裡allowToggle、setShowParagraph、prevShowParagraph會因為closure而對應此時： - allowToggle 對應到目前用allowToggle來作為識別字的記憶體區塊 - setShowPargraph 對應到目前用setShowPargraph來作為識別字的記憶體區塊 - prevShowParagraph 對應到目前用 prevShowParagraph來作為識別字的記憶體區塊。接著將toggleParagraphHandler會是該函式物件，並且將它設定在Toggle Paragraph! 這按鈕的點擊事件中。接著渲染後，點擊Allow Toggling後來使allowToggle更新為true來觸發渲染，可在下一次渲染時，toggleParagraphHandler 會因為deps是空陣列的緣故而不更動，僅繼續使用目前記憶體儲存的函式物件來回傳，所以toggleParagraphHandler還是以下內容來執行： - allowToggle - 當時為false的記憶體區塊`
<!--SR:!2022-10-09,3,250-->


#🧠 首先一開始在這裡會有名為Allow Toggling和Toggle Pargraph這兩個按鈕，想透過點擊一個按鈕Allow Toggling才能啟用另外一個按鈕Toggle Pargraph的正常作用，以下程式碼有問題，請問如何解決？![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1664995272/blog/react/hook/useCallback/useCallback-question-example_sebqb3.png) ->->-> `![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1664995272/blog/react/hook/useCallback/useCallback-solution-example_rpapwq.png)`
<!--SR:!2022-10-09,3,250-->


#🧠  上面程式碼解決了點擊一個按鈕Allow Toggling才能啟用另外一個按鈕Toggle Pargraph的正常作用，請說明為什麼![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1664995272/blog/react/hook/useCallback/useCallback-solution-example_rpapwq.png) ![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1664995272/blog/react/hook/useCallback/useCallback-question-example_sebqb3.png)->->-> `直接設定allowToggle為useCallback的deps陣列的元素一部分，就能在每次渲染函式執行時，就呼叫執行useCallback來獲得全新的函式物件，這時函式物件會以目前的記憶體區塊來參考並納入closure，所以當allowToggle從false轉換至true，useCallback就發覺到allowToggle有改變，所以就直接以重建函式物件的方式來執行useCallback，此時的新函式物件的新closure會對應： - allowToggle - 目前內容為true的記憶體區塊。這使得每次執行函式物件時，都會以true的形式來執行該函式物件，這樣子的切換功能就實現了點擊特定按鈕才能啟用另外一個按鈕的正常作用。`
<!--SR:!2022-10-09,3,250-->



---
Status: #🌱 
Tags:
[[React]]
Links:
[[Closure 是一種封閉空間的結構體，該結構體會定義著特定scopeA下的識別字對應著特定scopeB下的實體物件，scopeA和scopeB 可能會是一樣或者不一樣]]
[[React：useCallback 最主要是會依據依賴項目是否變動來決定是否重建函式物件並儲存在記憶體中，若變動就建立新函式物件和新closure，接著儲存並回傳，若沒變動就以目前最新函式物件回傳]]
References: