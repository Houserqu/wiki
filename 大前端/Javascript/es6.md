# es6

## 新增加的特性

- 模板字符串（为JavaScript提供了简单的字符串插值功能）
- 箭头函数（操作符左边为输入的参数，而右边则是进行的操作以及返回的值Inputs=>outputs。）
- for-of（用来遍历数据）
- arguments对象可被不定参数和默认参数完美代替。
- ES6将promise对象纳入规范，提供了原生的Promise对象。
- 增加了let和const命令，用来声明变量。增加了块级作用域。let命令实际上就增加了块级作用域。
- ES6规定，var命令和function命令声明的全局变量，属于全局对象的属性；let命令、const命令、class命令声明的全局变量，不属于全局对象的属性；
- 引入module模块的概念
- Default Parameters（默认参数） in ES6
- Multi-line Strings （多行字符串）in ES6
- Destructuring Assignment （解构赋值）in ES6
- Enhanced Object Literals （增强的对象文本）in ES6
- Block-Scoped Constructs Let and Const（块作用域构造Let and Const）
- Classes（类） in ES6

## => 函数

- 没有自己的this，而是使用当前上下文的this
- 通过 call() 或 apply() 方法调用一个函数时，只是传入了参数而已，对 this 并没有什么影响。
- 箭头函数不绑定Arguments 对象
- 箭头函数不能用作构造器，和 new一起用会抛出错误。
- 箭头函数没有prototype属性。
- yield 关键字通常不能在箭头函数中使用（除非是嵌套在允许使用的函数内）。因此，箭头函数不能用作生成器。
- params => {object:literal}这种简单的语法返回对象字面量出错。

## var/let/const

### var

函数作用域

### let

- 块级作用域
- 不能重定义
- let声明的全局变量不是全局对象的属性
- 形如for (let x...)的循环在每次迭代时都为x创建新的绑定

### const

- const声明的变量与let声明的变量类似，它们的不同之处在于，const声明的变量只可以在声明时赋值，