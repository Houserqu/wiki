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



