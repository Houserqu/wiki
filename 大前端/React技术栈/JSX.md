每一个JSX元素都只是 React.createElement(component, props, ...children) 的语法糖

```
//jsx
<a href="http://facebook.github.io/react/">Hello!</a>

// js
React.createElement('a', {href: 'http://facebook.github.io/react/'}, 'Hello!')
```

第一个参数是标签名，第二个参数是属性对象，第三个参数是子元素。