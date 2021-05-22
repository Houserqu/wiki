# TypeScript

## 值得参考的文档

[《TypeScript Deep Dive 中文版》](https://jkchao.github.io/typescript-book-chinese/)

[基本原理讲解《上帝视角看 TypeScript》](https://mp.weixin.qq.com/s?__biz=MzA3MjU5NjU2NA==&mid=2455504213&idx=1&sn=b1ec8829983ac3425abe76085405e329&chksm=88b3486ebfc4c1786429c143c3a0683a099290d794630b4c055c2961f31d8bda8d1c0e6775d5&scene=21#wechat_redirect)

[类型工具方法](https://juejin.im/post/6844903981521567752#heading-6)

## tsconfig.json

ts 项目配置文件

[tsconfig.json 配置文件解析](https://jishuin.proginn.com/p/763bfbd2b6a6)

## 模块导出

```jsx
// commonjs 模块
import * as xx from 'xx'

// 标准 es6 模块
import xx from 'xx'

// commonjs 模块，类型声明为 export = xx
import xx = require('xx')

// 没有类型声明，默认导入 any 类型
const xx = require('xx')
```

## 一些语法

### 数组转元组类型

```tsx
// as const 可以将数组值定义为具体等类型，遍历等操作可以被推导，否则只能推导出 string、number 等类型
const furniture = ['chair', 'table', 'lamp'] as const;
type Furniture = typeof furniture[number];
```

[模块](TypeScript%2065e0f4daf8bb42fb96187cbc2a8c1ee9/%E6%A8%A1%E5%9D%97%207515fdcf4f0e4399b8a69f3e83bd8bda.md)