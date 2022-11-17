## 描述


當點擊Load Comments按鈕後，就呈現comments，但不想在呈現comments的情況下還呈現按鈕，所以會得使用conditional rendering的技術在按鈕呈現上，在這裡會有以下解法：
1. react-router方法：使用route + exact來實現 
2. react體系：註冊新狀態＋觸發狀態更新和渲染

### react-router方法：使用route + exact來實現 

```
<Route path={`/quotes/${params.quoteId}`} exact>
  <div className='centered'>
    <Link to={`/quotes/${params.quoteId}/comments`} className='btn--flat'>
        Loads Comments
    </Link>
  </div>
</Route>
```


```
return (
    <React.Fragment>
      <h1>Quote Page</h1>
      <HighLightedQuote text={quote.text} author={quote.author} />
      <Route path={`/quotes/${params.quoteId}`} exact>
        <div className='centered'>
          <Link to={`/quotes/${params.quoteId}/comments`} className='btn--flat'>
            Loads Comments
          </Link>
        </div>
      </Route>
      <Route path={`/quotes/${params.quoteId}/comments`}>
        <Comments />
      </Route>
    </React.Fragment>
  );
};
```

## 複習
#🧠 當點擊Load Comments按鈕後，就呈現comments，但不想在呈現comments的情況下還呈現按鈕，通常會使用什麼概念來解決？ ->->-> `所以會得使用conditional rendering的技術在按鈕呈現上`

#🧠 當點擊Load Comments按鈕後，就呈現comments，但不想在呈現comments的情況下還呈現按鈕，通常會使用conditional rendering的技術在按鈕呈現上，具體會有哪些方式？ ->->-> `1. react-router方法：使用route + exact來實現  2. react體系：註冊新狀態＋觸發狀態更新和渲染`

#💻 Question :: ->->-> ``

---
Status: #🌱 
Tags:
[[React]]
Links:
References: