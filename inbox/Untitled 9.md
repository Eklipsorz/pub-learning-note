## 描述


```
const testhandler = () => {
  console.log(this, this.name);
};
function testhandler2() {
  console.log(this, this.name);
}
var name = 'window';
const object = {
  name: 'object',
  fn: testhandler,
};

object.fn();
```

## 複習
#🧠 Question :: ->->-> ``

---
Status: #🌱 
Tags:
[[HTML]] - [[JavaScript]]
Links:
References: