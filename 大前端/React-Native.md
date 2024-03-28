## 参考

[云音乐 React Native 体系建设与发展](https://juejin.cn/post/686772243636941620)

[React Native 新架构解析](https://segmentfault.com/a/1190000041182593)

## 库

> 资源列表 https://github.com/jondot/awesome-react-native
>
> 查询库的使用情况 https://reactnative.directory/

路由：https://reactnavigation.org/docs/getting-started/ 

本地store管理：https://github.com/sunnylqm/react-native-storage 

sqlite: https://github.com/realm/realm-js 

设备信息：https://github.com/react-native-device-info/react-native-device-info 

配置管理：https://github.com/luggit/react-native-config 

请求权限：[GitHub - zoontek/react-native-permissions: An unified permissions API for React Native on iOS and An](https://github.com/zoontek/react-native-permissions)

通讯录：https://github.com/morenoh149/react-native-contacts 

二维码扫描：https://github.com/ideacreation/react-native-barcodescanner 

UI:https://github.com/GeekyAnts/NativeBase 

运行时状态管理：https://mobx-state-tree.js.org/intro/getting-started 

开发工具：https://fbflipper.com/

### React-Native-Navigation

默认会带 header，它会处理安全区的问题，如果不使用默认 header `<Stack.Navigator headerMode="none">`

自行处理安全区用 [react-native-safe-area-context](https://github.com/th3rdwave/react-native-safe-area-context)

#### API

- `navigation.navigate('RouteName')` pushes a new route to the stack navigator if it's not already in the stack, otherwise it jumps to that screen.
- We can call `navigation.push('RouteName')` as many times as we like and it will continue pushing routes.
- The header bar will automatically show a back button, but you can programmatically go back by calling `navigation.goBack()`. On Android, the hardware back button just works as expected.
- You can go back to an existing screen in the stack with `navigation.navigate('RouteName')`, and you can go back to the first screen in the stack with `navigation.popToTop()`.
- The `navigation` prop is available to all screen components (components defined as screens in route configuration and rendered by React Navigation as a route).

## 热更新

国内热更新方案 https://pushy-admin.reactnative.cn/

## 问题记录

- yarn start 只启动了 metro，没有安装 android 相关依赖。

解决：完整命令启动 `npx react-native run-android`

- 在 genymotion 中打开调试面板 `adb shell input keyevent 82`

- pod install速度慢解决方案 原因：访问 github 蛮，解决：让 github 走代理

- react-native-orientation build 问题
  https://github.com/yamill/react-native-orientation/issues/407
  
- gradle 下载失败
  
  参考说明去手动下载 https://github.com/reactnativecn/react-native-website/issues/373

## 性能优化

- [React Native 性能优化指南](https://juejin.cn/post/6844904041290432525#heading-35)

- [没 2 年 React Native 开发经验，你都遇不到这些坑](https://juejin.cn/post/7012804162249293854)

切换 gradle 版本

https://lukerogerson.medium.com/how-to-upgrade-android-gradle-for-react-native-devs-eae77aed5423
