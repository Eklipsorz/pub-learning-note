## 描述

[[@reactpatternsJSXSpreadAttributes]]
> ## What is JSX Spread Attributes?[#](https://reactpatterns.js.org/docs/jsx-spread-attributes#what-is-jsx-spread-attributes "Direct link to heading")
>
> Spread attributes is a JSX feature, it's a syntax for passing all of an object's properties as JSX attributes.

> ## For examples[#](https://reactpatterns.js.org/docs/jsx-spread-attributes#for-examples "Direct link to heading")

>If you know all the properties that you want to place on a component ahead of time, it is easy to use JSX.

```
const component = <Component foo={x} bar={y} />
```

> If you don't know which properties you want to set, you might be tempted to add them onto the object later.

```
var component = <Component />;

component.props.foo = x // bad
component.props.bar = y // also bad
```

> Now you can use a new feature of JSX called spread attributes.

```
let props = {}
props.foo = x
props.bar = y
const component = <Component {...props} />
```


[[@reactJSXDepthReact]]
> ### Spread Attributes
>
> If you already have `props` as an object, and you want to pass it in JSX, you can use `...` as a “spread” syntax to pass the whole props object. These two components are equivalent:

```
function App1() {
  return <Greeting firstName="Ben" lastName="Hector" />;
}

function App2() {
  const props = {firstName: 'Ben', lastName: 'Hector'};
  return <Greeting {...props} />;}
```


## 複習


---
Status: #🌱 #📓 
Tags:
[[React]]
Links:
References:
[[@reactpatternsJSXSpreadAttributes]]
[[@reactJSXDepthReact]]