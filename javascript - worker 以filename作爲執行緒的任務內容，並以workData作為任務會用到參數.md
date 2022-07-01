


main.js：以subscriber.js作為任務內容來執行，並參雜workerData來當作其執行緒的參數
```
const worker = new Worker(__dirname + '/subscriber.js', { workerData: 'hiiiii each' });
```


subscriber.js
```
const { Worker, isMainThread, workerData } = require('node:worker_threads');
console.log('thread', workerData)
```