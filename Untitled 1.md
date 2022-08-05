## 描述

> 在刚学`React/Vue`的时候，配合`webpack`脚手架学习的过程中，碰到一个问题会非常疑惑，比如在`React`中有个`Public`文件夹可以放静态资源，但是在`src`目录中同样有个`assets`文件夹，这个同样也是放静态资源的，这个就很困惑了，为何放置静态资源的地方会有两个？


> 两者区别

> 其实放在两个文件夹区别就在于是否会被webpack所处理，如果您将文件放入该public文件夹，webpack 将不会处理它，在你打包的时候，会将public文件夹直接复制一份到你构建出来的文件夹中。而src/assets目录的文件（前提你在js中有引入），它会被webpack编译，比如图片，如果你的图片小于你在webpack中的loader下设置的limit大小（可配置），它会被编译成base64，从而在实际项目中减少http请求，放置在src/assets目录有以下几点好处：

    脚本和样式表被缩小并捆绑在一起以避免额外的网络请求。
    缺少文件会导致编译错误，而不是用户的404错误。
    结果文件名包含内容哈希，因此您无需担心浏览器缓存旧版本。

> 当然，在实际项目中，公共文件夹public还是有它的作用的，如果你希望你的文件不被编译，比如jquery.min.js，或者压缩好的js插件等，你就可以把文件放在public文件夹中，这样还可以减少文件构建时间，可以减少构建文件的大小。换过来想，如果你把所有静态资源全部放在assets文件夹中，你会发现最后打包出来的文件很大，导致首页白屏时间过长，所以，你可以把一些不会改动的静态文件放到public中。


##### 在[React](https://so.csdn.net/so/search?q=React&spm=1001.2101.3001.7020)中使用公共文件夹public

> 如果在`index.html`中，你可以像这样去使用它：

```
<img src="％PUBLIC_URL%/image/poster.jpeg" alt="">
```


> 只有前缀`public`可以访问文件夹中的文件`%PUBLIC_URL%`。如果需要使用`src`或中的文件`node_modules`，则必须将其复制到那里以明确指定将此文件作为构建的一部分的意图。  
>
> 当运行`npm run build`，`Create React App`将替换`%PUBLIC_URL%`为正确的绝对路径，因此即使使用客户端路由或将其托管在非根`URL`上，项目也会正常工作。  
> 
> 在`JavaScript`代码中，可以`process.env.PUBLIC_URL`出于类似目的使用：

```
render() {
	return <img src={process.env.PUBLIC_URL + '/img/logo.png'} />;
}
```



## 複習

---
Status: #🌱 
Tags:
Links:
References: