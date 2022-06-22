




```
npm install redis connect-redis express-session
```



```
const session = require("express-session")
let RedisStore = require("connect-redis")(session)

// redis@v4
const { createClient } = require("redis")
let redisClient = createClient({ legacyMode: true })
redisClient.connect().catch(console.error)

app.use(
  session({
    store: new RedisStore({ client: redisClient }),
    saveUninitialized: false,
    secret: "keyboard cat",
    resave: false,
  })
)
```