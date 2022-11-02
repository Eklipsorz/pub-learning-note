


## 描述


### react 在面對渲染內容為純粹的boolean時

React 會選擇不直接印該boolean內容：

```
  return (
    <React.Fragment>
      {true}
    </React.Fragment>
  );
```


```
  return (
    <React.Fragment>
      {false}
    </React.Fragment>
  );
```

#### 結果

```
  return (
    <React.Fragment>
    </React.Fragment>
  );
```


```
  return (
    <React.Fragment>      
    </React.Fragment>
  );
```

### res && jsx element的res 是boolean

以下面為例，
```
function App() {
  const result = false;
  return (
    <React.Fragment>
      {result && <ForwardCounter />}
      {!result && <BackwardCounter />}
    </React.Fragment>
  );
}
```


#### 若result為true的話

在JS層面和React都會直接回傳
```
<ForwardCounter />
```

#### 若result為false的話

若result為false的話，在JS層面，但React一遇到回傳內容為false/ture就選擇不印
```
false
```





## 複習


---
Status: #🌱 
Tags:
[[React]]
Links:
References: