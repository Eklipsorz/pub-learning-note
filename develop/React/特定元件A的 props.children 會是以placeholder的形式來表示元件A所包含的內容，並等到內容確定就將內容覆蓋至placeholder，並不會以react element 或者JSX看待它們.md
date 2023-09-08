
## 描述

[[@arnoldQuickIntroReact2018]]
> ### What even is ‘children’?

> The [React docs](https://facebook.github.io/react/docs/composition-vs-inheritance.html) say that you can use `props.children` on components that represent ‘generic boxes’ and that ‘don’t know their children ahead of time’. For me, that didn’t really clear things up. I’m sure for some, that definition makes perfect sense but it didn’t for me.

> My simple explanation of what `this.props.children` does is that it is used to display whatever you include between the opening and closing tags when **invoking** a component.

> ### A simple example
> 
> Here’s an example of a stateless function that is used to create a component. Again, since this is a stateless function, there is no `'this'` keyword so just use `props.children`
```
const Picture = (props) => {  
  return (  
    <div>  
      <img src={props.src}/>  
      {props.children}  
    </div>  
  )  
}
```

> This component contains an `<img>` that is receiving some `props` and then it is displaying `{props.children}`.

> Whenever this component is invoked `{props.children}` will also be displayed and this is just a reference to what is between the opening and closing tags of the component.


```
//App.jsrender () {  
  return (  
    <div className='container'>  
      <Picture key={picture.id} src={picture.src}>  
          //what is placed here is passed as props.children    
      </Picture>  
    </div>  
  )  
}
```


> Instead of invoking the component with a self-closing tag `<Picture />` if you invoke it will full opening and closing tags `<Picture> </Picture>` you can then place more code between it.

> This de-couples the `<Picture>` component from its content and makes it more reusable.


重點：
- 特定元件A的 props.children 會是以placeholder的形式來表示元件A所包含的內容，並且直接將內容覆蓋至placeholder，並不會以react element 或者JSX看待它們

## 複習
#🧠  React ：特定元件單獨回傳props.children，在這裏會觸發JSX的語法問題嗎？ ->->-> `並不會，由於他們本身並不會以react element 或者JSX看待它們，而是以placeholder來表示特定元件所包含的內容，等到內容確定就會將內容直接覆蓋`
<!--SR:!2023-09-30,22,210-->

#🧠 React ：特定元件單獨回傳props.children 會如何被解析 ->->-> `特定元件A的 props.children 會是以placeholder的形式來表示元件A所包含的內容，並且直接將內容覆蓋至placeholder，並不會以react element 或者JSX看待它們`
<!--SR:!2023-10-04,38,230-->

#🧠  React ：特定元件回傳內容中夾雜其他元件和props.children，在這裏的props.children會觸發JSX的語法問題嗎？->->-> `並不會，由於他們本身並不會以react element 或者JSX看待它們，而是以placeholder來表示特定元件所包含的內容，等到內容確定就會將內容直接覆蓋`
<!--SR:!2024-03-29,227,250-->


---
Status: #🌱 
Tags:
[[React]] - [[JavaScript]]
Links:
References:
[[@arnoldQuickIntroReact2018]]
