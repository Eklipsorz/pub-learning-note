## 描述



### parser blocking 
> Imagine an HTML page has two `<script src="...">` elements. The parser sees the first one. It has to stop* parsing while it fetches and then executes the javascript, because it might contain `document.write()` method calls that fundamentally change how the subsequent markup is to be parsed. 
> 
> Fetching resources over the internet is comparatively much slower than the other things the browser does, so it sits waiting with nothing to do. Eventually the JS arrive, executes and the parser can move on. It then sees the second `<script src="...">` tag and has to go through the whole process of waiting for the resource to load again. It's a sequential process, and that's parser blocking.


重點：
- parser blocking：停止


> CSS resources are different. When the parser sees a stylesheet to load, it issues the request to the server, and moves on. If there are other resources to load, these can all be fetched in parallel (subject to some HTTP restrictions). 
> 
> But only when the CSS resources are loaded and ready can the page be painted on the screen. That's render blocking, and because the fetches are in parallel, it's a less serious slow down.

> * Parser blocking is not quite as simple as that in some modern browsers. They have some ability to tentatively parse the following HTML in the hope that the script, when it loads and executes, doesn't do anything to mess up the subsequent parsing, or if it does, that the same resources are still required to be loaded. But they can still have to back out the work if the script does something awkward.


## 複習
#🧠 Question :: ->->-> ``

---
Status: #🌱 
Tags:
[[JavaScript]]
Links:
References:
