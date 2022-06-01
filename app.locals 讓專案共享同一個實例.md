A neat way to do this is to use `app.locals` provided by Express itself. [Here](http://expressjs.com/en/api.html#app.locals) is the documentation.

```javascript
// In app.js:
app.locals.variable_you_need = 42;

// In index.js
exports.route = function(req, res){
    var variable_i_needed = req.app.locals.variable_you_need;
}
```

https://stackoverflow.com/questions/9765215/global-variable-in-app-js-accessible-in-routes


重點：
- 一設定app.locals，就即可利用rep.app.locals.xxx 來傳遞

> You can access local variables in templates rendered within the application. This is useful for providing helper functions to templates, as well as application-level data. Local variables are available in middleware via `req.app.locals` (see [req.app](https://expressjs.com/zh-tw/api.html#req.app))

https://expressjs.com/zh-tw/api.html#app.locals