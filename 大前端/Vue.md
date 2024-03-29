# Vue

## Vue Router

### 重载路由页面

> 有些时候希望在**页面组件外**触发重载当前页面，但是不能刷新整个页面，因为全局 vuex 数据依然需要保留。

#### 方法一

> 新增一个中间页面（路径为 /refresh），在该页面中监听路由事件（`beforeRouteEnter`）,在事件逻辑中重新跳转回之前的页面。

组件代码：

```vue
<template></template>
<script>
  export default {
    beforeRouteEnter(to, from, next)  {
      next(vm => {
        vm.$router.replace(from.path);
        // 跳到该路由页面后，再替换为from.path来源路径
      })
    }
  }
</script>
```

路由注册：

```js
{
  name: "refresh",
  path: '/refresh',
  component: () => import('@/views/errPage/refresh') // Refresh 页面组件路径
}

```

使用：

```js
this.$router.replace('/refresh')
```

## Vue.nextTick()

> 在下次 DOM 更新循环结束之后执行延迟回调。在修改数据之后立即使用这个方法，获取更新后的 DOM。

[Vue.nextTick 的原理和用途](https://segmentfault.com/a/1190000012861862)

## 踩坑笔记

**keep-alive inclued 不生效**

include 数组值是组件的 name 属性值，不是路由的 name 值

## Vue3

### vue3快速上手

[让你30分钟快速掌握vue 3 - 掘金](https://juejin.cn/post/6887359442354962445#heading-27)

[vue3--vuex简单使用及持久化处理 - 掘金](https://juejin.cn/post/7006890304217284638)
