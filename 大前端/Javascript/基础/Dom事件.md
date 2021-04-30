# Dom事件

## 事件机制

DOM事件模型：事件捕获阶段、目标阶段、事件冒泡阶段。

*IE10及以下不支持捕获型事件*

### 相关方法

**addEventListener(event, listener, useCapture)**

参数定义：event---（事件名称，如click，不带on），listener---事件监听函数，useCapture---是否采用事件捕获进行事件捕捉，默认为false，即采用事件冒泡方式

**attachEvent(event,listener)**

参数定义：event---（事件名称，如onclick，带on），listener---事件监听函数。

*attachEvent主要用于IE浏览器，并且仅在IE10及以下才支持*

**preventDefault()**

阻止事件默认行为

**stopPropagation()**

阻止事件冒泡

## 事件捕获（event capturing）

当鼠标点击或者触发dom事件时，浏览器会从根节点开始由外到内进行事件传播，即点击了子元素，如果父元素通过事件捕获方式注册了对应的事件的话，会先触发父元素绑定的事件。

## 事件冒泡（dubbed bubbling）

与事件捕获恰恰相反，事件冒泡顺序是由内到外进行事件传播，直到根节点。

## 事件委托

利用事件捕获和事件委托的原理，不直接在需要触发的元素上绑定事件，而是在其父元素或者子元素上添加监听事件并判断触发元素，从而执行相关方法。

```jsx
parent.onclick = function(e){
    if(e.target.id == "child"){
        console.log("您点击了child元素")
    }
}
```

## 自定义事件

[实例](https://segmentfault.com/a/1190000008778993)