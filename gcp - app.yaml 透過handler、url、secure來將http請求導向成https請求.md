

## 描述

> `handlers`: Optional. A list of URL patterns and descriptions of how they should be handled. App Engine can handle URLs by executing application code, or by serving static files uploaded with the code, such as images, CSS, or JavaScript.

```
handlers:
- 	url: /.*
	secure: always
	redirect_http_response_code: 301
	script: auto
	
- 	url: /(.*\.(gif|png|jpg))$  
	static_files: static/\1  
	upload: static/.*\.(gif|png|jpg)$  
  
- 	url: /.*  
	script: auto
```

## 複習
#🧠 Question :: ->->-> ``

---
Status: #🌱 
Tags:
[[GCP]]
Links:
References:

