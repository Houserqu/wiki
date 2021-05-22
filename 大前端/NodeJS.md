# Node.js

## 基础

自己总结的 node 全栈开发思维导图 http://qiniu.houserqu.com/6ad6d70406b524f8caefae2feaa7828cee48d7e9d4b07b6f49ba0ee7b0510c15.png

## 性能分析

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

