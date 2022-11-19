


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



### res && jsx element的res 不為boolean

以下面為例，假設res不為boolean，會在判斷時轉換成boolean來進行最後的比對
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


#### 若res為0的話

在JS層面會印出0、\<BackwardCounter \/\>
在React都會直接回傳
```
0
<BackwardCounter \>
```

#### 若result為1的話

在JS層面會印出
```
<ForwardCounter />
false
```


在Reac層面會是：
```
<ForwardCounter />
```






## 複習
#🧠 React：若渲染內容是boolean的話，會渲染成什麼？ ->->-> `React一遇到回傳內容為false/ture就選擇不印`
<!--SR:!2022-12-17,28,250-->

#🧠  React：若渲染內容為{boolean}的話，會渲染成什麼？ ->->-> `React一遇到回傳內容為false/ture就選擇不印`
<!--SR:!2022-12-16,27,250-->

#🧠  React：若元件的渲染內容如下的話，其渲染結果會是什麼？ 為什麼？![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1667735041/blog/react/react-element/boolean-react-rendering-result_clnrqi.png)->->-> `<React.Fragment></React.Fragment> React一遇到回傳內容為false/ture就選擇不印`
<!--SR:!2022-12-16,27,250-->

#🧠 React：若元件的渲染內容如下的話，其渲染結果和JS層級各會是什麼樣的結果？![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1667735041/blog/react/react-element/complex-boolean-react_usafk7.png)->->-> `React：第一行沒渲染，第二行就印<BackwardCounter />；JS：第一行會是false，第二行會是<BackwardCounter />`
<!--SR:!2022-12-16,27,250-->

#🧠  React：若元件的渲染內容如下的話，假設result為true，其渲染結果和JS層級各會是什麼樣的結果？![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1667735041/blog/react/react-element/complex-boolean-react_usafk7.png) ->->-> `React：第一行渲染 <ForwardCounter />，第二行就沒渲染；JS：第一行會是<ForwardCounter />，第二行會是false`
<!--SR:!2022-11-19,10,250-->

#🧠 React：若元件的渲染內容如下的話，假設result為1，其渲染結果和JS層級各會是什麼樣的結果？![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1667735041/blog/react/react-element/complex-boolean-react_usafk7.png) ->->-> `在JS層面會印出<ForwardCounter />、false； React：<ForwardCounter />`
<!--SR:!2022-12-17,28,250-->


#🧠 React：若元件的渲染內容如下的話，假設result為0，其渲染結果和JS層級各會是什麼樣的結果？![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1667735041/blog/react/react-element/complex-boolean-react_usafk7.png) ->->-> `在JS層面會印出0、<BackwardCounter />； React：<ForwardCounter />；React：0 <BackwardCounter \>`
<!--SR:!2022-12-16,27,250-->


---
Status: #🌱 
Tags:
[[React]]
Links:
[[JS：And operator、Or operator、Not operator當遇到都是boolean就以boolean來處理；若當遇到任一一個不為boolean就以強制轉換boolean來比較獲取結果]]
References: