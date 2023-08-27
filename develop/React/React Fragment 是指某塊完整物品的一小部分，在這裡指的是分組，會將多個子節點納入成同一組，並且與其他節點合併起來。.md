## 描述
[[@reactFragmentsReact]]
> React 其中一種常見的使用情況是在一個 component 中回傳多個 element，fragment 讓你能夠在不用增加額外 DOM 節點的情況下，重新組合 child component

- fragment 是指某塊完整物品的一小部分，在這裡會是包含多個元件的邏輯區塊或者邏輯元件。
- fragment 本身是empty wrapper component
- fragment 主要用途為
	- 利用empty wrapper component 對於React建立DOM語法的合法性來實現目標-既可以滿足JSX語法侷限又可以不用增加額外DOM節點的情況下，來回傳一組多個子節點




### Fragment 結構

Fragment 實際上是
```
  const Fragment = (props) => {
    return props.children;
  };

  export default Fragment;
```



### Fragment 語法使用

Fragment 會產生出empty wrapper component，語法會是

1. 語法1：
```
return (
	<React.Fragment>
		<childrean>
	</React.Fragment>
);
```

2. 語法2：簡化而成的語法糖
```
return (
	<>
		<childrean>
	</>
);
```

#### 案例
```
return (
        <h2>Hi there!</h2>
        <p>This does not work :-< </p>
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


重點：
- Fragment 功能起源於React 16.2.0起
### fragment 命名緣由
fragment 
> a small piece or a part, especially when broken from something whole

重點：
- 從一個特定完整事物切分出來的一小部分

## 複習

#🧠  fragment 命名緣由 是什麼？ ->->-> `從一個特定完整事物切分出來的一小部分`
<!--SR:!2024-02-17,315,250-->


#🧠 fragment 在React上是指什麼意思？ ->->-> `fragment 是指某塊完整物品的一小部分，在這裡會是包含多個元件的邏輯區塊或者邏輯元件。`
<!--SR:!2024-06-20,393,250-->

#🧠 fragment 在React上是什麼Component？(請用簡短的話來說) ->->-> `empty wrapper component`
<!--SR:!2024-11-15,486,250-->


#🧠 React fragment 主要用途為 ->->-> `既可以滿足JSX語法侷限又可以不用增加額外DOM節點的情況下，來回傳一組多個子節點`
<!--SR:!2023-09-16,20,190-->

#🧠 React fragment 主要用途為既可以滿足JSX語法侷限又可以不用增加額外DOM節點的情況下，來回傳一組多個子節點，憑什麼可以滿足那些的？ ->->-> `利用empty wrapper component 對於React建立DOM語法的合法性`
<!--SR:!2024-11-18,488,250-->


#🧠 React Fragment 如何用程式碼表示它本身？ ->->-> `const Fragment = (props) => { return props.children;  }; export default Fragment;`
<!--SR:!2023-09-21,52,190-->


#🧠 React fragment 語法會有哪些形式(提示兩個) ->->-> `return (<React.Fragment> <childrean> </React.Fragment>) 和 return ( <> <children> </> )`
<!--SR:!2024-12-02,503,250-->

#🧠 這是React fragment 語法嗎？ 還是什麼(嚴格來說)![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1662894948/blog/react/fragment/react-fragment-sugar_xcazre.png) ->->-> `算是，但嚴格來說是fragment 的語法糖`
<!--SR:!2024-11-14,485,250-->



#🧠 請用React Fragment的非語法糖來解決以下程式碼 ![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1662894853/blog/react/fragment/react-fragment-example_l6fx92.png)->->-> ``
<!--SR:!2024-03-10,328,250-->


#🧠 請用React Fragment的語法糖來解決以下程式碼 ![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1662894853/blog/react/fragment/react-fragment-example_l6fx92.png)->->-> ``
<!--SR:!2024-10-15,460,250-->



---
Status: #🌱 
Tags:
[[React]] 
Links:
[[empty wrapper component實質上不會有任何對應Virtual DOM和對應實際DOM節點，憑藉著滿足JSX語法上的侷限-要有一個JSX parent 元件來包含子元件來包含(wrap)多個子元件來一次性回傳多個子元件]]
[[React：製作empty wrapper component來替代原本要用div包含的子節點，該wrapper component實際上對應著不存在的Virtual DOM結構，亦即為不會產生對應實際DOM 結構]]
References:
[[@reactFragmentsReact]]
[[@reactReactV16Improved]]