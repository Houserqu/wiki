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

[入门速成指南](https://learnku.com/go/t/24715)

## 基础

### 数组与切片

将切片 b 的元素追加到切片 a 之后：a = append(a, b...)

复制切片 a 的元素到新的切片 b 上：

```go
 b = make([]T, len(a))
 copy(b, a)
```

删除位于索引 i 的元素：a = append(a[:i], a[i+1:]...)

切除切片 a 中从索引 i 至 j 位置的元素：a = append(a[:i], a[j:]...)

为切片 a 扩展 j 个元素长度：a = append(a, make([]T, j)...)

在索引 i 的位置插入元素 x：a = append(a[:i], append([]T{x}, a[i:]...)...)

在索引 i 的位置插入长度为 j 的新切片：a = append(a[:i], append(make([]T, j), a[i:]...)...)

在索引 i 的位置插入切片 b 的所有元素：a = append(a[:i], append(b, a[i:]...)...)

取出位于切片 a 最末尾的元素 x：x, a = a[len(a)-1:], a[:len(a)-1]

将元素 x 追加到切片 a：a = append(a, x)

### error 与 panic

[Go 语言 panic 与 error 最佳实践](https://zhuanlan.zhihu.com/p/87345297)

## 编译

Go 支持不同平台的交叉编译，直接生成可执行文件（不需要安装 go 环境就可以运行）。

```
设置 GOOS 和 GOARCH 两个环境变量就能生成所需平台的Go程序

GOOS：目标可执行程序运行操作系统，支持 darwin，freebsd，linux，windows（darwin代表苹果电脑的系统）
GOARCH：目标可执行程序 CPU 构架，包括 386，amd64，arm，arm64

示例：
$ CGO_ENABLED=0 GOOS=linux GOARCH=amd64 go build test.go
$ CGO_ENABLED=0 GOOS=windows GOARCH=amd64 go build test.go
$ CGO_ENABLED=0 GOOS=darwin GOARCH=amd64 go build test.go

Golang version 1.5以前版本在首次交叉编译时还需要配置交叉编译环境：
CGO_ENABLED=0 GOOS=linux GOARCH=amd64 ./make.bash
CGO_ENABLED=0 GOOS=windows GOARCH=amd64 ./make.bash
```

