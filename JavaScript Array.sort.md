

寫法1

```
const compare = (a, b) => (Date.parse(b.createdAt) - Date.parse(a.createdAt))
```

寫法2
```
const compare = (a, b) => (Date.parse(b.createdAt) >= Date.parse(a.createdAt))
```


寫法1是正確的，但寫法2會導致錯誤，為什麼？