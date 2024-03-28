# React

## 原理

react的核心是虚拟dom和diff算法

[React 源码剖析系列 － 不可思议的 react diff](https://zhuanlan.zhihu.com/p/20346379)

### 虚拟DOM（Virtual DOM）

React进行开发时所有的DOM构造都是通过虚拟DOM进行，每当数据变化时，React都会重新构建整个DOM树，然后React将当前整个DOM树和上一次的DOM树进行对比（diff算法），得到DOM结构的区别，然后仅仅将需要变化的部分进行实际的浏览器DOM更新。

而且React能够批处理虚拟DOM的刷新，在一个事件循环（Event Loop）内的两次数据变化会被合并，

### diff算法

diff算法可以将树的比对复杂度从O（n^3）降低到O(n)，从而大大提高性能

### diff策略

1. Web UI 中 DOM 节点跨层级的移动操作特别少，可以忽略不计。
2. 拥有相同类的两个组件将会生成相似的树形结构，拥有不同类的两个组件将会生成不同的树形结构。
3. 对于同一层级的一组子节点，它们可以通过唯一 id 进行区分。

基于以上三个前提策略，React 分别对 tree diff、component diff 以及 element diff 进行算法优化，

### tree diff

对树进行分层比较，两棵树只会对同一层次的节点进行比较

### component diff

如果是同一类型的组件，按照原策略继续比较 virtual DOM tree。如果不是，则将该组件判断为 dirty component，从而替换整个组件下的所有子节点。

### element diff

当节点处于同一层级时，React diff 提供了三种节点操作，分别为：INSERT_MARKUP（插入）、MOVE_EXISTING（移动）和 REMOVE_NODE（删除）。

### Key

key 是用来帮助 react 识别哪些内容被更改、添加或者删除。

#### key 的唯一性

在相邻的元素间，key 值必须是唯一的，如果出现了相同的 key，同样会抛出一个 Warning，告诉相邻组件间有重复的 key 值。并且只会渲染第一个重复 key 值中的元素，因为 react 会认为后续拥有相同 key 的都是同一个组件。

#### key 值不可读

#### 反模式

react默认会在数组组件加上index值作为key，如果在该数组末尾push元素，react 经过 diff 后就会发现前面的元素都没有变化，就会只插入一个新的组件，但是如果在数组前unshift元素，导致之前每个都发生变化，就会重新渲染所有组件，影响性能。所以需要给每个元素加上唯一稳定的key值。

## 生命周期

### 实例化阶段

组件初次实例化时依次调用下列方法

getDefaultProps

getInitialState

componentWillMount

该方法在首次渲染之前调用，也是再 render 方法调用之前修改 state 的最后一次机会。

render

该方法会创建一个虚拟DOM，用来表示组件的输出。对于一个组件来讲，render方法是唯一一个必需的方法。

componentDidMount

该方法不会在服务端被渲染的过程中调用。该方法被调用时，已经渲染出真实的 DOM，可以再该方法中通过 this.getDOMNode() 访问到真实的 DOM(推荐使用

### 存在期

此时组件已经渲染好并插入到真实dom中，组件的state发生改变时依次调用的方法

componentWillReceiveProps

shouldComponentUpdate

如果你确定组件的 props 或者 state 的改变不需要重新渲染，可以通过在这个方法里通过返回 false 来阻止组件的重新渲染，那么后续方法也不会执行。

componentWillUpdate

注意不要在此方面里再去更新 props 或者 state。

render

该方法会创建一个虚拟DOM，用来表示组件的输出。

componentDidUpdate

可以在这里访问并修改 DOM

### 销毁时

componentWillUnmount

## Hooks

hooks 的确可以简化一些 state 、生命周期相关的代码，我觉得最大的特点是可以将生命周期相关的逻辑用自定义 hooks 一起抽出来。自定义 hooks 完全依赖状态变化来触发，导致在处理用户通过事件触发一些操作的时候，实现起来很蹩脚，例如每次点击按钮请求数据、mount 阶段不自动执行 hooks。

### 请求数据

1. 自定义 hooks 只适合用来管理状态，不适合管理事件
2. 需要通过事件触发的异步操作，建议在组件方法里包装自定义方法
3. 初次渲染就加载的数据可以用自定义 hooks 去封装（[useSWR](https://github.com/vercel/swr#dependent-fetching)）

```jsx
// 请求用户数据的示例（初次渲染完请求一次，后续每次点击按钮请次）
export default function Home() {
  const [userinfo, setUserinfo] = useState(null)

  async function queryUser() {
    const res = await fetch('http://localhost:3000/api/user')
    const data =  await res.json()
    setUserinfo(data)
  }

  useEffect(() => {
    queryUser()
  }, [])

  return (
    <div>
      <button onClick={queryUser}> get </button>
      <p>{userinfo && userinfo.name}</p>       
    </div>
  )
}
```

```jsx
// 使用自定义 hooks 去请求数据
export default function Home() {
  // 发起请求
  async function queryUser() {
    const res = await fetch('http://localhost:3000/api/user')
    return await res.json()
  }

  // 初次渲染就会执行，无法反复触发
  const { userinfo, error } = useSWR('/api/user', queryUser)

  return (
    <div>
      <button onClick={queryUser}> get </button>
      <p>{userinfo && userinfo.name}</p>       
    </div>
  )
}

```

```jsx
// useSWR 给出的一个通过点击触发请求的示例，需要引入额外的状态，只能触发一次
function FetchOnClick() {
  const [shouldFetch, setShouldFetch] = React.useState(false);
  const { data } = useSWR(shouldFetch ? "/api/users/1" : null, fetcher);
  function handleClick() {
    setShouldFetch(true);
  }
  return (
    <>
      <button disable={shouldFetch} onClick={handleClick}>Fetch</button>
      {data ? <h1>{data.fullName}</h1> : null}
    </>
  );
}
```

### 自带 Hooks

#### useCallback

缓存方法实例，避免父组件渲染而引起子组件不必要的渲染

```jsx
// 下面的组件在父组件重新渲染的时候也会触发渲染，因为 onClick 匿名函数每次执行返回的内存地址是不同的
<Child onClick={() => {...}} />

// 在 Class 组件中的优化方式
<Child onClick={this.handleChildClick} />

// 用 useCallback 优化 
// 第三个参数数组是声明这些变量发生变化时，useCallback 需要返回新的方法实例，从而触发 Child 重新渲染
const handleChildClick = useCallback(() => {...}, [a])
<Child onClick={handleChildClick} />
```

#### useMemo

缓存值，避免组件重新渲染引起不必要的计算

```jsx
// 一下代码都在 render 方法中
// 不使用 useMemo，每次其他值的改变引起组件重新渲染的时候，compute 方法都会执行一次
const computeValue = compute(count);

// 使用 useMemo，只有在 count 发生变化时才执行，其他变量变化时，不会执行，直接使用之前缓存的结果
const computeValue = useMemo(() => compute(count), [count]);
```

## 使用 Typescript

react + typescript [typescript-cheatsheets/react](https://github.com/typescript-cheatsheets/react)

## 状态管理

### Redux

#### 中间件原理

Redux 的中间件提供的是位于 action 被发起之后，到达 reducer 之前的扩展点，换而言之，原本 view -> action -> reducer -> store 的数据流加上中间件后变成了 view -> action -> middleware -> reducer -> store ，在这一环节我们可以做一些 “副作用” 的操作，如 异步请求、打印日志等。

#### 基本思路

将一个Action划分成多个状态Action，例如请求数据

- 操作发起时的 startAction
- 操作成功时的 successAction
- 操作失败时的 failAction

操作开始时，送出一个 Action，触发 State 更新为"正在操作"状态，View 重新渲染
操作结束后，再送出一个 Action，触发 State 更新为"操作结束"状态，View 再一次重新渲染

#### redux-thunk 中间件

操作结束时，系统自动送出第二个 Action 呢？
thunk中间允许一个store.dispatch接受函数作为参数，从而实现一个action在异步结束后出发另外的action

### mobx

Mobx基于观察者模式，采用多节点管理数据，

很明显 Mobx 的代码要精简得多。通过 OOP 风格和良好的开发实践，你可以快速的构建各种应用。最大的弊病是很容易编写糟糕的不可维护的代码。但是，社区发展方面 Mobx 在国内的发展还是比较缓慢的，遇到的问题可能社区都没有遇到过。

而 Redux 更受欢迎一些，而且特别适合构建大型复杂应用。这是一个规定严格的框架，其规则确保开发人员可以编写易于测试和可维护的代码。但是，的确不适合开发小项目。

参考：[Redux 和 Mobx 哪个更适合你？](https://juejin.im/entry/5a61c3166fb9a01c9e460976)



如何定义 react hook type 类型

https://devtrium.com/posts/react-typescript-how-to-type-hooks
