## 描述


> `process.argv` is an array containing the command line arguments. The first element will be 'node', the second element will be the name of the JavaScript file. The next elements will be any additional command line arguments.

```javascript
// print process.argv
process.argv.forEach(function (val, index, array) {
  console.log(index + ': ' + val);
});
```

重點：
- process.argv 是一個陣列，儲存著使用者使用node指定對執行檔執行所額外添加的參數
```
node xxx.js argv
```

This will generate:

```
$ node process-2.js one two=three four
0: node
1: /Users/mjr/work/node/process-2.js
2: one
3: two=three
4: four
```

https://www.digitalocean.com/community/tutorials/nodejs-command-line-arguments-node-scripts
---
Status: #
Tags:
Links:
References:
[[@moogooJavascriptHowPass]]