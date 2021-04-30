# Ajax

AJAX即“Asynchronous Javascript And XML”（异步JavaScript和XML），是指一种创建交互式网页应用的网页开发技术。AJAX 是一种用于创建快速动态网页的技术。AJAX = 异步 JavaScript和XML（标准通用标记语言的子集）

Ajax的核心是创建 XMLHttpRequest 对象

创建ajax的过程

- step1. 创建XMLHttpRequest对象，也就是创建一个异步调用对象；
- step2. 创建一个新的HTTP请求，并指定改HTTP请求的方法、URL以及验证信息；
- step3. 设置响应HTTP状态变化的函数；
- step4. 发送HTTP请求；
- step5. 获取异步调用返回的数据；
- step6. 使用javascript和DOM实现局部刷新；

**请求状态**

- 0 － （未初始化）还没有调用send()方法
- 1 － （载入）已调用send()方法，正在发送请求 、
- 2 － （载入完成）send()方法执行完成，已经接收到全部响应内容
- 3 － （交互）正在解析响应内容 、
- 4 － （完成）响应内容解析完成，可以在客户端调用了

### 原生实现

```jsx
var Ajax={
  get: function(url, fn) {
    // XMLHttpRequest对象用于在后台与服务器交换数据   
    var xhr = new XMLHttpRequest();            
    xhr.open('GET', url, true);
    xhr.onreadystatechange = function() {
      // readyState == 4说明请求已完成
      if (xhr.readyState == 4 && xhr.status == 200 || xhr.status == 304) { 
        // 从服务器获得数据 
        fn.call(this, xhr.responseText);  
      }
    };
    xhr.send();
  },
  // datat应为'a=a1&b=b1'这种字符串格式，在jq里如果data为对象会自动将对象转成这种字符串格式
  post: function (url, data, fn) {
    var xhr = new XMLHttpRequest();
    xhr.open("POST", url, true);
    // 添加http头，发送信息至服务器时内容编码类型
    xhr.setRequestHeader("Content-Type", "application/x-www-form-urlencoded");  
    xhr.onreadystatechange = function() {
      if (xhr.readyState == 4 && (xhr.status == 200 || xhr.status == 304)) {
        fn.call(this, xhr.responseText);
      }
    };
    xhr.send(data);
  }
}
```