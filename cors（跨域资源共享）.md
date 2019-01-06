## 简介
> CORS是一个W3C标准，全称是"跨域资源共享"（Cross-origin resource sharing）。
当一个资源从与该资源本身所在的服务器不同的域或端口请求一个资源时，资源会发起一个跨域 HTTP 请求。
 
- 比如，站点 http://domain-a.com 的某 HTML 页面通过 <img> 的 src 请求 http://domain-b.com/image.jpg。网络上的许多页面都会加载来自不同域的CSS样式表，图像和脚本等资源。
 
==出于安全策略，浏览器本身会限制从脚本内发起的跨源HTTP请求。 XMLHttpRequest和Fetch API遵循同源策略。 这意味着使用这些API的Web应用程序只能从加载应用程序的同一个域请求HTTP资源，除非使用CORS头文件。==

## 两种请求
> 浏览器将 CORS 请求分成两类：简单请求（simple request）和非简单请求（not-so-simple request）。
### 简单请求
> 某些请求不会触发 CORS 预检请求。这样的请求被称为“简单请求” 

1.使用下列方法请求

 - HEAD
 - GET
 - POST

2.HTTP的头信息不超出以下几种字段，（不得人为设置该集合之外的其他首部字段）
- [Accept](https://developer.mozilla.org/zh-CN/docs/Web/HTTP/Headers/Accept)
- [Accept-Language](https://developer.mozilla.org/zh-CN/docs/Web/HTTP/Headers/Accept-Language)
- [Content-Language](https://developer.mozilla.org/zh-CN/docs/Web/HTTP/Headers/Content-Language)
- [Last-Event-ID](https://developer.mozilla.org/en-US/docs/Web/API/MessageEvent/lastEventId)
- [Content-Type](https://developer.mozilla.org/zh-CN/docs/Web/HTTP/Headers/Content-Type)：只限于三个值 application/x-www-form-urlencoded、multipart/form-data、text/plain

3.请求中的任意 [XMLHttpRequestUpload](https://developer.mozilla.org/zh-CN/docs/Web/API/XMLHttpRequest/upload) 对象均没有注册任何事件监听器；（XMLHttpRequestUpload 对象可以使用 XMLHttpRequest.upload 属性访问。）

4.请求中没有使用 [ReadableStream](https://developer.mozilla.org/zh-CN/docs/Web/API/ReadableStream) 对象。

### 预检请求

> 非简单请求是那种对服务器有特殊要求的请求，比如请求方法是PUT或DELETE，或者Content-Type字段的类型是application/json。

非简单请求的CORS请求，会在正式通信之前，增加一次HTTP查询请求，称为"==预检=="请求（preflight）。

> 一旦服务器通过了"预检"请求，以后每次浏览器正常的CORS请求，就都跟简单请求一样，会有一个Origin头信息字段。服务器的回应，也都会有一个Access-Control-Allow-Origin头信息字段。

浏览器先询问服务器，当前网页所在的域名是否在服务器的许可名单之中，以及可以使用哪些HTTP动词和头信息字段。只有得到肯定答复，浏览器才会发出正式的XMLHttpRequest请求，否则就报错。

1.使用下列方法请求
- PUT
- DELETE
- OPTIONS
- TRACE
- PATCH

2.认为改动下列的请求参数

- Accept
- Accept-Language
- Content-Language
- Content-Type (排除上面提到的，简单请求中的三种请求)
- DPR
- Downlink
- Save-Data
- Viewport-Width
- Width

3.请求中的 ``XMLHttpRequestUpload`` 对象注册了任意多个事件监听器。

4.请求中使用了 ``ReadableStream`` 对象。

