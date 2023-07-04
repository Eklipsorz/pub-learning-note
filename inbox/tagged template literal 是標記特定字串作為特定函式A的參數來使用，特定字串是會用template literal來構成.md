## 描述

### tagged template literal 
[[@mdnTemplateLiteralsTemplate]]
> Tagged templates

> A more advanced form of template literals are tagged templates.
>
> Tags allow you to parse template literals with a function. The first argument of a tag function contains an array of string values. The remaining arguments are related to the expressions.
>
> The tag function can then perform whatever operations on these arguments you wish, and return the manipulated string. (Alternatively, it can return something completely different, as described in one of the following examples.)

```
var person = 'Mike';
var age = 28;

function myTag(strings, personExp, ageExp) {

  var str0 = strings[0]; // "that "
  var str1 = strings[1]; // " is a "

  // There is technically a string after
  // the final expression (in our example),
  // but it is empty (""), so disregard.
  // var str2 = strings[2];

  var ageStr;
  if (ageExp > 99){
    ageStr = 'centenarian';
  } else {
    ageStr = 'youngster';
  }

  return str0 + personExp + str1 + ageStr;

}

var output = myTag`that ${ person } is a ${ age }`;

console.log(output);
// that Mike is a youngster
```

重點：
- tagged template literal 算是一種 template literal
- tagged template literal 是標記特定字串作為特定函式A的參數來使用，特定字串是會用template literal來構成，整體形式為如下，其中functionName為函式A的名稱
```
functionName`<template literal>`
```

- 系統把沒用\$\{\}特別包住的字串結合成一個字串當作特定函式A的第一個參數，剩下後續參數都擷取\$\{\}，比如說
	- myTag會是函式，其宣告為function myTag(strings, argu1, argu2, ...)
	- 沒用\$\{\}特別包住的字串結合成一個字串當作特定函式A的第一個參數，that is a ，該字串會用字串陣列來儲存
	- 第二個參數就取\$\{person\}
	- 第三個參數就取\$\{age\}
```
myTag`that ${ person } is a ${ age }`
```
- 特定函式A的回傳值為任意型別的資料，沒回傳就undefined
## 複習

#🧠 tagged template literal  是算 template literal 嗎？ ->->-> `算`
<!--SR:!2024-10-04,459,250-->

#🧠 tagged template literal是什麼？->->-> `是標記特定字串作為特定函式A的參數來使用，特定字串是會用template literal來構成`
<!--SR:!2024-10-14,472,250-->

#🧠 tagged template literal 的形式是什麼->->-> `functionName(反引號)<template literal>(反引號)`
<!--SR:!2023-06-25,184,250-->

#🧠 tagged template literal 是由什麼構成 ->->-> `tag function和特定字串`
<!--SR:!2023-07-08,194,250-->

#🧠 tag function 要如何把template literal 中的內容當作參數來使用？ ->->-> `沒用\$\{\}特別包住的字串結合成一個字串當作特定函式A的第一個參數，that is a ，該字串會用字串陣列來儲存、剩下後續參數都擷取\$\{\}`
<!--SR:!2023-07-04,190,250-->

#🧠 myTag\`that \$\{ person \} is a \$\{ age \}\` ，以這個為例，說明一下哪個是tag function，如何取參數？->->-> `myTag會是函式，其宣告為function myTag(strings, argu1, argu2, ...)、沒用\$\{\}特別包住的字串結合成一個字串當作特定函式A的第一個參數，that is a ，該字串會用字串陣列來儲存、第二個參數就取\$\{person\}、第三個參數就取\$\{age\}`
<!--SR:!2024-09-07,443,250-->


#🧠 tagged template literal中的tag function會是回傳什麼型別的資料？ ->->-> `任意型別的資料`
<!--SR:!2024-09-04,440,250-->
#🧠 tagged template literal中的tag function若沒指定回傳，那麼會回傳什麼？ ->->-> `undefined`
<!--SR:!2024-10-07,461,250-->

---
Status: #🌱 
Tags:
[[JS]]
Links:
References:
[[@mdnTemplateLiteralsTemplate]]