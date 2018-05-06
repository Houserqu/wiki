# this 的指向问题

## 普通直接调用
this 指向全局对象

```js
function foo(){
  console.log(this)
}
foo(); // 输出全局作用域的顶级对象
```

## 通过对象调用
this指向直接调用该方法的对象；

## 全局作用域下直接调用
严格模式 this === undefined，
非严格模式：this指向全局对象(浏览器中为window,node中为特殊的模块作用域)

## 在构造函数中
this指向new 创建出的对象

```js
var inst = new Constr();
console.log(savedThis === inst); // true
```

## 在 eval() 中
与eval的作用域保持一致