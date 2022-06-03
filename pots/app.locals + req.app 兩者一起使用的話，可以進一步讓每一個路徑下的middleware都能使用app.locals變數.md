
## 描述

### app.locals 是什麼？

[[@geeksforgeeksExpressJsApp2020]]所描述：
> The app.locals object has properties that are local variables within the application.

重點：
- app.locals 定義著整個express app下的區域變數，換言之，就是只屬於特定app的變數

### req.app 是什麼？

[[@express.jsExpressReqApp]]所描述：
> ### req.app

> This property holds a reference to the instance of the Express application that is using the middleware.

重點：
- req 物件是只有middleware會使用的
- req.app 會指向正在使用該middleware的 express app，也就是相當於以下的app所指向的實例
```
const app = express()
```

### app.locals + req.app 用途？
app.locals + req.app 兩者一起使用的話，可以進一步讓每一個路徑下的middleware都能使用app.locals變數

> A neat way to do this is to use `app.locals` provided by Express itself. [Here](http://expressjs.com/en/api.html#app.locals) is the documentation.

```javascript
// In app.js:
app.locals.variable_you_need = 42;

// In index.js
exports.route = function(req, res){
    var variable_i_needed = req.app.locals.variable_you_need;
}
```


## 複習

#🧠 Express 框架下的 app.locals 是什麼？ ->->-> `pp.locals 定義著整個express app下的區域變數，換言之，就是只屬於特定app的變數`
<!--SR:!2022-06-05,3,250-->

#🧠  Express 框架下的 req.app 是什麼->->-> `req 物件是只有middleware會使用的，req.app 會指向正在使用該middleware的 express app，也就是相當於以下的app所指向的實例`
<!--SR:!2022-06-05,2,230-->

#🧠 express 如何透過app.locals和req.app來讓每個路徑下的middleware都能使用app.locals變數 ->->-> `只要讓在路徑下對app.locals做屬性上的新增/變更，就能在後面路徑下的middleware透過req.app來調用app本身，接著透過它來存取app.locals，換言之，就是req.app.locals`

---
Status: #🌱 
Tags:
[[Express]]
Links:
References:
[[@aliNodeJsGlobal]]
[[@express.jsExpressReqApp]]
[[@geeksforgeeksExpressJsApp2020]]