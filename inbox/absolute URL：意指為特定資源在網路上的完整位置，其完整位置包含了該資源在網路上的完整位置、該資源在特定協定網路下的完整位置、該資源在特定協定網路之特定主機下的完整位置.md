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
- absolute URL：意指為特定資源在網路上的完整位置，其完整位置包含了該資源在網路上的完整位置、該資源在特定協定網路下的完整位置、該資源在特定協定網路之特定主機下的完整位置，這使得它有三種形式來表示其位置
- 主要有三種形式：
	- Full URL
	- Implicit Protocol
	- Implicit Domain Name
-  Full URL：
	- 該資源在網路上的完整位置
	- 主要由protocol、host、port、path所構成
	- 格式：
```
protocol://host:port/path
```
- Implicit protocol：
	- 以暗示方式來指定protocol是什麼的情況下來指定其資源所在的完整位置，即為該資源在特定協定網路下的完整位置
	- 其中指定資源的protocol會採用目前所在的資源之完整位置所擁有的protocol
	- 主要由host、port、path所構成，格式為
```
//host:port/path
```
-  implicit domain name：
	- 以暗示方式來指定特定協定網路之特定主機是什麼的情況下來指定其資源所在的完整位置，即為該資源在特定協定網路之特定主機下的完整位置
	- 其中指定資源的protocol 和 domain name會採用於目前所在的資源之完整位置所擁有的protocol、domain name
	- 主要由path所構成，格式為
```
/path
```


#### 案例

Full URL
```
https://developer.mozilla.org/en-US/docs/Learn
```

 Implicit protocol 案例：假設目前存取的資源所擁有的protocol會是https，因此會是對應到第一個URL
```
//developer.mozilla.org/en-US/docs/Learn
```

 implicit domain name 案例：假設目前存取的資源所擁有的protocol和domain會是https和developer.mozilla.org，因此會對應到第一個URL
```
/en-US/docs/Learn
```


## 複習
#🧠  absolute URL 是什麼？ ->->-> `意指為特定資源在網路上的完整位置`

#🧠  absolute URL 是為特定資源在網路上的完整位置，它包含了什麼？->->-> `該資源在網路上的完整位置、該資源在特定協定網路下的完整位置、該資源在特定協定網路之特定主機下的完整位置`


#🧠  absolute URL 有哪三種形式？簡答 ->->-> `	- Full URL - Implicit Protocol - Implicit Domain Name`

#🧠 absolute URL 有哪三種形式？Full URL是什麼？ ->->-> `該資源在網路上的完整位置、`

#🧠 absolute URL 有哪三種形式？Full URL是什麼？由何種構成？ 格式？ ->->-> `	- 該資源在網路上的完整位置 - 主要由protocol、host、port、path所構成 - 格式：protocol://host:port/path`

#🧠 absolute URL 有哪三種形式？ Implicit protocol是什麼？ ->->-> ``

#🧠 Question :: ->->-> ``

#🧠 Question :: ->->-> ``



---
Status: #🌱 
Tags:
Links:
References:
[[@mdnWhatURLLearn]]