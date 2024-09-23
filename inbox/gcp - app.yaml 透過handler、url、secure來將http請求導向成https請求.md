

## 描述

### handlers 用途 和 URL

[[@gcpAppYamlConfiguration]] 所描述
> `handlers`: Optional. A list of URL patterns and descriptions of how they should be handled. App Engine can handle URLs by executing application code, or by serving static files uploaded with the code, such as images, CSS, or JavaScript.

> `url` Required element under `handlers`. The URL pattern, as a regular expression.


重點：
- handlers 是在app.yaml定義了app engine所要處理的URL是哪些(會以app engine所在的DOMAIN為主)以及這些URL該如何處理
- url 是handlers用來定義哪些URL要被處理，格式會是以正規表達式來處理
- 舉例： 在這裡會以url作為區分，總共分成三種URL格式要處理，每種都有各自要被處理的設定，這三種分別為
	- host/：只要請求會是以host/作為前綴就會被處理，比如host/hi、host/hi2
	- host/example1/：只要請求會是以host/example1/作為前綴就會被處理，比如host/example1/hi、host/example1/hi2
	- host/example2/：只要請求會是以host/example2/作為前綴就會被處理，比如host/example2/hi、host/example2/hi2
```
handlers:
- 	url: /example1/.*
	static_files: static/\1  
	upload: static/.*\.(gif|png|jpg)$  
  
- 	url: /example2/.*
	script: auto
	
- 	url: /.*
	secure: always
	redirect_http_response_code: 301
	script: auto
	

```


### secure 和 redirect_http_response_code

> `secure` Optional. Any URL handler can use the `secure` setting, including script handlers and static file handlers. The `secure` element has the following possible values:

> `always`: Requests for a URL that match this handler that do not use HTTPS are automatically redirected to the HTTPS URL with the same path. Query parameters are preserved for the redirect.

> `redirect_http_response_code` Optional. `redirect_http_response_code` is used with the `secure` setting to set the HTTP response code returned when performing a redirect required by how the `secure` setting is configured. `redirect_http_response_code` element has the following possible values:

重點：
- secure 是指定要不要將http請求導向成https，若是always就是會把http請求自動導向https
- redirect_http_response_code 則是指定將http導向至https的回應封包內含的code為特定特代碼，具體會有301

### script 
> `script` Optional. Specifies that requests to the specific handler should target your app. The only accepted value for the `script` element is `auto` because all traffic is served using the entrypoint command. In order to use static handlers, at least one of your handlers must contain the line `script: auto` or define an `entrypoint` element to deploy successfully.

重點：
- script 指定所有指向特定handler的請求應該針對著目前的app engine來處理，預設只有auto

## 複習


#🧠 GCP App專案下要如何讓使用者瀏覽http的端點時能夠自動轉換成https的端點，能夠實現其設定的檔案會是什麼？其概念為何？ ->->-> `app.yaml，主要概念為替所有http的請求端點自動轉換成https的對應端點`
<!--SR:!2024-04-24,281,250-->



#🧠 app.yaml 中的handlers 是做什麼用的->->-> `是在app.yaml定義了app engine所要處理的URL是哪些(會以app engine所在的DOMAIN為主)以及這些URL該如何處理`
<!--SR:!2025-02-13,576,250-->

#🧠 app.yaml 中的handlers 以什麼來區分各個需要處理的URL，會用到什麼語法(正規？) ->->-> `使用- url: 正規表達式`
<!--SR:!2024-04-03,388,250-->

app.yaml 中的secure 是做什麼用的 ->->-> ` 是指定要不要將http請求導向成https，若是always就是會把http請求自動導向https`
<!--SR:!2025-03-09,167,230-->

---
Status: #🌱 
Tags:
[[GCP]]
Links:
References:
[[@gcpAppYamlConfiguration]]

