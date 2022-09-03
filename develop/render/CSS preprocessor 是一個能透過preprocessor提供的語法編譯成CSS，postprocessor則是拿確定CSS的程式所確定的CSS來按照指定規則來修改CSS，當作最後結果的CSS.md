

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
- CSS preprocessor 是一個程式，能透過preprocessor提供的語法編譯成CSS的程式
- CSS preprocessor 具體會是會於確定正式使用哪一個CSS檔案之前，來將preprocessor提供的語法所構成的檔案經過preprocesssor處理後而產生出對應的CSS，並指定使用該結果-CSS作為正式使用的CSS
- CSS postprocessor 是一個程式，主要會接收CSS原檔並根據指定規則來將CSS轉換成另一種CSS的程式
- CSS postprocessor 具體會是在確定使用哪一個CSS檔案之後，來將正式確定使用的CSS檔案當作輸入，並將輸入丟至postprocessor來根據指定規則來將CSS轉換成另一種CSS
[[@ithomeDAY13PostprocessorPostCss]] 所描述：
![](https://i.imgur.com/VCgqqTv.png)
- CSS preprocessor vs. CSS postprocessor ：
	- 執行順序：前者會於確定使用CSS檔案之前執行，後者會於確定CSS檔案之後執行
	- 輸入資料：前者會使用由preprocessor語法構成的檔案來處理，後者則是用原本要正式使用的CSS檔案當作輸入
	- 輸出資料：前者是將由preprocessor語法構成的檔案編譯成CSS，後者則是按照指定規則來將輸入轉換成另一種形式的CSS

### preprocessor 命名緣由

[[@wikidataPreprocessor2022]]
> In computer science, a preprocessor (or precompiler)[1] is a program that processes its input data to produce output that is used as input to another program. 
> 
> The output is said to be a preprocessed form of the input data, which is often used by some subsequent programs like compilers.


重點：
- 在電腦科學裡，
- preprocessor 是一種程式A，是在產生特定結果的程式B之前所會執行的程式A，並將程式A結果當作程式B的輸入來處理 
- 執行順序為：preprocessor -> processor 
- 若是探討postprocessor的話，會是指特定結果下的後製處理程式，在這裡會是指將程式B的處理結果當作執行程式C的輸入資料，並由程式C來處理最後的結果，而程式C會是指postprocessor



## 複習
#🧠 preprocessor 是指什麼？ ->->-> `preprocessor 是一種程式A，是在產生特定結果的程式B之前所會執行的程式A，並將程式A結果當作程式B的輸入來處理 `
<!--SR:!2022-09-28,26,250-->


#🧠 postprocessor 是指什麼？ ->->-> `若是探討postprocessor的話，會是指特定結果下的後製處理程式，在這裡會是指將程式B的處理結果當作執行程式C的輸入資料，並由程式C來處理最後的結果，而程式C會是指postprocessor`
<!--SR:!2022-09-18,18,250-->


#🧠 CSS preprocessor 是什麼？ ->->-> `CSS preprocessor 是一個程式，能透過preprocessor提供的語法編譯成CSS的程式`
<!--SR:!2022-09-16,28,250-->

#🧠 請從為何取preprocessor 來說明CSS preprocessor是什麼？ ->->-> `具體會是會於確定CSS檔案的程式之前，來將preprocessor提供的語法所構成的檔案經過preprocesssor處理後而產生出對應的CSS`
<!--SR:!2022-09-13,26,250-->

#🧠 CSS postprocessor 是什麼？->->-> `CSS postprocessor 是一個程式，主要會接收CSS原檔並根據指定規則來將CSS轉換成另一種CSS的程式`
<!--SR:!2022-09-12,25,250-->

#🧠 請從為何取postprocessor 來說明CSS postprocessor是什麼？ ->->-> `具體會是在確定使用哪一個CSS檔案之後，來將正式確定使用的CSS檔案當作輸入，並將輸入丟至postprocessor來根據指定規則來將CSS轉換成另一種CSS`
<!--SR:!2022-10-01,28,250-->



#🧠 畫圖來說明CSS preprocessor、CSS、CSS postprocessor的關係 ->->-> `![](https://i.imgur.com/VCgqqTv.png)`
<!--SR:!2022-09-15,27,250-->

#🧠 CSS preprocessor 和 CSS postprocessor的關係這兩者的差別是什麼？(有三個) ->->-> `- 執行順序：前者會於確定使用CSS檔案之前執行，後者會於確定CSS檔案之後執行 - 輸入資料：前者會使用由preprocessor語法構成的檔案來處理，後者則是用原本要正式使用的CSS檔案當作輸入 - 輸出資料：前者是將由preprocessor語法構成的檔案編譯成CSS，後者則是按照指定規則來將輸入轉換成另一種形式的CSS`
<!--SR:!2022-09-03,10,250-->


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