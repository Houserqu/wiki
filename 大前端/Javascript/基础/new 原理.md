# new 原理

```jsx
var cat = new Animal("cat");
```

背后执行如下操作

```jsx
new Animal('cat') = {
    var obj = {};
    obj.__proto__ = Animal.prototype;
    var result = Animal.call(obj,"cat");
    return typeof result === 'object'? result : obj;
}
```

判断cat是否是Animal示例对象

```jsx
cat instanceof Aniaml    // true
```