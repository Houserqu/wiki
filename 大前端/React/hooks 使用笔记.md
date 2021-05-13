# hooks 使用笔记

# 请求数据

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

# 自带 Hooks

## useCallback

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

## useMemo

缓存值，避免组件重新渲染引起不必要的计算

```jsx
// 一下代码都在 render 方法中
// 不使用 useMemo，每次其他值的改变引起组件重新渲染的时候，compute 方法都会执行一次
const computeValue = compute(count);

// 使用 useMemo，只有在 count 发生变化时才执行，其他变量变化时，不会执行，直接使用之前缓存的结果
const computeValue = useMemo(() => compute(count), [count]);
```