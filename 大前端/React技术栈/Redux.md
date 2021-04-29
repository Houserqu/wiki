## 中间件原理

Redux 的中间件提供的是位于 action 被发起之后，到达 reducer 之前的扩展点，换而言之，原本 view -> action -> reducer -> store 的数据流加上中间件后变成了 view -> action -> middleware -> reducer -> store ，在这一环节我们可以做一些 “副作用” 的操作，如 异步请求、打印日志等。

## 基本思路

将一个Action划分成多个状态Action，例如请求数据
- 操作发起时的 startAction
- 操作成功时的 successAction
- 操作失败时的 failAction

操作开始时，送出一个 Action，触发 State 更新为"正在操作"状态，View 重新渲染
操作结束后，再送出一个 Action，触发 State 更新为"操作结束"状态，View 再一次重新渲染

## redux-thunk 中间件

操作结束时，系统自动送出第二个 Action 呢？
thunk中间允许一个store.dispatch接受函数作为参数，从而实现一个action在异步结束后出发另外的action