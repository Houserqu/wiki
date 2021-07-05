# TypeScript

## 值得参考的文档

[《TypeScript Deep Dive 中文版》](https://jkchao.github.io/typescript-book-chinese/)

[ 深入理解 TypeScript](https://jkchao.github.io/typescript-book-chinese/)

[基本原理讲解《上帝视角看 TypeScript》](https://mp.weixin.qq.com/s?__biz=MzA3MjU5NjU2NA==&mid=2455504213&idx=1&sn=b1ec8829983ac3425abe76085405e329&chksm=88b3486ebfc4c1786429c143c3a0683a099290d794630b4c055c2961f31d8bda8d1c0e6775d5&scene=21#wechat_redirect)

[类型工具方法](https://juejin.im/post/6844903981521567752#heading-6)

[4W字从0到部署上线，用 TS 带你彻底掌握前端工程化](https://mp.weixin.qq.com/s/heAeiXfJ8BHu-CO-kpTVLA)

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

### Type 与 Interface

[Typescript 中的 interface 和 type 到底有什么区别](https://juejin.cn/post/6844903749501059085)

最主要的区别是申明合并，两个同名的 interface 内的申明直接合并，如果用 type，通过 `&` 进行合并，而且可以定义成新的 type。

### 数组转元组类型

```tsx
// as const 可以将数组值定义为具体等类型，遍历等操作可以被推导，否则只能推导出 string、number 等类型
const furniture = ['chair', 'table', 'lamp'] as const;
type Furniture = typeof furniture[number];
```

[模块](TypeScript%2065e0f4daf8bb42fb96187cbc2a8c1ee9/%E6%A8%A1%E5%9D%97%207515fdcf4f0e4399b8a69f3e83bd8bda.md)

## 工具类型

```typescript
Partial<T>   // 将构造类型T的所有属性设置为可选
Require<T>   // 将类型T所有属性设为require
Record<K, T> // 构造一个对象类型，其属性名为K，属性值为T
Pick<T, K>   // 从类型T中挑选部分属性K来构造新的类型 Pick<Todo, 'title' | 'completed'>
Exclude<T, U>// 从类型T中，剔除所有能赋值给U的属性 Exclude< 'a' | 'b' | 'c', 'b'| 'c'> => 'a'
Extract<T, U>// 从类型T中提取所有可以赋值给U的类型 Extract< 'a' | 'b' | 'c', 'b'| 'c'> => 'b' | 'c'
Omit<T, K>   // 从类型T中剔除所有能赋值给K的属性 Omit<Todo, 'title'>
NonNullable  // 从T中剔除null和undefined
ReturnType<T>// 由函数类型T的返回值类型构造一个类型 ReturnType<()=> string> => string
Readonly<T>  // 将T中所有属性设为只读
```

## 热更新

> https://hackernoon.com/how-to-restart-the-typescript-nodejs-application-fast-v11d3t3f

主要有3个方案：

- [ts-node-dev](https://github.com/wclr/ts-node-dev) (推荐：速度最快，因为修改代码后不需要重新全部编译)

- tsc -w + node
- nodemon + ts-node

