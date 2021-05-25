# JS基础

## 背景

[ES6、ES7、ES8、ES9、ES10新特性一览](https://juejin.cn/post/6844903811622912014)

## 闭包

闭包是指能够访问其他作用域变量的函数。[闭包原理解释](https://mp.weixin.qq.com/s?__biz=MzAxODE2MjM1MA==&mid=2651553785&idx=1&sn=a8efd632cc52dac510b6dee87b50ccaa&chksm=8025a838b752212e141c83d08f55ce5d56f79e70e0bfca8dea9559175876b021bc41aa741b75&scene=38#wechat_redirect)

作用：

一个是前面提到的可以读取函数内部的变量，另一个就是让这些变量的值始终保持在内存中。

注意的问题：

- 由于闭包会使得函数中的变量都被保存在内存中，内存消耗很大，
- 闭包会在父函数外部，改变父函数内部变量的值

## 对象

### 对象的创建方式

1.  工厂模式：创建一个工厂方法，接受参数，然后new Object，绑定参数属性和方法，return 这个对象。使用时直接调用这个工厂方法。
2.  构造函数模式：通过 new 构造函数
3.  原型模式：在构造函数的基础上通过原型添加属性。会导致这些属性在所有实例中共享
4.  混合构造函数和原型模式：实例私有属性通过构造函数添加，公有属性通过原型添加。通过new 创建
5.  动态原型模式：在构造方法中增加某些属性判断，如果某个属性不存，才允许添加到原型中。
6.  寄生构造函数模式：与工厂模式写法一样，只是在创建实例的时候通过 new 构造函数。（无法通过instanceof确定对象类型，不建议使用）
7.  稳妥构造函数模式

### 对象属性遍历

#### for..in

遍历对象**自身和继承的** [可枚举属性](https://www.cnblogs.com/kongxy/p/4618173.html)

```
for(let key in obj){}
```

#### Object.keys(obj)

返回一个数组，包括对象自身的（不含继承的）所有可枚举属性（不含 Symbol 类型的属性）

#### Object.getOwnPropertyNames(obj)

返回一个数组，包含对象自身的所有属性（不含 Symbol 类型的属性，不包含继承属性，但是包括不可枚举属性）

#### Object.getOwnPropertySymbols(obj)

返回一个数组，包含对象自身的所有 Symbol 类型的属性（不包括继承的属性）

#### Reflect.ownKeys(obj)

返回一个数组，包含对象自身的所有属性（包含 Symbol 类型的属性，还有不可枚举的属性，但是不包括继承的属性）

### new 原理

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

## 面向对象编程

[js:面向对象编程，带你认识封装、继承和多态](https://juejin.cn/post/6844903480868470798)

### 继承

1. 原型链继承
2. 借用构造函数继承
   在子类的构造方法通过执行Father.call(this)调用父类的构造方法。
   问题：父类的属性都会copy一份到子类，方法无法复用。
3. 组合继承(原型+借用构造)
   共用的属性通过原型继承，实例属性通过借用构造函数继承
4. 原型式继承
   利用var son = Object.create(Father)
5. 寄生式继承
   类似工厂方法，定义一个创建方法，内部采用原型式继承法创建对象，然后添加新的属性，最后return
6. 寄生组合式继承
   定义一个创建方法，接受子父对象作为参数，先创建父对象并把其原型赋值给临时变量，然后子对象赋值给他的constructor属性，最后把这个增强的对象作为子对象的原型。

## 数组

### 数组遍历

#### 最基本的 for 循环、while 循环遍历（缺陷是多添加了一个计数变量）

#### for…of 

``` 
for(let value of arr){
    console.log(value);
}
```

#### Array.prototype.forEach()

对数组的每个元素执行一次提供的函数

#### Array.prototype.map()

返回一个新数组，每个元素都是回调函数返回的值

## 数字

### 精度问题

[JavaScript 浮点数运算的精度问题](https://www.notion.so/JavaScript-WEB-d229e1b8d0f94cb8bd4b5e9b79fa53cb)

## 原型链

> 1.对象有属性__proto__,指向该对象的构造函数的原型对象。2.方法除了有属性__proto__,还有属性prototype，prototype指向该方法的原型对象。

每个对象都有一个私有属性（称之为 [[Prototype]]），它指向它的原型对象（prototype）。该 prototype 对象又具有一个自己的 prototype ，层层向上直到一个对象的原型为 null。根据定义，null 没有原型，并作为这个原型链中的最后一个环节。几乎所有 JavaScript 中的对象都是位于原型链顶端的Object的实例。

当访问对象的某个属性的时候，会先查找当前对象的属性，然后在查找原型对象的属性，如果没找到继续查找该原型对象的原型对象属性，层层查找直到原型链顶端。

### 相关操作

判断实例 与原型的关系：instanceof

原型对象的键名: `__proto__`

创建没有原型的对象：`Object.create(null)`

## 运算符

[运算符优先级](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Operators/Operator_Precedence)

## 作用域

### 作用域链

当查找变量的时候，会先从当前上下文的变量对象中查找，如果没有找到，就会从父级(词法层面上的父级)执行上下文的变量对象中查找，一直找到全局上下文的变量对象，也就是全局对象。这样由多个执行上下文的变量对象构成的链表就叫做作用域链。

### 变量提升

## Ajax

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

## call() apply() bind()

> [我所见过的讲"javascript中apply、call、bind"最清晰最易懂的文章](https://blog.csdn.net/aitangyong/article/details/49278171)
> [理解 javascript 里的 bind() 函数](http://www.webhek.com/post/javascript-bind.html)

call 和 apply 都是为了改变某个函数运行时的上下文（context）而存在的，换句话说，就是为了改变函数体内部 this 的指向。二者而言，作用完全一样，只是接受参数的方式不太一样.

apply 、 call 、bind 三者都是用来改变函数的this对象的指向的；
apply 、 call 、bind 三者第一个参数都是this要指向的对象，也就是想指定的上下文；
apply 、 call 、bind 三者都可以利用后续参数传参；
bind是返回对应函数，便于稍后调用；apply 、call 则是立即调用。

```js
var obj = { x: 81 };
 
var foo = {
    getX: function() {
        return this.x;
    }
}
 
console.log(foo.getX.bind(obj)());  //81
console.log(foo.getX.call(obj));    //81
console.log(foo.getX.apply(obj));   //81
```

## console

### console.log

#### 控制台彩色输出

```jsx
console.log('\033[42;32m Success \033[0m info')
```

**格式** `\033[背景色编号;字色编号m` 。

**字色编号**

30黑，31红，32绿，33黄，34蓝，35紫，36深绿，37白色 

**背景编号**

40黑，41红，42绿，43黄，44蓝，45紫，46深绿，47白色

**\033[0m** 

是结束标记，表示前面样式到这里结束

**其他特殊的标记**

- `\033[0m` 关闭所有属性
- `\033[1m` 设置高亮度
- `\033[4m` 下划线
- `\033[5m` 闪烁
- `\033[7m` 反显
- `\033[8m` 消隐
- `\033[nA` 光标上移n行
- `\033[nB` 光标下移n行
- `\033[nC` 光标右移n列
- `\033[nD` 光标左移n列
- `\033[y;xH` 设置光标位置（y列x行）
- `\033[2J` 清屏
- `\033[K` 清除从光标到行尾的内容

## Dom事件

### 事件机制

DOM事件模型：事件捕获阶段、目标阶段、事件冒泡阶段。

*IE10及以下不支持捕获型事件*

### 相关方法

**addEventListener(event, listener, useCapture)**

参数定义：event---（事件名称，如click，不带on），listener---事件监听函数，useCapture---是否采用事件捕获进行事件捕捉，默认为false，即采用事件冒泡方式

**attachEvent(event,listener)** *仅在IE10及以下才支持* 

参数定义：event---（事件名称，如onclick，带on），listener---事件监听函数。

**preventDefault()**

阻止事件默认行为

**stopPropagation()**

阻止事件冒泡

### 事件捕获（event capturing）

当鼠标点击或者触发dom事件时，浏览器会从根节点开始由外到内进行事件传播，即点击了子元素，如果父元素通过事件捕获方式注册了对应的事件的话，会先触发父元素绑定的事件。

### 事件冒泡（dubbed bubbling）

与事件捕获恰恰相反，事件冒泡顺序是由内到外进行事件传播，直到根节点。

### 事件委托

利用事件捕获和事件委托的原理，不直接在需要触发的元素上绑定事件，而是在其父元素或者子元素上添加监听事件并判断触发元素，从而执行相关方法。

```jsx
parent.onclick = function(e){
    if(e.target.id == "child"){
        console.log("您点击了child元素")
    }
}
```

### 自定义事件

[实例](https://segmentfault.com/a/1190000008778993)

## Proxy/Reflect

> [Proxy 和 Reflect](https://juejin.cn/post/6844904090116292616)

### Proxy

#### 定义

Proxy 对象用于定义基本操作的自定义行为（如属性查找、赋值、枚举、函数调用等）。

#### 用途

利用Proxy可以拦截对象的 get、set、delete 操作，进行一些自定义操作，例如参数校验、格式转换等。

如果对象属性配置了`configurable: false` 與 `writable: false`，则不能被 proxy 拦截

#### this 问题

Proxy 代理的对象的 this 指向的是 Proxy，如果需要指向原始对象可以通过 bind 解决

```sql
let div = document.querySelector('div'); // 随便拿一个页面的 div, 对他进行代理

// 第一种代理方法
let divProxy = new Proxy(div, {
  get: function (target, key, receiver) {
    // 访问这个 div 的任何属性，都直接返回
    return target[key]; // target[key].bind(target); 这样让 this 指向原对象
  }
});
// 调用 div 的 querySelector 方法，拿他下边的 a 标签
// chrome 上会报错：Uncaught TypeError: Illegal invocation
console.log(divProxy.querySelector('a')); 
```

### Reflect

#### 定义

Reflect 是一个内置的对象，它提供拦截 JavaScript 操作的方法。这些方法与proxy handlers的方法相同。Reflect不是一个函数对象，因此它是不可构造的。

#### 用途

Reflect 可是个静态对象，可以接受目标对象作为参数，并执行该对象的方法

#### 示例

```sql
const duck = {
  name: 'Maurice',
  color: 'white',
}

Reflect.has(duck, 'color');
// true
Reflect.has(duck, 'haircut');
// false
```

一般 reflect 会跟 proxy 一起使用，通过 reflect 去修改属性，而不是直接访问属性

```sql
const handler = {
  get(target, prop) {
    return Reflect.get(target, prop);
  }
};
const proxy = new Proxy({}, handler);
```

### Proxy 与 Reflect 的不同

调用方式不同，但是能实现的功能是相同的

![picture 26](http://qiniu.houserqu.com/dc0c45f97463f9396147c85b1feeddd794a0e7a9b92fc6b3030ceb0aa9558dc2.png)  

## this

### this 的指向问题

#### 普通直接调用

this 指向全局对象

```js
function foo(){
  console.log(this)
}
foo(); // 输出全局作用域的顶级对象
```

#### 通过对象调用

this 指向直接调用该方法的对象(普通函数)；

#### 全局作用域下直接调用

严格模式 this === undefined，
非严格模式：this指向全局对象(浏览器中为window,node中为特殊的模块作用域)

### 在构造函数中

this指向new 创建出的对象

```js
var inst = new Constr();
console.log(savedThis === inst); // true
```

### 在 eval() 中

与eval的作用域保持一致

当线程中没有执行任何同步代码的前提下才会执行异步代码，

> [JavaScript：彻底理解同步、异步和事件循环(Event Loop)](https://segmentfault.com/a/1190000004322358)
> [阮一峰异步编程](http://www.ruanyifeng.com/blog/2015/04/generator.html)

## 异步编程的方法

#### 回调函数

采用这种方式，我们把同步操作变成了异步操作，f1不会堵塞程序运行，相当于先执行程序的主要逻辑，将耗时的操作推迟执行。
回调函数的优点是简单、容易理解和部署，缺点是不利于代码的阅读和维护，各个部分之间高度耦合（Coupling），流程会很混乱，而且每个任务只能指定一个回调函数。

#### 事件监听

任务的执行不取决于代码的顺序，而取决于某个事件是否发生。

#### Promises对象

Promises对象是CommonJS工作组提出的一种规范，目的是为异步编程提供统一接口。

Promises可以简单理解为一个事务，这个事务存在三种状态：

已经完成了 resolved
因为某种原因被中断了 rejected
还在等待上一个事务结束 pending

简单说，它的思想是，每一个异步任务返回一个Promises对象，该对象有一个then方法，允许指定回调函数。

#### generator

#### async/await

