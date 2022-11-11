## 描述



### layout component 是什麼？

[[@olenadrugalyaLayoutComponentWhy]]
> This component does exactly what its name says - it defines the **layout of the application**. It simply accepts `children` as `props` and render them to the DOM together or without other child components.

> It's a good practice to separate it from other components in the project in a separate folder like this:

![](https://res.cloudinary.com/practicaldev/image/fetch/s--VRBJFi1q--/c_limit%2Cf_auto%2Cfl_progressive%2Cq_auto%2Cw_880/https://dev-to-uploads.s3.amazonaws.com/i/1atexmv0lw87bdvdn8re.png)

重點：
- layout component 會是指元件本身會


#### 使用方式

> In the Layout folder we create **Layout.js** file and store the code of layout component there:

```
import React from 'react';

const Layout =({children}) =>{
    return(
        <>
        <div>
            <ToolBar/>
            <Sides/>
            <Backdrop/>
        </div>
        <main>{children}</main>
        </>
    )
}

export default Layout;
```

> In the main **App.js** file we import Layout and wrap our application with it:
```
import React from "react";
import Layout from "./components/Layout/Layout";

function App() {
  return (
    <>
      <Layout>
        <p>Test</p>
      </Layout>
    <>
  );
}

export default App;
```

> So we have separated layout logic into the component and if we want to change layout later, we can simple do that with changing just one component.




> Because Layout component is so simple, it can be re-used in other parts of application, where a developer wants to use the same page layout. Moreover, it's possible to create customs reusable layouts which use FlexBox or Grid properties like this:

```
<Flexbox vertical gap={3}>
  <Flexbox noGrow>
    <h1>A Title for You</h1>
  </Flexbox>
  <Flexbox bottom>
    <p>Your cool paragraph.</p>
  </Flexbox>
</Flexbox>
```

> Working with reusable layouts is a very good practice, because it let you write code once and use it in a lot of parts of your application.

> Here below are some of the reusable layout components which one can use while building applications:


**_1. React grid layout_** - [demo](https://strml.github.io/react-grid-layout/examples/0-showcase.html) and [code](https://github.com/STRML/react-grid-layout)  
**_2. React Flexbox grid_** - [code](https://github.com/roylee0704/react-flexbox-grid)  
**_3. React Material-UI grid_** - [source](https://material-ui.com/components/grid/)  
**_4. Grommet grid layout_** - [source](https://v2.grommet.io/grid)  
**_5. React Bootstrap / Reactstrap grid layout_** - [source](https://react-bootstrap.netlify.app/layout/grid/)  
**_6. Autoresponsive React_** - [code](https://github.com/xudafeng/autoresponsive-react)  
**_7. React stack grid_** - [demo](https://tsuyoshiwada.github.io/react-stack-grid/#/) and [code](https://github.com/tsuyoshiwada/react-stack-grid)  
**_8. Hedron_** - [code](https://github.com/garetmckinley/hedron)  
**_9. React grid system_** - [code](https://github.com/sealninja/react-grid-system)  
**_10. Rebass React grid_** - [code](https://github.com/rebassjs/grid)  
**_11. Semantic-UI React grid_** - [source](https://react.semantic-ui.com/collections/grid/)  
**_12. Reflexbox_** - [code](https://github.com/jxnblk/reflexbox)


### layout 意義
> the way that something is arranged


重點：
- layout 會是指特定事物被擺放的方式




## 複習


---
Status: #🌱 
Tags:
[[React]]
Links:
References:
[[@olenadrugalyaLayoutComponentWhy]]