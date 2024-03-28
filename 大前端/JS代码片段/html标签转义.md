## html 标签转义

对于需要前端直接渲染的 html 富文本代码，进行转义后存储，防止前端直接插入原始 html 导致 XSS 攻击

> 如果用 react 这种库，可以无需这样操作

```js
value = value.replace(/&/g, "&amp;");
value = value.replace(/</g, "&lt;");
value = value.replace(/>/g, "&gt;");
value = value.replace(/ /g, "&nbsp;");
value = value.replace(/"/g, '&quot;');
```

