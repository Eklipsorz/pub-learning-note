引用[[@avengerWhyDoesIsNaN2019]]所描述
> JavaScript interprets an empty string as a 0, which then fails the isNAN test. You can use parseInt on the string first which won't convert the empty string to 0. The result should then fail isNAN.



> You may find this surprising or maybe not, but here is some test code to show you the wackyness of the JavaScript engine.

```javascript
document.write(isNaN("")) // false
document.write(isNaN(" "))  // false
document.write(isNaN(0))  // false
document.write(isNaN(null)) // false
document.write(isNaN(false))  // false
document.write("" == false)  // true
document.write("" == 0)  // true
document.write(" " == 0)  // true
document.write(" " == false)  // true
document.write(0 == false) // true
document.write(" " == "") // false
```


## 描述

## 複習
#🧠 Question :: ->->-> ``

---
Status: 
Tags:
Links:
References:
[[@avengerWhyDoesIsNaN2019]]