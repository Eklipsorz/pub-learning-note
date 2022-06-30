

## 描述
http://heartfootprint.blogspot.com/2012/07/querystring.html

https://www.cnblogs.com/CrazyCoder/archive/2007/10/17/928261.html
> 现在手上的项目中使用了ClickOnce技术来部署客户端，客户端有时需要从服务器传一些参数，对于ClickOnce部署的程序来说我们可以在launch的URL中使用query strings来达到这一目的。参照MSDN上的文章，很快就写完了代码。好了，试试看。部署，从服务器launch客户端，似乎一切正常，所有参数的值都顺利得到了。

> 可还没等Check-in代码，一个测试就失败了。Debug了半天才发现原来是一个参数值中又加号：+。在使用HttpUtility.ParseQueryString分析query string后参数值中的加号变成了空格，以前似乎没遇到过这样的现象。[Google](http://www.google.cn/search?q=querystring+plus+sign&complete=1&hl=zh-CN&newwindow=1&rlz=1T4GGIG_enCN241CN241)了一下才知道原来加号在query string是保留用来代表空格的，要在query string中传这些保留字符必须对query string进行编码。

> 修改了服务端的代码，想当然的在客户端加了decode的方法，没想到结果还是不对。查了MSDN关于HttpUtility.ParseQueryString方法的帮助才知道原来这个方法内置会对query string进行解码（decode）并返回包含结果的NameValueCollection。

> 忙了半天最后终于搞定了。

> 总结一下：

> 1）安全起见query string一定要encode
> 2）HttpUtility.ParseQueryString会自动做decode，不要画蛇添足。


### 
https://stackoverflow.com/questions/6855624/plus-sign-in-query-string
> `+` sign has a semantic meaning in the query string. It is used to represent a space. Another character that has semantic importance in the query string is `&` which is used to separate the various `var=value` pairs in the query string.

> Most server side scripts would decode the query parameters before using them, so that a `+`gets properly converted to a space. Now, if you want a literal `+` to be present in the query string, you need to specify `%2B` instead.

> `+` sign in the query string is URL-decoded to a space. `%2B` in the query string is URL-decoded to a + sign.


https://www.albionresearch.com/tools/urlencode
> RFC2396 mode (no Unicode or UTF8, space encoded as ‘+’)


### 案例
編碼方：
```
daeaf+wadadwa+dasddaw
```


解碼方：
```
daeaf wadadwa dasddaw
```


## 複習
#🧠 Question :: ->->-> ``

---
Status: #🌱 
Tags:
Links:
References: