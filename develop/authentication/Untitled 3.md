## 描述


https://auth0.com/docs/secure/tokens/access-tokens/get-access-tokens


https://auth0.com/blog/id-token-access-token-what-is-the-difference/


https://juejin.cn/post/7131956073472196621


> 第一种，是颁发token的时候有一个受众人aud ，也就是颁发给谁 ，我们颁发token的时候，每个用户根据 username+pwd+datetime.now() 的规则作为颁发受众人。

> 这样如果更改了用户名或者密码则受众人就会变更，此时的token已经无效了需要刷新token。另外datetime.now()也可以存在缓存或者用户表，当用户退出登录，或者管理员取消其token有效，则只需更改用户的datetime时间即可，受众人发生变更，token无效。后台需配置ValidateAudience = true,进行认证受众人是否一致。

> 第二种，上篇文章提到过payload载体是可以添加自己的逻辑的，那么我们可以赋予一个 version 作为token的版本信息。例如默认正常产生的token版，也可以是当前时间的时间戳，并记录到用户表或者用户缓存。当token被用户强制失效，或者管理员强制失效，则只需更改这个版本信息即可。认证的时候如果发现版本不一致，则token失效。

  



## 複習



---
Status: 
Tags:
Links:
References: