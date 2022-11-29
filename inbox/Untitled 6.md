## 描述


### 對特定Quote增加評論功能

主要需要實現：
1. 發送請求向後端伺服器要求增加評論至特定Quote
2. 發送過程中必須呈現載入中
3. 當完成發送並成功新增時，就轉移至瀏覽特定Quote下的所有評論

###  方向1 & 方向3的實現
方向1：發送請求向後端伺服器要求增加評論至特定Quote

```
  const { sendRequest, status, error } = useHttp(addComment);

  const { onAddedComment } = props;
  useEffect(() => {
    if (status === 'completed' && !error) {
      onAddedComment();
    }
  }, [status, error, onAddedComment]);

  const submitFormHandler = (event) => {
    event.preventDefault();

    // optional: Could validate here

    // send comment to server
    sendRequest({
      commentData: { text: commentTextRef.current.value },
      quoteId: props.quoteId,
    });
  };
```

## 複習


---
Status: #🌱 
Tags:
[[React]]
Links:
References: