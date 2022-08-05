

## 描述

[[@mdnCSSPreprocessorMDN]] 所描述的：preprocessor
> A CSS preprocessor is a program that lets you generate CSS from the preprocessor's own unique syntax.


> A few of most popular CSS preprocessors:
> - Sass
> - LESS
> - Stylus
> - PostCSS

[[@huliXinDeShiMoShiPostcss]] 所描述的：preprocessor vs. postprocessor
> 簡單來說，預處理器是你把一些長得很像css但不是css的東西丟給它，處理過後會給你編譯過後的css  
> 
	而css再經過後處理器，透過一些規則幫它加上一些東西，最後產生出完成品！

重點：
- CSS preprocessor 是一個程式，能透過preprocessor提供的語法編譯成CSS
- CSS preprocessor 具體會是會於確定CSS檔案的程式之前，來將preprocessor提供的語法所構成的檔案經過preprocesssor處理後而產生出對應的CSS
- CSS postprocessor 是一個程式，主要會接收CSS原檔並根據指定規則來將CSS轉換成另一種CSS
- CSS postprocessor 具體會是在確定CSS檔案的程式之後，來將確定CSS檔案的程式輸出出來的CSS當作輸入，並將輸入丟至postprocessor來根據指定規則來將CSS轉換成另一種CSS
[[@ithomeDAY13PostprocessorPostCss]] 所描述：
![](https://i.imgur.com/VCgqqTv.png)
- CSS preprocessor vs. CSS postprocessor ：
	- 執行順序：前者會於確定CSS檔案的程式之前執行，後者會於確定CSS檔案的程式之後執行
	- 輸入資料：前者會使用由preprocessor語法構成的檔案來處理，後者則是用確定CSS檔案的程式之處理結果來處理
	- 處理方式：前者是將輸入編譯成CSS，後者則是按照指定規則來將輸入轉換成另一種形式的CSS
### preprocessor 命名緣由

[[@wikidataPreprocessor2022]]
> In computer science, a preprocessor (or precompiler)[1] is a program that processes its input data to produce output that is used as input to another program. 
> 
> The output is said to be a preprocessed form of the input data, which is often used by some subsequent programs like compilers.


重點：
- 在電腦科學裡，preprocessor 是一種程式A，用來處理輸入資料並產生出執行其他程式B所需要的輸入資料，對於程式B而言，程式A是先於它來處理資料並將結果當作是執行程式B的輸入資料
- 執行順序為：preprocessor -> processor 
- 若是探討postprocessor的話，在這裡會是指將程式B的處理結果當作執行程式C的輸入資料，並由程式C來處理最後的結果，而程式C會是指postprocessor



## 複習
#🧠 Question :: ->->-> ``
<!--SR:!2022-08-08,3,250-->

---
Status: #🌱 
Tags:
[[CSS]] - [[Operating System]]
Links:
References:
[[@mdnCSSPreprocessorMDN]]
[[@wikidataPreprocessor2022]]
[[@huliXinDeShiMoShiPostcss]]
[[@ithomeDAY13PostprocessorPostCss]]