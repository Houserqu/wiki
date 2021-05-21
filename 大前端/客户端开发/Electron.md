# Electron

基于 Chromium 和 Node.js 的桌面客户端开发工具，支持 MacOS、Window、Linux 平台

# 打包

## 体积优化

1. 减少 package.json 中 dependencies 的依赖项，因为对应的 node_modules 中的文件也会打包进去
2. 双 package.json 项目结构，打包有专门的 package.json 文件

体积优化参考 [https://juejin.im/post/6844904071682326535](https://juejin.im/post/6844904071682326535)