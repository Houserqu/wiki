# apply/call/bind

[我所见过的讲"javascript中apply、call、bind"最清晰最易懂的文章](https://blog.csdn.net/aitangyong/article/details/49278171)
[理解 javascript 里的 bind() 函数](http://www.webhek.com/post/javascript-bind.html)

call 和 apply 都是为了改变某个函数运行时的上下文（context）而存在的，换句话说，就是为了改变函数体内部 this 的指向。

二者而言，作用完全一样，只是接受参数的方式不太一样.

apply 、 call 、bind 三者都是用来改变函数的this对象的指向的；apply 、 call 、bind 三者第一个参数都是this要指向的对象，也就是想指定的上下文；apply 、 call 、bind 三者都可以利用后续参数传参；bind是返回对应函数，便于稍后调用；apply 、call 则是立即调用。

```jsx
var obj = {
    x: 81,
};
 
var foo = {
    getX: function() {
        return this.x;
    }
}
 
console.log(foo.getX.bind(obj)());  //81
console.log(foo.getX.call(obj));    //81
console.log(foo.getX.apply(obj));   //81
```