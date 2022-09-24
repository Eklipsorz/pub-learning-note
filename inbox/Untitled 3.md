## 描述




### 用法



> 在下面的例子中，`FancyButton` 藉由 `React.forwardRef` 來獲取傳遞到它身上的 `ref`，然後再傳遞到它 render 的 DOM `button` 上：

```
const FancyButton = React.forwardRef((props, ref) => (  

  <button ref={ref} className="FancyButton">    
	  {props.children}
  </button>
));

// You can now get a ref directly to the DOM button:
const ref = React.createRef();
<FancyButton ref={ref}>Click me!</FancyButton>;
```

> 這樣一來，使用 `FancyButton` 的 component 可以獲得它底下的 `button` 的 DOM 節點的 ref，並可以在需要的時候獲取它 —— 就如同直接使用 `button` DOM 一樣。

> 以下一步一步的解釋上面的例子到底發生了什麼事：

> 1.  我們藉由呼叫 `React.createRef` 產生了一個 [React ref](https://zh-hant.reactjs.org/docs/refs-and-the-dom.html)，然後將它賦值於叫做 `ref` 的變數裡。
> 2.  我們藉由把 `ref` 當成一個 JSX attribute 來把它傳遞到 `<FancyButton ref={ref}>`。
> 3.  React 把 `ref` 當作第二個變數傳到 `forwardRef` 裡的 `(props, ref) => ...` function。
> 4.  我們藉由把這個 `ref` 當作 JSX attribute 來傳遞到更下面的 `<button ref={ref}>`。
> 5.  當 ref 被附上之後，`ref.current` 會指向 `<button>` DOM 節點。


  
forwardRef 回傳React Component，但這個Component 可被Ref技術擷取到對應的實際DOM節點



重點：
- React.createRef 會回傳React ref，而React ref 本身是儲存特定DOM節點之參照位置的物件
- React.forward


## 複習

---
Status: #🌱 #📓 
Tags:
Links:
References:
