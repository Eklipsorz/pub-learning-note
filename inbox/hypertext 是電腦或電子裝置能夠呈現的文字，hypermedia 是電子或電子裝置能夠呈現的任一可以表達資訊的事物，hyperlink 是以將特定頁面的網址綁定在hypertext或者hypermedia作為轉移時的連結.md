## 描述

### Hypermedia 命名緣由


> a combination of videos, images, sounds, text, etc. that are connected together on a website, which you can click on in order to use them or to go to other related videos, websites, etc.:


> Hypermedia enables us to link text to text, text to image, and image to image, on both a macro and micro level.

[[@wikidataHypermedia2022]]
> Hypermedia, an extension of the term hypertext, is a nonlinear medium of information that includes graphics, audio, video, plain text and hyperlinks.

重點：
1. hypertext的延伸版本，能夠以多媒體來綁定特定的hyperlink，多媒體包含的形式可以是文字、圖片、聲音、影片等等
2. 當多媒體發生事件觸發時，就會按照綁定的hyperlink對應的頁面來將使用者導向其頁面
3. 例子：在這裡假設一張圖片會跟http://example.com做綁定，當使用者點擊該圖片時，就會將使用者導向至http://example.com的頁面。


重點：
- hypermedia 意旨超出media意義範疇的media，原本media意義範疇是指原本僅能在特定事物上才能呈現和修改的事物，比如原本只能在紙張呈現的文字、圖片或者只能在播放機播放音樂。在這裡會是指能夠在電腦/電子裝置呈現的文字、圖片、影片、聲音
- media 源自於表達資訊的圖片、報紙、影片、音樂
[[medium 為傳遞或表達特定事物的任一方法或形式，比如表達資訊的圖片、報紙、影片，其中media為單數，medium為複數]]
- 用途：
	- 內容呈現
	- 當成hyperlink來使用

#### hypertext vs. hypermedia vs. hyperlink

1. hypertext 是電腦/電子裝置能夠呈現的文字
2. hypermedia 是電子/電子裝置能夠呈現的任一可以表達資訊的事物，如文字、圖片
3. hyperlink 是以將特定頁面的網址綁定在hypertext或者hypermedia作為轉移時的連結

### hyperlink

[[@HyperlinkVsHypertext2020]]
> The hyperlink contains the URL of the webpages.

[[@wikidataHyperlinkWikipedia]]
>  a hyperlink, or simply a link, is a digital reference to data that the user can follow or be guided by clicking or tapping

1. 一個指向於特定網頁頁面X的連結，該連結通常會包含該頁面X的所在位置(如URI)
2. 通常會綁定一組超文字(Hypertext)，當超文字被某事件觸發(點擊)時就會按照綁定的連結來將使用者導向指定頁面X

重點：
- hyperlink 意指為超出連結意義範疇的連結，原本連結意義範疇是單純指特定事物A與特定事物B之間的連結，在這是指連結是直接允許對特定事物A進行互動，來轉移至特定特定事物B
- 在網頁上的具體連結實現：
	- 連結會是綁定著特定頁面網址的文字/圖片/影片/超媒體，當文字/圖片/影片/超媒體上發生事件就會轉移至網址。
	 - 連結會是綁定著特定頁面網址的文字/圖片/影片/超媒體 中的文字/圖片/影片/超媒體皆為能夠在電腦/電子裝置上呈現的文字/圖片/影片/超媒體


### Hypertext
[[@HyperlinkVsHypertext2020]]
> Hypertext is a text which contains the visible text to redirect the targeted page(page URL contained by Hyperlink)

[[@wikidataHypertext2022]]
> Hypertext is text displayed on a computer display or other electronic devices with references (hyperlinks) to other text that the reader can immediately access.


1. 一個能夠在電腦/電子裝置上顯示的可見文字，並綁定特定的hyperlink
2. 當hypertext上發生事件時，就會按照綁定hyperlink對應的頁面來將使用者導向其頁面
3. 例子：假設以text作為hypertext來與http://example.com進行hyperlink的綁定，而其hyperlink會是http://example.com，當使用者點擊text，就會將使用者導向至該頁面。

```
<a src="http://example.com">text</a>
```


重點：
- hypertext 意指為超出文字意義範疇的文字，原本文字意義範疇是指只能在紙才能寫上文字或者呈現文字，在這是指文字是呈現在無形介質下或者呈現在電腦/電子裝置上
- 用途為：
	- 作為內容呈現
	- 當成hyperlink使用


#### hyperlink vs. hypertext

1. hyperlink 會是綁定著特定頁面網址的文字/圖片/影片；hypertext 是指呈現在電腦上或者電子裝置上的文字


### hyper 命名緣由

> Hyper- is used to form adjectives that describe someone as having a lot or too much of a particular quality.

重點：
- Hyper 是形容某事物A超出特定程度的範疇


## 複習

#🧠 hyper 命名緣由為何？ ->->-> `Hyper 是形容某事物A超出特定程度的範疇`
<!--SR:!2024-04-18,330,250-->

#🧠 hypertext 命名緣由為何？ ->->-> `hypertext 意指為超出文字意義範疇的文字，原本文字意義範疇是指只能在紙才能寫上文字或者呈現文字，在這是指文字是呈現在無形介質下或者呈現在電腦/電子裝置上`
<!--SR:!2024-01-20,277,250-->

#🧠 hypertext 的用途為何？->->-> `	- 作為內容呈現 - 當成hyperlink使用`
<!--SR:!2024-01-27,283,250-->


#🧠 hyperlink 命名緣由為何？ ->->-> ` hyperlink 意指為超出連結意義範疇的連結，原本連結意義範疇是單純指特定事物A與特定事物B之間的連結，在這是指連結是直接允許對特定事物A進行互動，來轉移至特定特定事物B`
<!--SR:!2023-08-10,186,250-->

#🧠 hyperlink在網頁上的具體連結實現是什麼？ (請說明互動會有什麼動作) ->->-> `連結會是綁定著特定頁面網址的文字/圖片/影片/超媒體，當文字/圖片/影片/超媒體上發生事件就會轉移至網址。`
<!--SR:!2024-09-02,417,250-->

#🧠 hyperlink在網頁上的具體連結實現是什麼？ ->->-> `連結會是綁定著特定頁面網址的文字/圖片/影片/超媒體，當文字/圖片/影片/超媒體上發生事件就會轉移至網址。`
<!--SR:!2024-03-16,249,230-->

#🧠 hyperlink在網頁上的具體連結實現是綁定著特定頁面網址的文字/圖片/影片/超媒體，那麼文字/圖片/影片/超媒體會是指什麼？ ->->-> `能夠在電腦/電子裝置上呈現的文字/圖片/影片/超媒體`
<!--SR:!2023-10-27,156,190-->

#🧠 hypelink vs. hypertext 差異是什麼？->->-> `hyperlink 會是綁定著特定頁面網址的文字/圖片/影片；hypertext 是指呈現在電腦上或者電子裝置上的文字`
<!--SR:!2023-07-23,173,250-->

#🧠 hypelink vs. hypertext vs. hypermedia 差異是什麼？ ->->-> `1. hypertext 是電腦/電子裝置能夠呈現的文字 2. hypermedia 是電子/電子裝置能夠呈現的任一可以表達資訊的事物，如文字、圖片 3. hyperlink 是以將特定頁面的網址綁定在hypertext或者hypermedia作為轉移時的連結`
<!--SR:!2024-04-06,327,250-->

#🧠 hypermedia 中的media源自於哪裡？->->-> `表達資訊的圖片、報紙、影片、音樂`
<!--SR:!2024-02-02,285,250-->

#🧠 hypermedia 命名緣由為何？->->-> `hypermedia 意旨超出media意義範疇的media，原本media意義範疇是指原本僅能在特定事物上才能呈現和修改的事物，比如原本只能在紙張呈現的文字、圖片或者只能在播放機播放音樂。在這裡會是指能夠在電腦/電子裝置呈現的文字、圖片、影片、聲音`
<!--SR:!2023-08-19,191,250-->

#🧠 hypermedia 用途是什麼？ ->->-> `	- 內容呈現 - 當成hyperlink來使用`
<!--SR:!2023-08-19,191,250-->


---
Status: #🌱 
Tags:
Links:
[[medium 為傳遞或表達特定事物的任一方法或形式，比如表達資訊的圖片、報紙、影片，其中media為單數，medium為複數]]
References:
[[@HyperlinkVsHypertext2020]]
[[@wikidataHypertext2022]]
[[@wikidataHyperlinkWikipedia]]