react的核心是虚拟dom和diff算法

## 虚拟DOM（Virtual DOM）

React进行开发时所有的DOM构造都是通过虚拟DOM进行，每当数据变化时，React都会重新构建整个DOM树，然后React将当前整个DOM树和上一次的DOM树进行对比（diff算法），得到DOM结构的区别，然后仅仅将需要变化的部分进行实际的浏览器DOM更新。

而且React能够批处理虚拟DOM的刷新，在一个事件循环（Event Loop）内的两次数据变化会被合并，

## diff算法

diff算法可以将树的比对复杂度从O（n^3）降低到O(n)，从而大大提高性能

## diff策略

1. Web UI 中 DOM 节点跨层级的移动操作特别少，可以忽略不计。
2. 拥有相同类的两个组件将会生成相似的树形结构，拥有不同类的两个组件将会生成不同的树形结构。
3. 对于同一层级的一组子节点，它们可以通过唯一 id 进行区分。

基于以上三个前提策略，React 分别对 tree diff、component diff 以及 element diff 进行算法优化，

### tree diff

对树进行分层比较，两棵树只会对同一层次的节点进行比较

### component diff

如果是同一类型的组件，按照原策略继续比较 virtual DOM tree。
如果不是，则将该组件判断为 dirty component，从而替换整个组件下的所有子节点。

### element diff

当节点处于同一层级时，React diff 提供了三种节点操作，分别为：INSERT_MARKUP（插入）、MOVE_EXISTING（移动）和 REMOVE_NODE（删除）。

*****
##### 参考

[参考](https://zhuanlan.zhihu.com/p/20346379)