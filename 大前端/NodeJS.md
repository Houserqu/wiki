# Node.js

## 基础

自己总结的 node 全栈开发思维导图 http://qiniu.houserqu.com/6ad6d70406b524f8caefae2feaa7828cee48d7e9d4b07b6f49ba0ee7b0510c15.png

## 性能分析

[对node工程进行压力测试与性能分析](https://juejin.cn/post/6844903665166188551)

通过 V8 Profiler 可以分析调用栈的耗时，找到耗时的操作

## 工具库

[TypeOrm](Node%20js%20ca596fd24ea04188946c20e6b2ccf656/TypeOrm%207f4a1108bccc45a782b034bf288083f5.md)

[Sequelize](Node%20js%20ca596fd24ea04188946c20e6b2ccf656/Sequelize%207fbf4dcb00324f92b748079121ef78ae.md)

## 技术

[命令行工具开发](Node%20js%20ca596fd24ea04188946c20e6b2ccf656/%E5%91%BD%E4%BB%A4%E8%A1%8C%E5%B7%A5%E5%85%B7%E5%BC%80%E5%8F%91%203b33f9b2bde84470aba11d2383174b2c.md)

## NPM

**peerDependencies**

目的是提示宿主环境去安装满足插件peerDependencies所指定依赖的包，然后在插件import或者require所依赖的包的时候，永远都是引用宿主环境统一安装的npm包，最终解决插件与所依赖包不一致的问题

## 命令行工具开发

### 库

- shelljs 方便调用系统 shell  命令
- yargs 方便处理命令行参数

## 模块化

### 模块引入顺序

首先加载核心模块,不管有没有同名/同目录的情况下,核心模块优先加载. 

其次按照相对路径/绝对路径加载文件模块(加载顺序,首先试图按照路径查找 .js 扩展名的文件,如果没有,试图按照路径查找 .json 扩展名的文件,如果还是没有,就按照路径查找 .node 扩展名的c++模块了) 

最后搜索 node_modules 目录下通过npm下载的第三方模块.  

注意:首次加载这类模块最慢,因为执行文件所在目录的node_mondel 文件夹下找不到时,会去父级node_mondel 文件夹里查找,如果还是找不到会去父级的父级node_mondel 文件夹里查找.......但是,只要首次加载成功后,node就会缓存起来,它缓存的是编译后的二进制模块,所以以后的加载速度和效率都的有保证的. 

### 简单模块化

1. 通过script标签实现模块化，但是依然会造成变量污染，而且还需要人为控制顺序

2. 通过立即执行函数进行函数作用域的隔离

### nodejs的规范CommonJs

一个文件就是一个模块，文件名就是模块的名字，使用模块的方法也和commonjs中一致，只需require就好了。CommonJS 模块在 require 的时候会立即执行模块文件里的代码，并缓存，当第二次 require 相同的文件的时候，直接从缓存中读取结果，效果跟 es6 模块一样。

```
module.export = add
var add = require('math');
```

缺点：

- 同步加载
- 不能非阻塞的并行加载多个模块

### AMD：Asynchronous Module Definition异步模块定义

示例

```
define("module", ["dep1", "dep2"], function(d1, d2) {
  return someExportedValue;
});
require(["module", "../file"], function(module, file) { /* ... */ });
```

优点：

- 适合在浏览器环境中异步加载模块
- 可以并行加载多个模块

缺点：

- 提高了开发成本，代码的阅读和书写比较困难，模块定义方式的语义不顺畅
- 不符合通用的模块化思维方式，是一种妥协的实现

### CMD规范

与 CommonJS 和 Node.js 的 Modules 规范保持了很大的兼容性。在 CMD 规范中，一个模块就是一个文件。

```
define(function(require, exports, module) {
  var $ = require('jquery');
  var Spinning = require('./spinning');
  exports.doSomething = ...
  module.exports = ...
})
```

### AMD和CMD的区别

1、对于依赖的模块，AMD是提前执行，CMD是延迟执行。
2、AMD推崇依赖前置；CMD推崇依赖就近，只有在用到某个模块的时候再去require。

### ES6模块化

ES6 模块的设计思想，是尽量的静态化，使得**编译时就能确定模块的依赖关系**，以及输入和输出的变量，能够提供更好的**变量类型检查**。CommonJS和AMD模块，都只能在运行时确定这些东西。es6 module 在声明 import 时并不会执行对应模块文件里的代码，而是在使用到了该模块导出的值的时候，才会去执行。es6 模块是【**单例】**的，一个模块只会执行一次，第二次读取该模块导出的变量的时候，直接从内存中读取。

es6 模块和 CommonJS 模块主要的区别是引用，前者不会立即执行，但是必须写在文件顶部，用于静态引用关系分析，后者在引用的时候立即执行，可以在代码任何位置去 require

[参考链接](http://xieyufei.com/2017/02/19/JS-Standard.html)

