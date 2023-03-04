
## 描述


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
- 

## 複習
#🧠 Question :: ->->-> ``

---
Status: #🌱 
Tags:
[[React]] - [[JavaScript]]
Links:
References:
