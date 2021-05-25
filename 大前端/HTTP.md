# HTTP

[「查缺补漏」巩固你的HTTP知识体系](https://juejin.cn/post/6857287743966281736)

[送给前端 er 一份 HTTP 基础知识大图](https://mp.weixin.qq.com/s/3kR3Ptb2uiQ1sKlnnTr6mQ)

## 浏览器缓存

浏览器根据一下两个返回的头信息判断请求操作
Expires：时间，告诉浏览器在该时间前可以使用本地缓存
Cache-Control：控制缓存有效时间
Last-Modified：缓存失效后,向服务器查询是否有更新

- 本地缓存阶段：先在本地查找该资源，如果有发现该资源，而且该资源还没有过期，就使用这一个资源，完全不会发送http请求到服务器；
- 协商缓存阶段：如果在本地缓存找到对应的资源，但是不知道该资源是否过期或者已经过期，则发一个携带Last-Modified/Etag的http请求到服务器,然后服务器判断这个请求，如果请求的资源在服务器上没有改动过，则返回304，让浏览器使用本地找到的那个资源；

- 缓存失败阶段：当服务器发现请求的资源已经修改过，或者这是一个新的请求(在本来没有找到资源)，服务器则返回该资源的数据，并且返回200， 当然这个是指找到资源的情况下，如果服务器上没有这个资源，则返回404。

### 服务器缓存

- cdn实现
- Combo服务：将多个资源合并成一个文件，一次返回。

### HTML5缓存

- localstorage：用户可离线访问你的应用，这对于无法随时保持联网状态的移动终端用户来说尤其重要
  用户访问本地的缓存文件，通常意味着更快的访问速度
  仅仅加载被修改过的资源，避免同一资源对服务器多次的请求，大大降低了对服务器的访问压力
- 离线存储manifest

### 参考
[参考](http://imweb.io/topic/55c6f9bac222e3af6ce235b9)

## 浏览器同源策略

### 同源条件

协议相同，域名相同，端口相同

### 非同源下的行为限制

- Cookie、LocalStorage 和 IndexDB 无法读取。
- DOM 无法获得。
- AJAX 请求不能发送。

由于同源策略的限制，XmlHttpRequest只允许请求当前源（域名、协议、端口）的资源，

### 解决方法

#### JSONP：

原理是：动态插入script标签，通过script标签引入一个js文件，这个js文件载入成功后会执行我们在url参数中指定的函数，并且会把我们需要的json数据作为参数传入。

```js
function addScriptTag(src) {
  var script = document.createElement('script');
  script.setAttribute("type","text/javascript");
  script.src = src;
  document.body.appendChild(script);
}

window.onload = function () {
  addScriptTag('http://example.com/ip?callback=foo');
}

function foo(data) {
  console.log('Your public IP address is: ' + data.ip);
};
```

优点是兼容性好，简单易用，支持浏览器与服务器双向通信。缺点是只支持GET请求。

#### CORS

服务器端对于CORS的支持，主要就是通过设置Access-Control-Allow-Origin来进行的。如果浏览器检测到相应的设置，就可以允许Ajax进行跨域的访问。

- 如果需要携带 cookie，`Access-Control-Allow-Origin` header 的值不能使用通配符，必须指定 host
- fetch 发起的 cors 请求只能获取到标准 header(Cache-Control,Content-Language,Content-Type,Expires,Last-Modified,Pragma)，如果需要能够获取其他的 header，需要服务端在`access-control-expose-headers` 中设置

#### Websocket

#### 通过修改document.domain来跨子域

将子域和主域的document.domain设为同一个主域.前提条件：这两个域名必须属于同一个基础域名!而且所用的协议，端口都要一致，否则无法利用document.domain进行跨域

主域相同的使用document.domain

#### 使用window.name来进行跨域

window对象有个name属性，该属性有个特征：即在一个窗口(window)的生命周期内,窗口载入的所有的页面都是共享一个window.name的，每个页面对window.name都有读写的权限，window.name是持久存在一个窗口载入过的所有页面中的

#### 使用HTML5中新引进的window.postMessage方法来跨域传送数据

#### flash

#### 在服务器上设置代理页面等跨域方式

* * * * *

##### 参考链接 

[浏览器同源政策及其规避方法](http://www.ruanyifeng.com/blog/2016/04/same-origin-policy.html)
[跨域资源共享 CORS 详解](http://www.ruanyifeng.com/blog/2016/04/cors.html)

HTTP协议通常承载于TCP协议之上，在HTTP和TCP之间添加一个安全协议层（SSL或TSL），这个时候，就成了我们常说的HTTPS。

默认HTTP的端口号为80，HTTPS的端口号为443。

因为网络请求需要中间有很多的服务器路由器的转发。中间的节点都可能篡改信息，而如果使用HTTPS，密钥在你和终点站才有。

*****

## HTTPS

[HTTPS 升级指南](http://www.ruanyifeng.com/blog/2016/08/migrate-from-http-to-https.html)
[图解SSL/TLS协议](http://www.ruanyifeng.com/blog/2014/09/illustration-ssl.html)

![img](https://user-images.githubusercontent.com/34484322/89356430-58e32e00-d6f0-11ea-9320-115133c36e3e.png)