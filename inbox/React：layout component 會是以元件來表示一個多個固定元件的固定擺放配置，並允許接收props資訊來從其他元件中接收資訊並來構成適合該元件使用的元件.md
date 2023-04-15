## 描述



### layout component 是什麼？

[[@olenadrugalyaLayoutComponentWhy]]
> This component does exactly what its name says - it defines the **layout of the application**. It simply accepts `children` as `props` and render them to the DOM together or without other child components.

> It's a good practice to separate it from other components in the project in a separate folder like this:

![](https://res.cloudinary.com/practicaldev/image/fetch/s--VRBJFi1q--/c_limit%2Cf_auto%2Cfl_progressive%2Cq_auto%2Cw_880/https://dev-to-uploads.s3.amazonaws.com/i/1atexmv0lw87bdvdn8re.png)

重點：
- layout component 會是以元件來表示多個固定元件的固定擺放配置，並允許接收props資訊來從其他元件中接收資訊並來構成適合該元件使用的元件，或者說 layout component 建立一個配置來供其他元件填入內容的元件
- 用途為：是定義特定元件的擺放方式，其中特定元件為包含的後裔元件
- 通常會定義在
	- /src/components/layout
	- /src/components/Layout
- 開發方式：盡量讓layout component 本身保持可重復性使用的元件

#### 案例：使用方式

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

重點：
- 在這裡定義一個Layout元件，裡頭已經定義好每個元件的擺放方式，並且以props.children來接收從其他元件傳遞過來的資訊來建構



#### 其他案例

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
- layout 會是指特定事物被擺放的方式，通常會當作成多個事物的擺放方式

## 複習



#🧠  layout component 用途是什麼？ ->->-> `是定義特定元件的擺放方式，其中特定元件為包含的後裔元件`
<!--SR:!2023-09-18,194,250-->


#🧠 layout 意義 會是什麼？ ->->-> ` layout 會是指特定事物被擺放的方式`
<!--SR:!2023-09-16,193,250-->


#🧠 layout 意義 會是什麼？以多個事物來說的話？ ->->-> `通常會當作成多個事物的擺放方式`
<!--SR:!2023-06-16,131,250-->


#🧠 react：layout component 的用途是定義特定元件的擺放方式，其中特定元件為包含的後裔元件，具體是什麼？->->-> `會是以元件來表示多個固定元件的固定擺放配置，並允許接收props資訊來從其他元件中接收資訊並來構成適合該元件使用的元件`
<!--SR:!2023-07-07,145,250-->



#🧠 layout component 會是以元件來表示多個固定元件的固定擺放配置，並允許接收props資訊來從其他元件中接收資訊並來構成適合該元件使用的元件，講白話會是什麼意思？(後裔擺放方式) ->->-> `以元件建構以後裔元件為主的固定擺放方式。`
<!--SR:!2023-04-16,39,230-->

#🧠 layout component 會是以元件來表示多個固定元件的固定擺放配置，並允許接收props資訊來從其他元件中接收資訊並來構成適合該元件使用的元件，講白話會是什麼意思？ ->->-> `以元件建構以後裔元件為主的固定擺放方式。`
<!--SR:!2023-07-11,87,230-->


#🧠 若要將component 以layout用途來區分的話，會放在哪個地方？ ->->-> `/src/components/layout、/src/components/Layout`
<!--SR:!2023-06-26,136,250-->



#🧠 layout component 開發時會要注意什麼？ ->->-> `盡量讓layout component 本身為可重復性使用的元件`
<!--SR:!2023-09-08,187,250-->


---
Status: #🌱 
Tags:
[[React]]
Links:
References:
[[@olenadrugalyaLayoutComponentWhy]]