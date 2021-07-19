## 资源

[awesome-react-native](https://github.com/jondot/awesome-react-native): react-native 生态相关资源整理，

[云音乐 React Native 体系建设与发展](https://juejin.cn/post/686772243636941620)

## 性能

获取通讯录功能，react-native 比 API-Cloud 快非常多，不止 10 倍

## 库

[nativebase](https://nativebase.io/)

### React-Native-Navigation

默认会带 header，它会处理安全区的问题，如果不使用默认 header `<Stack.Navigator headerMode="none">`

自行处理安全区用 [react-native-safe-area-context](https://github.com/th3rdwave/react-native-safe-area-context)

#### API

- `navigation.navigate('RouteName')` pushes a new route to the stack navigator if it's not already in the stack, otherwise it jumps to that screen.
- We can call `navigation.push('RouteName')` as many times as we like and it will continue pushing routes.
- The header bar will automatically show a back button, but you can programmatically go back by calling `navigation.goBack()`. On Android, the hardware back button just works as expected.
- You can go back to an existing screen in the stack with `navigation.navigate('RouteName')`, and you can go back to the first screen in the stack with `navigation.popToTop()`.
- The `navigation` prop is available to all screen components (components defined as screens in route configuration and rendered by React Navigation as a route).

