## 描述

### absolute URL

[[@mdnWhatURLLearn]]
>  Examples of absolute URLs：
> 1.  Full URL (the same as the one we used before)
```
https://developer.mozilla.org/en-US/docs/Learn
```
> 2. Implicit protocol：In this case, the browser will call that URL with the same protocol as the one used to load the document hosting that URL.
```
//developer.mozilla.org/en-US/docs/Learn
```
> 3. Implicit domain name：This is the most common use case for an absolute URL within an HTML document. The browser will use the same protocol and the same domain name as the one used to load the document hosting that URL. **Note:** _it isn't possible to omit the domain name without omitting the protocol as well_.
```
/en-US/docs/Learn
```

重點：
- absolute URL：意指為特定資源完整位置，其完整位置包含了該資源在網路上的完整位置、該資源在特定協定網路下的完整位置、該資源在特定主機下的完整位置，這使得它有三種形式來表示其位置
- 主要有三種形式：
	- Full URL：該資源在網路上的完整位置，主要由protocol、host、port、path所構成
	- Implicit protocol：該資源在特定協定網路下的完整位置，主要由host、port、path所構成，其中protocol會採用目前所在的資源之完整位置所擁有的protocol


### relative URL




> If the path part of the URL starts with the "`/`" character, the browser will fetch that resource from the top root of the server, without reference to the context given by the current document.


## 複習
#🧠 Question :: ->->-> ``

---
Status: #🌱 
Tags:
Links:
References:
[[@mdnWhatURLLearn]]