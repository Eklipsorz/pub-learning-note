## 描述
[[@reactFragmentsReact]]
> React 其中一種常見的使用情況是在一個 component 中回傳多個 element，fragment 讓你能夠在不用增加額外 DOM 節點的情況下，重新組合 child component

fragmenet 本身是內建的empty wrapper component機制


Fragment 實際上是
```
  const Wrapper = (props) => {
    return props.children;
  };

  export default Wrapper;
```


Fragment 會產生出empty wrapper component，語法會是
```
return (
    <React.Fragment>
        <h2>Hi there!</h2>
        <p>This does not work :-< </p>
    </React.Fragment>
);

```

```
return (
    <>
        <h2>Hi there!</h2>
        <p>This does not work :-< </p>
    </>
);
```

### 功能源自於哪個版本？

[[@reactReactV16Improved]]
> # React v16.2.0: Improved Support for Fragments
> November 28, 2017 by [Clement Hoang](https://twitter.com/c8hoang)
>
> React 16.2 is now available! The biggest addition is improved support for returning multiple children from a component’s render method. We call this feature _fragments_:
## 複習


---
Status: #🌱 #📓 
Tags:
[[React]] 
Links:
[[empty wrapper component實質上不會有任何對應Virtual DOM和對應實際DOM節點，憑藉著滿足JSX語法上的侷限-要有一個JSX parent 元件來包含子元件來包含(wrap)多個子元件來一次性回傳多個子元件]]
[[React：製作empty wrapper component來替代原本要用div包含的子節點，該wrapper component實際上對應著不存在的Virtual DOM結構，亦即為不會產生對應實際DOM 結構]]
References:
[[@reactFragmentsReact]]
[[@reactReactV16Improved]]