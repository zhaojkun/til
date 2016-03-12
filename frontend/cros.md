# 跨域访问

Date: 2016-03-11

Tag: js 跨域 html frame cors

只要协议、域名、端口有任何一个不同，都被当作是不同的域。

跨域访问有如下几种方式：

### 跨域资源共享CORS

COS（Cross-Origin Resource Sharing）跨域资源共享，定义了必须在访问跨域资源时，浏览器与服务器应该如何沟通。`CORS`背后的基本思想就是使用自定义的HTTP头部让浏览器与服务器进行沟通，从而决定请求或响应是应该成功还是失败。

服务器端对于`CROS`的支持，主要就是通过设置`Access-Control-Allow-Origin`来进行的，如果浏览器检测到相应的设置，就可以允许Ajax进行跨域访问。

### jsonp

`JSONP`由两部分组成：回调函数和数据。回调函数是当响应到来时应该在页面中调用的函数，而数据就是传入回调函数中的JSON数据。`JSONP`利用的是在页面上引入不同域上的js脚本来实现。

Cros与JSON的对比：
* JSONP只能实现GET请求，而CORS支持所有类型的HTTP请求
* 使用CORS，开发者可以使用普通的`XMLHttpRequst`发起秦秋和获得数据，比起`JSONP`有更好的错误处理
* `JSONP`主要被老的浏览器支持，它们往往不支持CORS，而绝大多数现代浏览器都支持了`CORS`

### iframe

* 通过修改`document.domain`来跨域，值得注意的是，`document.domain`的设置是有限制的，我们只能把document.domain设置成自身或更高一级的父域，且主域必须相同。修改之后就可以进一步获取dom和js
* 使用`window.name`来进行跨域，只要不关闭浏览器,`window.name`可以在不同页面加载后依然保持。
* location.hash 较为常用，把传递的数据依附在url上
* postMessage，HTML5新增的方法。跨文档消息传输

参考文献：
* https://segmentfault.com/a/1190000000718840
* http://www.cnblogs.com/rainman/archive/2011/02/20/1959325.html
* https://segmentfault.com/a/1190000000702539