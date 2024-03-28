# Golang

## 特点

- 定位跟 C++ 类似，系统级语言开发
- 适合做分布式、复杂的后端系统，性能好，稳定
- 多线程开发更加友好，方便
- 支持多返回值，
- 没有异常，无法使用 try catch 进行捕获，一般通过返回值处理，这样导致需要写很多判断错误值的代码，好处是代码更加健壮，开发者需明确的处理错误
- golang：多线程非阻塞，node：单线程非阻塞
- 可以直接打包成二进制文件，不需要 golang 环境和安装依赖就可以运行，对基于 Docker 的部署更加方便
- 不支持范型，导致容易产生重复逻辑的代码 (进行中)

## 资料

> 快速了解语法：[入门速成指南](https://learnku.com/go/t/24715)
>
> 推荐基础学习资料：[the-way-to-go_ZH_CN](https://github.com/unknwon/the-way-to-go_ZH_CN) 
>
> go 生态：[Go知识图谱](https://www.processon.com/view/link/5a9ba4c8e4b0a9d22eb3bdf0#map)
>
> go 常见代码：https://gobyexample.com/
>
> go 代码规范 [Go Code Review Comments](https://github.com/golang/go/wiki/CodeReviewComments)
>
> 3种方式！Go Error处理最佳实践: https://mp.weixin.qq.com/s/ibGCUovoDHY2H9aa5jnDfA

## 基础

### 25 个保留关键字

- `var` ,`const` ：变量和常量的声明
- `package` ：声明包
- `import`：导入包
- `func`： 用于定义函数和方法
- `return` ：用于从函数返回
- `defer`  ：在函数退出之前执行
- `go` : 用于并行
- `select`: 用于选择不同类型的通讯
- `interface` ：用于定义接口
- `struct` ：用于定义抽象数据类型
- `break`、`case`、`continue`、`for`、`fallthrough`、`else`、`if`、`switch`、`goto`、`default` ：流程控制
- `chan` ：用于channel通讯
- `type`：用于声明自定义类型
- `map`：用于声明map类型数据
- `range` ：用于读取 slice、map、channel 数据

### 基本数据类型

能够通过`make()`创建的都是引用类型，有 slice、map、chan，返回的是指针

#### 数组与切片

```go
var numbers []int // 初始化没有容量的切片
numbers := make([]int, 15) // 创建指定长度的切片

numbers = append(numbers, 1, 2, 3, 4) // 在数组末尾增加元素，容量不足时增加容量
copy(b, a) // 复制切片 a 的元素到新的切片 b 上：
```

```go
删除位于索引 i 的元素：a = append(a[:i], a[i+1:]...)
切除切片 a 中从索引 i 至 j 位置的元素：a = append(a[:i], a[j:]...)
为切片 a 扩展 j 个元素长度：a = append(a, make([]T, j)...)
在索引 i 的位置插入元素 x：a = append(a[:i], append([]T{x}, a[i:]...)...)
在索引 i 的位置插入长度为 j 的新切片：a = append(a[:i], append(make([]T, j), a[i:]...)...)
在索引 i 的位置插入切片 b 的所有元素：a = append(a[:i], append(b, a[i:]...)...)
取出位于切片 a 最末尾的元素 x：x, a = a[len(a)-1:], a[:len(a)-1]
将元素 x 追加到切片 a：a = append(a, x)
```

#### 字符串

##### strconv 包

实现了字符串与数字（整数、浮点数等）之间的互相转换.

```go
// 接受1，t，T，TRUE，true，True，0，f，F，FALSE，false，False。 其他任何值都将返回错误
strconv.ParseBool(str string) (value bool, err error) 
// 字符串转数字
int, err := strconv.Atoi(string)
int64, err := strconv.ParseInt(string, 10, 64)
// 数字转字符串
string := strconv.Itoa(int)
string := strconv.FormatInt(int64,10)
```

**常用操作**

```go
// 字符串截取
str := "Hello HaiCoder!"
str1 := str[0:4] // Hell
```



#### 数字

```go
// 整数:
int / uint // 位数取决于 CPU 的位数
int8（-128 -> 127）
int16（-32768 -> 32767）
int32（-2,147,483,648 -> 2,147,483,647）
int64（-9,223,372,036,854,775,808 -> 9,223,372,036,854,775,807）

// 无符号整数
uint8（0 -> 255）
uint16（0 -> 65,535）
uint32（0 -> 4,294,967,295）
uint64（0 -> 18,446,744,073,709,551,615）

// 浮点型（IEEE-754 标准）
float32（+- 1e-45 -> +- 3.4 * 1e38）
float64（+- 5 1e-324 -> 107 1e308）
```

#### 结构体 struct

```go
// 声明
type Person struct {
  name string
  age int
  gender string
}

p := Person{name: "Bob", age: 42, gender: "Male"} // 1.指定属性和值的方式初始化
p := Person{"Bob", 42, "Male"} // 2.指定值的方式初始化（需要跟声明的属性顺序一致）

p.name // 访问属性
pp = &person; pp.name // 也可以通过指针直接访问属性
```

##### 方法

作用在结构体上的函数

```go
// 给 person 结构体定义 describe 方法
func (p *Person) describe() {
  fmt.Printf("%v is %v years old.", p.name, p.age)
}

// 调用
pp := &person{name: "Bob", age: 42, gender: "Male"}
pp.describe()
```

#### 接口 interface

方法的集合

```go
// 声明接口
type animal interface {
  description() string
}
// 声明结构体
type cat struct {
  Type  string
  Sound string
}
// 结构体实现接口方法
func (c cat) description() string {
  return fmt.Sprintf("Sound: %v", c.Sound)
}
// 初始化接口并指定结构体实例
var a animal
a = snake{Poisonous: true}
```

#### Map

key-value 数据结构

```go
m := make(map[string]int) // 创建 key:string value:int
m["clearity"] = 2 // 赋值
m["clearity"] // 取值
```

#### 指针

```go
var ap *int // * 定义指针，ap 是指向整数类型的指针，值为地址
a := 12; ap = &a // & 取地址，&a 的到变量 a 的地址，赋值给指针类型变量 ap
fmt.Println(*ap) // * 访问指针变量的值
```

在将结构体作为参数传递或者为已定义类型声明方法时，通常首选指针。特点：

1. 只需要传递指针，节省内存
2. 能够修改原始数据（因为传递的不是变量副本）

### 函数 

#### 声明

```go
func add(a int, b int) int {...} // 单返回值
func add(a int, b int) (int, error) {...} // 多返回值
func add(a int, b int) (c int, err error) { // 声明的多返回值,
  c = a + b // c 已经声明，直接使用
  return    // 可以不用指明变量
}

func (c *person) add(a int, b int) int {...} // 方法的声明
```

#### defer

总是在函数结束时执行，即使函数发生 panic。常用于进行后置操作如关闭打开的文件、释放数据库链接等。

```go
func f() {
  defer fmt.Println("defer") // 后执行
  fmt.Println("func")
}

// 在 defer 恢复 panic，可以避免程序 crash
func f() {
	defer func() {
    if r := recover(); r != nil {
      fmt.Println("Recovered in f", r)
    }
  }()
  
  panic("panic")
}
```

### 协程 goroutine

轻量级的线程，可以在一个线程里面跑多个协程，通过通道（chanel）来实现数据共享。是语言层面的现实。

#### 通道

```go
func main(){
  c := make(chan string)        // 声明通道
  go func(){ c <- "hello" }()   // 写数据到通道
  msg := <-c                    // 从通道取数据
  fmt.Println(msg)
}
```

##### 多通道处理

```go
// 类似于 switch，用来处理多个通道。并且可以阻塞程序退出。
select {
 	case s1 := <-c1:
  	fmt.Println(s1)
 	case s2 := <-c2:
  	fmt.Println(s2)
 }
```

##### 缓冲通道

```go
ch := make(chan string, 2) // 缓冲区容量为 2 的通道
```

### error 与 panic

[Go 语言 panic 与 error 最佳实践](https://zhuanlan.zhihu.com/p/87345297)

### 运算符

```go
优先级     运算符
 7      ^ !
 6      * / % << >> & &^
 5      + - | ^
 4      == != < <= >= >
 3      <-
 2      &&
 1      ||
```

### 标准 API

#### 时间 time

> https://www.zhangbj.com/p/652.html

## 编译

Go 支持不同平台的交叉编译，直接生成可执行文件（不需要安装 go 环境就可以运行）。

```bash
设置 GOOS 和 GOARCH 两个环境变量就能生成所需平台的Go程序

GOOS：目标可执行程序运行操作系统，支持 darwin，freebsd，linux，windows（darwin代表苹果电脑的系统）
GOARCH：目标可执行程序 CPU 构架，包括 386，amd64，arm，arm64

示例：
CGO_ENABLED=0 GOOS=linux GOARCH=amd64 go build -o app main.go
CGO_ENABLED=0 GOOS=windows GOARCH=amd64 go build -o app main.go
CGO_ENABLED=0 GOOS=darwin GOARCH=amd64 go build -o app main.go

Golang version 1.5以前版本在首次交叉编译时还需要配置交叉编译环境：
CGO_ENABLED=0 GOOS=linux GOARCH=amd64 ./make.bash
CGO_ENABLED=0 GOOS=windows GOARCH=amd64 ./make.bash
```

## 公共库

[标准库文档](https://pkg.go.dev/std)，[标准库文档（中文）](https://studygolang.com/pkgdoc)

| 库                                      | 标准库 | 说明                                                         |
| --------------------------------------- | ------ | ------------------------------------------------------------ |
| [Viper](https://github.com/spf13/viper) |        | 功能全面的配置处理库，支持多种配置获取方式：文件、服务、环境变量 |
| [cobra](https://github.com/spf13/cobra) |        | cli 开发工具库                                               |
| pdfcpu                                  |        | 处理 pdf 文件（加水印、拆分）                                |
| ImageMagick                             |        | [参考](https://jelly.jd.com/article/5c34081bd7aa2c0055d09a71) |

## 代码片段

创建文件的同时创建不存在的目录

```go
func CreateFileWithFolder(p string) (*os.File, error) {
	if err := os.MkdirAll(filepath.Dir(p), 0770); err != nil {
		return nil, err
	}
	return os.Create(p)
}
```

