## 描述


### 每一次經由useCallback 所得到的函式物件所擁有的closure

由於useCallback 回傳的函式是函式物件，所以會擁有closure概念，每個函式物件會透過closure來對應特定執行時間點下的渲染函式所產生出來的記憶體區塊


### 案例：

首先一開始在這裡會有名為Allow Toggling和Toggle Pargraph這兩個按鈕，一開始toggleParagraphHandler會從useCallback這個Hook獲取到一個函式物件並儲存在記憶體內，其函式內容為如下，在這裡allowToggle、setShowParagraph、prevShowParagraph會因為closure而對應此時：
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

## 複習

---
Status: #🌱 
Tags:
[[React]]
Links:
[[Closure 是一種封閉空間的結構體，該結構體會定義著特定scopeA下的識別字對應著特定scopeB下的實體物件，scopeA和scopeB 可能會是一樣或者不一樣]]
[[React：useCallback 最主要是透過將指定函式儲存在記憶體並於每一次元件的渲染函式被觸發執行時，就將記憶體的指定函式回傳給元件使用]]
References: