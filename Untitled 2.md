## 描述

### SGML vs. XML vs. HTML

[[@guolijiaotongdaxueXMLYuHTML]] 所描述：
> SGML（標準通用標示語言Standard Generalized Markup Language） [<註一>](http://yes.nctu.edu.tw/Lecture/NewTech/C05_NewEra/XML/IntroXML/chapter2.html#ps) 語法簡化而來的子集，SGML是屬與功能強大的標示、管理和排版語言。那為什麼不用 SGML呢？因為它的結構太複雜了，所以在1991年由Tim Berners-Lee建立了HTML語法，簡單易學，也使得今日網路上的資訊能 夠快速傳播，互相共享。但是後來被認為HTML語法太過於鬆散，不夠嚴謹，所以才有目前的XML出現，算是青出於藍的孫子輩， 它可說是取SGML之長補HTML之短。


[[@heshijunFengSiXin65TiaoXiaoXi]] 所描述：
>  XML是以 SGML 的格式精簡後制定出來的，制定者當然是全球資訊網協會 (World Wide Web Consortium，W3C)。XML是SGML 的一個子集合，誕生的目的是為了擴充網路的應用、靡補 HTML 的不完美， 以及讓 SGML 也能容易地在網路上應用。所以XML肩負著使得全球資訊網能夠傳輸或處理更豐富資訊的責任。
>   
>  在一般情況之中， HTML或是 JAVA 就已經相當夠用了，但隨著資訊的擴充，資料量的暴增，與資料的複雜化，HTML就顯得捉襟肘見，而 JAVA 又 顯得大才小用且不易學習。有了XML 與 HTML 的相輔相成，這些問題就解決了。所以 XML 並不是用來終結 HTML，取代 SGML，而或是廢除舊的標準。XML是用來制定新的標準、用來定義一種新的標記語言。 XML是一種用來定義其它語言的另一種語法系統，這正是XML功能強大的主因。


> 当初HTML是SGML的一个应用（意思是SGML可以有许多应用，比如docbook最初也是SGML的一个应用），而XML是简化了的SGML并用来取代SGML的。而XHTML就是HTML从SGML转用XML语法的结果。所以它们是有关系，但不是同个层面的东西。

> 注意今天的HTML已经不是当初意义上的HTML了（包含了当初的html/xhtml/dom等许多标准和api，而不是单单一个语言词汇集的定义），所以关系又弱了一层。



重點：
- SGML (Standard Gerneralized Markup Language) 是傳統標籤語言，基於其語言特性而衍生出來的標籤語言HTML，換言之，基於SGML特性建立的應用
- XML 則是將SGML格式精簡後制訂出來的標籤語言，其中HTML從SGML轉換成以XML為基礎而建構的應用就是XHTML
- SGML 和 XML 皆由W3C制定
- 現今的HTML 標準支援著有 **以SGML特性建立的HTML**、**以XML特性建立的XHTML**、**DOM標準**，所以並不是純粹以SGML作為基礎。
  
### 舉例

> 在一般情況之中， HTML或是 JAVA 就已經相當夠用了，但隨著資訊的擴充，資料量的暴增，與資料的複雜化，HTML就顯得捉襟肘見，而 JAVA 又 顯得大才小用且不易學習。有了XML 與 HTML 的相輔相成，這些問題就解決了。所以 XML 並不是用來終結 HTML，取代 SGML，而或是廢除舊的標準。XML是用來制定新的標準、用來定義一種新的標記語言。 XML是一種用來定義其它語言的另一種語法系統，這正是XML功能強大的主因。

[[@guolijiaotongdaxueXMLYuHTML]] 所描述：
> 舉例來說，下面這段HTML碼，將成績結果以table的方式呈現：



> 如上所見，HTML的問題正出在，HTML的標籤大多是設計來呈現文章的格局(layout)和外觀的，譬如像上例中的\<br\>、 \<table\>、\<td\>，還有像\<ul\>、\<ol\>、\<li\>、\<font\>等標籤比比皆是。但是在某些情況下， 同一種資料可能有很多種表示法，如在此是用\<tr\>、\<td\>等方式呈現，但是在另一個地方可能用完全不同的方法 呈現(如用\<ul\>、\<li\>...\</u\l>的條列方法)，如此的話，若想要用程式將這些不同網頁中相同的資料整合 起來的話將是一件十分困難的工作，因為不知道此標籤所代表的真正意義。更別提想將這些各式各樣的網頁去蕪存菁，找出關 鍵資訊，達成任務了。如果這些網頁的功能只是單純地提供人類閱讀，消化，那就沒有問題了(假設一切都排列整齊)；但在資 訊爆炸的網路世界，人類需要仰賴機器來替我們分憂解勞，以HTML碼來標注的資訊，對機器和寫程式的人來說，處理起來實在 是太沒有效率了。

 > 此時若是利用XML，則可以將此成績結果以下列的方式呈現：

> 我們可以發現XML的標籤竟然是中文的，這就是XML與HTML最大的不同點。在XML中，我們可以自由訂定標籤。定義出來的標籤， 可以按自己的意思充分表達文件的內容。在XML中，著重在內容，這與強調佈局的HTML十分地不同。至於XML外觀的呈現，可透 過搭配 CSS 或是 XSLT 來做 XML 轉 HTML 或其他格式的轉換。[<註二>](http://yes.nctu.edu.tw/Lecture/NewTech/C05_NewEra/XML/IntroXML/chapter2.html#ps1)

> 總而言之，XML的功能在於強化HTML，所以他的格式與HTML比較起來還要嚴謹。如果你有一些寫HTML文件的經驗，你更應該 仔細研究XML元素的規則。HTML可以容忍的事，對XML卻行不通。一些應該要注意的重要改變如下：


```
- XML的元素名稱有分大小寫。HTML的標籤不分大小寫。
- XML的元素永遠都需要起始標籤和結尾標籤。另方面，HTML的元素在某些情況下，可以不寫結尾標籤。
- XML空元素需要在右箭號前面加一個斜線(如 <example/>)。然而，HTML只用一個單獨的起始標籤即可，沒有終結的斜線。
-  XML元素視空白為內容的一部分，除非特別明講，否則會予以保留。但在HTML中，大部分的元素都會拋棄多餘的空白，當 瀏覽器在排定內容的格式時，會予以斷行。
```


> 與許多HTML元素不同的是，XML元素的基礎是其功能，而非其格式。你不應該根據標記，就假定任何的格式或樣式。相反地， XML把版面配置留給樣規。樣規是獨立的文件，把元素配上樣式。
## 複習
#🧠 Question :: ->->-> ``

---
Status: #🌱 
Tags:
[[HTML]] - [[XML]]
Links:
References:
[[@guolijiaotongdaxueXMLYuHTML]]
[[@heshijunFengSiXin65TiaoXiaoXi]]