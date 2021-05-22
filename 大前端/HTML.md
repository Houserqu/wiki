## 事件机制

DOM事件模型：事件捕获阶段、目标阶段、事件冒泡阶段。

*IE10及以下不支持捕获型事件*

#### 相关方法

**addEventListener(event, listener, useCapture)**

参数定义：event---（事件名称，如click，不带on），listener---事件监听函数，useCapture---是否采用事件捕获进行事件捕捉，默认为false，即采用事件冒泡方式

> addEventListener在 IE11、Chrome 、Firefox、Safari等浏览器都得到支持。

**attachEvent(event,listener)**

参数定义：event---（事件名称，如onclick，带on），listener---事件监听函数。

*attachEvent主要用于IE浏览器，并且仅在IE10及以下才支持*

**preventDefault()**

阻止事件默认行为

**stopPropagation()** 

阻止事件冒泡

### 事件捕获（event  capturing）

当鼠标点击或者触发dom事件时，浏览器会从根节点开始由外到内进行事件传播，即点击了子元素，如果父元素通过事件捕获方式注册了对应的事件的话，会先触发父元素绑定的事件。

### 事件冒泡（dubbed  bubbling）

与事件捕获恰恰相反，事件冒泡顺序是由内到外进行事件传播，直到根节点。

### 事件委托

利用事件捕获和事件委托的原理，不直接在需要触发的元素上绑定事件，而是在其父元素或者子元素上添加监听事件并判断触发元素，从而执行相关方法。

```js
parent.onclick = function(e){
    if(e.target.id == "child"){
        console.log("您点击了child元素")
    }
}
```

### 自定义事件

[实例](https://segmentfault.com/a/1190000008778993)

## 标签

### 标签的公有属性

accesskey 规定激活元素的快捷键；
class 规定元素的一个或多个类名（引用样式表中的类）；
contenteditable 规定元素内容是否可编辑；
contextmenu 规定元素的上下文菜单。上下文菜单在用户点击元素时显示。
data-* 用于存储页面或应用程序的私有定制数据。
dir 规定元素中内容的文本方向。
draggable 规定元素是否可拖动。
dropzone 规定在拖动被拖动数据时是否进行复制、移动或链接。
hidden  样式上会导致元素不显示，但是不能用这个属性实现样式。
id 规定元素的唯一 id。
lang 规定元素内容的语言。
spellcheck 规定是否对元素进行拼写和语法检查。
style 规定元素的CSS行内元素。
tabindex 规定元素的tab键次序。
title 规定有关元素的额外信息。
translate 规定是否应该翻译元素内容。

### meta

手机浏览器是把页面放在一个虚拟的"窗口"（viewport）中，通常这个虚拟的"窗口"（viewport）比屏幕宽，这样就不用把每个网页挤到很小的窗口中（这样会破坏没有针对手机浏览器优化的网页的布局），用户可以通过平移和缩放来看网页的不同部分。

```html
<meta name="viewport" content="width=device-width, initial-scale=1">
```

width：控制 viewport 的大小，可以指定的一个值，如 600，或者特殊的值，如 device-width 为设备的宽度（单位为缩放为 100% 时的 CSS 的像素）。
height：和 width 相对应，指定高度。
initial-scale：初始缩放比例，也即是当页面第一次 load 的时候缩放比例。
maximum-scale：允许用户缩放到的最大比例。
minimum-scale：允许用户缩放到的最小比例。
user-scalable：用户是否可以手动缩放。

## Iframe

### 缺点

- iframe会阻塞主页面的 Onload 事件；

- 搜索引擎的检索程序无法解读这种页面，不利于 SEO;

- iframe和主页面共享连接池，而浏览器对相同域的连接有限制，所以会影响页面的并行加载。

- 最好是通过 javascript动态给iframe添加 src 属性值，这样可以绕开以上两个问题。

