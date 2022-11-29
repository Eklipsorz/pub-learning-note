## 描述


### 對特定Quote增加評論功能

主要需要實現：
1. 發送請求向後端伺服器要求增加評論至特定Quote
2. 當完成發送並成功新增時，就轉移至瀏覽特定Quote下的所有評論
3. 在瀏覽特定Quote下的所有評論下，若評論還在載入就必須呈現載入中

###  方向1 & 方向2的實現
在新增評論表單下進行：
方向1：發送請求向後端伺服器要求增加評論至特定Quote
方向3：當完成發送並成功新增時，就轉移至瀏覽特定Quote下的所有評論

邏輯是：
1. 每一次render之後都檢查目前請求資料載入狀況，若請求載入狀況是沒問題就執行onAddedComment來轉移至瀏覽特定Quote下的所有評論
2. 當觸發表單提交時，就向伺服器發送增加評論的請求

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
  
  return (
    <form className={classes.form} onSubmit={submitFormHandler}>
      <div className={classes.control} onSubmit={submitFormHandler}>
        <label htmlFor='comment'>Your Comment</label>
        <textarea id='comment' rows='5' ref={commentTextRef}></textarea>
      </div>
      <div className={classes.actions}>
        <button className='btn'>Add Comment</button>
      </div>
    </form>
  );
```


### 方向2&方向3的實現
在commentsList：
方向2：在瀏覽特定Quote下的所有評論下，若評論還在載入就必須呈現載入中

邏輯是：
1. 進入所有評論頁面時會發送索要所有評論的請求並作出渲染
2. 當增加評論時就重新發送索要所有評論的請求並作出渲染
3. 若狀態為pending就呈現資料載入中、若錯誤發生就呈現有錯誤、若零個評論資料就呈現0筆資料、若有N個評論資料就呈現資料
```
const [isAddingComment, setIsAddingComment] = useState(false);

  const params = useParams();
  const { quoteId } = params;

  const {
    sendRequest,
    status,
    data: loadedComments,
    error,
  } = useHttp(getAllComments, true);

  useEffect(() => {
    sendRequest(quoteId);
  }, [sendRequest, quoteId]);

  const addedCommentHandler = useCallback(() => {
    sendRequest(quoteId);
  }, [sendRequest, quoteId]);

  let content = '';

  if (status === 'pending') {
    content = (
      <div className='centered'>
        <LoadingSpinner />
      </div>
    );
  }

  if (error) {
    content = <p className='centered focused'>{error}</p>;
  }

  if (status === 'completed' && !loadedComments.length) {
    content = <p className='centered focused'>No Comment Found!!!</p>;
  }

  if (status === 'completed' && loadedComments.length) {
    content = <CommentsList comments={loadedComments} />;
  }

  return (
    <section className={classes.comments}>
      <h2>User Comments</h2>
      {!isAddingComment && (
        <button className='btn' onClick={startAddCommentHandler}>
          Add a Comment
        </button>
      )}
      {isAddingComment && (
        <NewCommentForm
          quoteId={params.quoteId}
          onAddedComment={addedCommentHandler}
        />
      )}
      {content}
    </section>
  );
```

## 複習

#💻 Question :: ->->-> ``

---
Status: #🌱 
Tags:
[[React]]
Links:
References: