# Node.js

## 资源

[彻底搞懂 npm、yarn 与 pnpm 依赖管理逻辑](https://mp.weixin.qq.com/s/N2G--m4rGpgXb26X7WZF7Q)

[node-gyp 实现 nodejs 调用 C++ - 掘金](https://juejin.cn/post/6844903971220357134)

## 基础

### package.json

[关于前端大管家 package.json，你知道多少？](https://juejin.cn/post/7023539063424548872)

### 主要模块

[Node.js API 文档](http://nodejs.cn/api/)

| 英文名称                                                     | 功能                                                         |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| [assert（断言）](http://nodejs.cn/api/assert.html#assert_assert) | 断言函数，用于判断表达式结果是否符合预期                     |
| [async_hooks（异步钩子)](http://nodejs.cn/api/async_hooks.html#async_hooks_async_hooks) | 提供了一个用于注册回调函数的 API，实现对异步流程的追踪       |
| [Buffer（缓冲器）](http://nodejs.cn/api/buffer.html#buffer_buffer) | `Buffer` 对象用于表示固定长度的字节序列                      |
| [child_process（子进程）](http://nodejs.cn/api/child_process.html#child_process_child_process) | 提供了衍生子进程，父子进程通过消息进行通讯                   |
| [cluster（集群）](http://nodejs.cn/api/cluster.html#cluster_cluster) | 可以用来创建共享服务器端口的子进程，能够共享任何 TCP 连接    |
| [console（控制台）](http://nodejs.cn/api/console.html#console_console) | 调试控制台，可以打印调试内容                                 |
| [crypto（加密）](http://nodejs.cn/api/crypto.html#crypto_crypto) | 提供了加密功能，对 OpenSSL 的哈希、HMAC、加密、解密、签名、以及验证功能的封装 |
| [debugger（调试器）](http://nodejs.cn/api/debugger.html#debugger_debugger) | 进程外的调试实用程序，可通过 [V8 检查器](http://nodejs.cn/api/debugger.html#debugger_v8_inspector_integration_for_node_js)或内置的调试客户端访问 |
| [dgram（数据报）](http://nodejs.cn/api/dgram.html#dgram_udp_datagram_sockets) | 提供了 UDP 数据报 socket 的实现                              |
| [dns（域名服务器）](http://nodejs.cn/api/dns.html#dns_dns)   | 用于进行域名解析                                             |
| [Error（错误）](http://nodejs.cn/api/errors.html#errors_errors) | 错误对象，会捕获堆栈跟踪，所有错误都实例化自或继承自 `Error` 类 |
| [events（事件触发器）](http://nodejs.cn/api/events.html#events_events) | 提供`EventEmitter`类，是事件触发与事件监听器功能的封装       |
| [fs（文件系统）](http://nodejs.cn/api/fs.html#fs_file_system) | 提供与文件系统进行交互的能力                                 |
| [global（全局变量）](http://nodejs.cn/api/globals.html#globals_global_objects) | NodeJs 提供的全局变量，无需引用即可在模块中使用              |
| [http](http://nodejs.cn/api/http.html#http_http)/[http2](http://nodejs.cn/api/http2.html#http2_http_2)/[https](http://nodejs.cn/api/https.html#https_https) | 创建 HTTP 的服务端和客户端                                   |
| [inspector（检查器）](http://nodejs.cn/api/inspector.html#inspector_inspector) | 提供了与 V8 调试器交互的 API                                 |
| [module（模块）](http://nodejs.cn/api/module.html#module_modules_module_api) | 与模块交互时可用的工具方法                                   |
| [net（网络）](http://nodejs.cn/api/net.html#net_net)         | 用于创建基于流的 TCP 或 [IPC](http://nodejs.cn/api/net.html#net_ipc_support) 的服务器与客户端。http/http2/https 都是继承于该模块 |
| [os（操作系统）](http://nodejs.cn/api/os.html#os_os)         | 提供了与操作系统相关的实用方法和属性                         |
| [path（路径）](http://nodejs.cn/api/path.html#path_path)     | 提供了文件和目录的路径处理工具方法                           |
| [perf_hooks（性能钩子）](http://nodejs.cn/api/perf_hooks.html#perf_hooks_performance_measurement_apis) | 提供了性能时间相关的 API，可以保存和获取性能相关的高精度的度量数据 |
| [process（进程）](http://nodejs.cn/api/process.html#process_process) | `process` 对象是一个全局变量，提供了有关当前 Node.js 进程的信息并对其进行控制 |
| [querystring（查询字符串）](http://nodejs.cn/api/querystring.html#querystring_query_string) | 用于解析和格式化 URL 查询字符串                              |
| [readline（逐行读取）](http://nodejs.cn/api/readline.html#readline_readline) | 提供了一次一行地读取[可读流](http://nodejs.cn/api/stream.html#stream_readable_streams)中数据的接口 |
| [repl（交互式解释器）](http://nodejs.cn/api/repl.html#repl_repl) | 提供了一种“读取-求值-输出”循环（REPL）的实现，直接运行 node 命令也可以进入该模式 |
| [stream（流）](http://nodejs.cn/api/stream.html#stream_stream) | 处理流式数据的抽象接口                                       |
| [string_decoder（字符串解码器）](http://nodejs.cn/api/string_decoder.html#string_decoder_string_decoder) | 将 `Buffer` 对象解码为字符串                                 |
| [timer（定时器）](http://nodejs.cn/api/timers.html#timers_timers) | setTimeOut(), setInterval(), setImmediate()                  |
| [tls（安全传输层）](http://nodejs.cn/api/tls.html#tls_tls_ssl) | 安全传输层（TLS）及安全套接层（SSL）协议的实现，建立在OpenSSL的基础上 |
| [trace_events（跟踪事件）](http://nodejs.cn/api/tracing.html#tracing_trace_events) | 追踪 V8、NodeJS 内核和用户代码的信息                         |
| [url（URL）](http://nodejs.cn/api/url.html#url_url)          | 处理与解析 URL                                               |
| [util（实用工具）](http://nodejs.cn/api/util.html#util_util) | Node.js 内部 API 的会用到的工具方法，开发者也可以使用        |
| [v8（V8引擎）](http://nodejs.cn/api/v8.html#v8_v8)           | 暴露了特定于内置到 Node.js 二进制文件中的 [V8](http://url.nodejs.cn/Nt1LnB) 版本的 API |
| [vm（虚拟机）](http://nodejs.cn/api/vm.html#vm_vm_executing_javascript) | 可以在不同的 V8 上下文中编译和运行代码                       |
| [wasi（WASI）](http://nodejs.cn/api/wasi.html#wasi_webassembly_system_interface_wasi) | 提供了字节码形式的编译目标，允许浏览器可以执行由 C、Go 等语言编写的代码 |
| [worker_threads（工作线程）](http://nodejs.cn/api/worker_threads.html#worker_threads_worker_threads) | 工作线程（子线程），可以与主线程共享内存。（与浏览器中的 Web Work 有差异） |
| [zlib（压缩）](http://nodejs.cn/api/zlib.html#zlib_zlib)     | 模块提供通过 Gzip、Deflate/Inflate、和 Brotli 实现的压缩功能 |

## 原理

![img](http://qiniu.houserqu.com/4111821277-577a300546802_fix732.png)

### 组成

#### V8

C++ 实现的 JS 代码执行引擎。V8 将你写的 JavaScript 代码编译为机器码然后执行。一个 Node 进程包含一个 V8 实例，该实例是多线程的

- 主线程：编译、执行代码。

- 编译/优化线程：在主线程执行的时候，可以优化代码。

- 分析器线程：记录分析代码运行时间，为 Crankshaft 优化代码执行提供依据。

- 垃圾回收的几个线程。

#### libuv

![img](http://qiniu.houserqu.com/FuX1qcGJgwYtX9zNbBAOSaQeD8Qz-20210707205352134.png)

提供异步功能的 C 库。它在运行时负责一个事件循环（Event Loop）、一个线程池、文件系统 I/O、DNS 相关和网络 I/O，以及一些其他重要功能。

对于Network I/O相关的请求， 根据OS平台不同，分别使用Linux上的epoll，OSX和BSD类OS上的kqueue，SunOS上的event ports以及Windows上的IOCP机制。

而对于File I/O为代表的请求，则使用线程池的方式实现异步请求处理。

#### C++ 库

c-ares、crypto、http 等库，提供了对系统底层功能的访问，包括网络、压缩、加密等

#### C/C++Binding

将 Node.js 自带 C/C++ 写的核心库的接口暴露给 JS 环境，允许 JS 直接调用。

#### C/C++ Addons

Binding 仅桥接 Node.js 核心库的一些依赖，其他第三方或者你自己写的 C/C++ 库需要通过他来桥接。

### 进程与线程

[深入理解Node.js 进程与线程](https://segmentfault.com/a/1190000020077274)

- Node.js 虽然是单线程模型，但是其基于事件驱动、异步非阻塞模式，可以应用于高并发场景，避免了线程创建、线程之间上下文切换所产生的资源开销

### 事件循环

![image-20210707221331922](http://qiniu.houserqu.com/image-20210707221331922.png)

> 浏览器也有事件循环，但是并不是由 V8（属于 ECMAScript 标准）提供，而是 Web Environment（属于 W3 C标准的内容）

**执行流程**

- 初始化 NodeJS 运行环境、libuv 线程池、V8 环境
- 创建 NodeJS 运行实例，启动该实例
- V8 引擎解析和执行 JS 代码
- 如果存在异步调用，提交到 libuv 中的事件队列中，libuv 会分配线程去执行，执行完成之后将事件放到指定类型的已就绪事件队列中
- 同步代码执行完毕，进入事件循环
- 在每个事件循环中，事件循环线程按照 FIFO 的顺序从就绪事件队列中取出事件，并交给 V8 执行其回调函数
- 进入下一个事件循环

**时间循环中的各个阶段**

> [Node.js 事件循环，定时器和 `process.nextTick()`](https://nodejs.org/zh-cn/docs/guides/event-loop-timers-and-nexttick/)
>
> [不要混淆nodejs和浏览器中的event loop](https://cnodejs.org/topic/5a9108d78d6e16e56bb80882)

```
   ┌───────────────────────────┐
┌─>│           timers          │
│  └─────────────┬─────────────┘
│  ┌─────────────┴─────────────┐
│  │     pending callbacks     │
│  └─────────────┬─────────────┘
│  ┌─────────────┴─────────────┐
│  │       idle, prepare       │
│  └─────────────┬─────────────┘      ┌───────────────┐
│  ┌─────────────┴─────────────┐      │   incoming:   │
│  │           poll            │<─────┤  connections, │
│  └─────────────┬─────────────┘      │   data, etc.  │
│  ┌─────────────┴─────────────┐      └───────────────┘
│  │           check           │
│  └─────────────┬─────────────┘
│  ┌─────────────┴─────────────┐
└──┤      close callbacks      │
   └───────────────────────────┘
```

每个阶段都有一个要执行的事件回调 FIFO 队列，如果队列耗尽或达到最大执行回调数量，则进入下一个阶段。

- timers：此阶段执行由 `setTimeout` 和 `setInterval` 设置的回调。
- pending callbacks：某些由特殊的系统操作触发的callback(如某些TCP error)会在此阶段被执行. 例如, 尝试建立TCP连接时触发`ECONNREFUSED`错误, 则关联的callback会被调用。
- idle, prepare：仅在内部使用。
- poll：执行与 I/O 相关的事件回调。如果队列为空，node 将在此处阻塞等待一定时间（如果 immediates 队列有 callback 待执行，则会直接结束该阶段）。
- check：在这里调用 `setImmediate` 回调（在I/O回调中，`setImmediate` 一定后于 `setTimeout` 执行）。
- close callbacks：一些关闭回调，例如 socket.on('close', ...)。

process.nextTick(): 独立于事件循环异步 API，该方法接受的回调函数会被添加到 `nextTickQueue`，当前同步代码执行完后立即执行该队列里的回调，无论当前处于事件循环的哪个阶段。（应用场景：需要等后面的同步代码执行完之后，立即执行的操作，例如释放资源，触发事件）

事件轮询线程执行事件的回调函数，并且负责对处理类似网络 I/O 的非阻塞异步请求（如果回调中有异步请求）。

**net 模块处理请求流程的函数调用**

![img](http://qiniu.houserqu.com/56014909-b8624100-5d29-11e9-9542-66c04acae9f8.png)

####  性能优化

**优化原则：不要阻塞事件循环线程**

https://nodejs.org/zh-cn/docs/guides/dont-block-the-event-loop/

对一个复杂的任务，最好把它从事件循环线程转移到工作线程池上。

每个相对长的任务会直接减少了工作线程池的可用线程数量，直到它的任务完成

将任务拆分为子任务时，较短的任务将拆分为少量的子任务，而更长的任务将拆分为更多的子任务。 在较长任务的每个子任务之间，分配给它的工作线程可以调度执行另一个更短的任务拆分出来的子任务，从而提高工作池的总体任务吞吐量。

Node.js 有两种类型的线程：一个事件循环线程和 `k` 个工作线程。 事件循环负责 JavaScript 回调和非阻塞 I/O，工作线程执行与 C++ 代码对应的、完成异步请求的任务，包括阻塞 I/O 和 CPU 密集型工作。这两种类型的线程一次都只能处理一个活动。所以尽可能保证这两种线程都不要被阻塞。

### 模块化

#### 模块加载顺序	

##### 阶段1. 粗查阶段

- 如果是node核心模块，就直接返回模块名称
- 如果是引入的第三方npm模块，会返回父级所在文件夹下的node_modules，父父级所在文件夹下的node_modules，依次递归，一直到/node_modules和用户名下的.node_modules以及全局环境变量配置的全局安装的模块文件夹组成的数组
- 如果是相对路径引入的模块，会将相对路径和父级路径之间进行一个path.resolve()，然后返回

##### 阶段2. 精确查找，获取文件绝对路径

以require('express')为例

- 先尝试加载node_modules/express，这种没有扩展名的文件是否存在
- 尝试按照扩展名规则查找，依次判断node_modules文件夹下.js .json .node结尾的文件名为express的文件是否存在，返回文件的绝对路径
- 判断node_modules/express文件夹下的package.json是否存在，如果存在，返回main字段指定的文件的绝对路径
- 判断node_modules/express/index.js是否存在，存在返回对应文件绝对路径

### path

```js
__dirname          // 返回当前模块所在目录的绝对路径 (类似 path.dirname())
__filename         // 返回前模块的绝对路径
path.basename('/目录1/目录2/文件.html');  // 返回: '文件.html' 【返回最后一部分】
path.extname('index.coffee.md');        // 返回: '.md' 【拓展名】
path.join('目录1', '目录2', '目录3/目录4') // 返回: '目录1/目录2/目录3/目录4' 【将路径片段生成规范的路径】
path.basename('/目录1/目录2/文件.html');  // 返回: '文件.html' 【返回路径最后一部分】
path.resolve('/目录1/目录2', './目录3');  // 返回: '/目录1/目录2/目录3' 【返回绝对路径】处理流程类似依次 cd， pwd

// path 对象组成，如果存在 dir，则忽略 root，如果存在 base，则忽略 name 和 ext
┌─────────────────────┬────────────┐
│          dir        │    base    │
├──────┬              ├──────┬─────┤
│ root │              │ name │ ext │
"  /    目录1/目录2    / 文件   .txt "
└──────┴──────────────┴──────┴─────┘
```

### crypto

> 待完善

### url

上方的是传统的 `url.parse()` 返回的对象的属性。 下方的则是 [WHATWG](https://url.spec.whatwg.org/) 的 `URL` 对象的属性

```
┌────────────────────────────────────────────────────────────────────────────────────────────────┐
│                                              href                                              │
├──────────┬──┬─────────────────────┬────────────────────────┬───────────────────────────┬───────┤
│ protocol │  │        auth         │          host          │           path            │ hash  │
│          │  │                     ├─────────────────┬──────┼──────────┬────────────────┤       │
│          │  │                     │    hostname     │ port │ pathname │     search     │       │
│          │  │                     │                 │      │          ├─┬──────────────┤       │
│          │  │                     │                 │      │          │ │    query     │       │
"  https:   //    user   :   pass   @ sub.example.com : 8080   /p/a/t/h  ?  query=string   #hash "
│          │  │          │          │    hostname     │ port │          │                │       │
│          │  │          │          ├─────────────────┴──────┤          │                │       │
│ protocol │  │ username │ password │          host          │          │                │       │
├──────────┴──┼──────────┴──────────┼────────────────────────┤          │                │       │
│   origin    │                     │         origin         │ pathname │     search     │ hash  │
├─────────────┴─────────────────────┴────────────────────────┴──────────┴────────────────┴───────┤
│                                              href                                              │
└────────────────────────────────────────────────────────────────────────────────────────────────┘
```



## 性能分析

[对node工程进行压力测试与性能分析](https://juejin.cn/post/6844903665166188551)

### 内存泄漏

常见原因：

- 全局变量：全局变量不会被清除，定义了太多全局变量或挂载了大量数据
- 闭包：如果闭包函数没有被释放，那么他引用的父函数里的变量也不会被释放
- 事件监听：对相同的事件进行重复监听，没有移除
- 缓存：在内存中缓存了太多数据
- 阻塞请求：执行了CPU耗时任务，后面进来的请求一直无法被处理而堆积

内存快照：

heapdump 工具可以记录内存快照，然后通过 Chrome Memory 工具可以分析内存。

[使用 chrome-devtools Memory 面板](https://zhuanlan.zhihu.com/p/80792297)

## 技术

### 命令行工具开发

[命令行工具开发](Node%20js%20ca596fd24ea04188946c20e6b2ccf656/%E5%91%BD%E4%BB%A4%E8%A1%8C%E5%B7%A5%E5%85%B7%E5%BC%80%E5%8F%91%203b33f9b2bde84470aba11d2383174b2c.md)

- shelljs 方便调用系统 shell  命令
- yargs 方便处理命令行参数

## NPM

**peerDependencies**

目的是提示宿主环境去安装满足插件peerDependencies所指定依赖的包，然后在插件import或者require所依赖的包的时候，永远都是引用宿主环境统一安装的npm包，最终解决插件与所依赖包不一致的问题

## 模块化

### 模块引入顺序

首先加载核心模块,不管有没有同名/同目录的情况下,核心模块优先加载. 

其次按照相对路径/绝对路径加载文件模块(加载顺序,首先试图按照路径查找 .js 扩展名的文件,如果没有,试图按照路径查找 .json 扩展名的文件,如果还是没有,就按照路径查找 .node 扩展名的c++模块了) 

最后搜索 node_modules 目录下通过npm下载的第三方模块.  

注意:首次加载这类模块最慢,因为执行文件所在目录的node_mondel 文件夹下找不到时,会去父级node_mondel 文件夹里查找,如果还是找不到会去父级的父级node_mondel 文件夹里查找.......但是,只要首次加载成功后,node就会缓存起来,它缓存的是编译后的二进制模块,所以以后的加载速度和效率都的有保证的. 

### 简单模块化

1. 通过script标签实现模块化，但是依然会造成变量污染，而且还需要人为控制顺序

2. 通过立即执行函数进行函数作用域的隔离

### nodejs的规范CommonJs

一个文件就是一个模块，文件名就是模块的名字，使用模块的方法也和commonjs中一致，只需require就好了。CommonJS 模块在 require 的时候会立即执行模块文件里的代码，并缓存，当第二次 require 相同的文件的时候，直接从缓存中读取结果，效果跟 es6 模块一样。

```
module.export = add
var add = require('math');
```

缺点：

- 同步加载
- 不能非阻塞的并行加载多个模块

### AMD：Asynchronous Module Definition异步模块定义

示例

```
define("module", ["dep1", "dep2"], function(d1, d2) {
  return someExportedValue;
});
require(["module", "../file"], function(module, file) { /* ... */ });
```

优点：

- 适合在浏览器环境中异步加载模块
- 可以并行加载多个模块

缺点：

- 提高了开发成本，代码的阅读和书写比较困难，模块定义方式的语义不顺畅
- 不符合通用的模块化思维方式，是一种妥协的实现

### CMD规范

与 CommonJS 和 Node.js 的 Modules 规范保持了很大的兼容性。在 CMD 规范中，一个模块就是一个文件。

```
define(function(require, exports, module) {
  var $ = require('jquery');
  var Spinning = require('./spinning');
  exports.doSomething = ...
  module.exports = ...
})
```

### AMD和CMD的区别

1、对于依赖的模块，AMD是提前执行，CMD是延迟执行。
2、AMD推崇依赖前置；CMD推崇依赖就近，只有在用到某个模块的时候再去require。

### ES6模块化

ES6 模块的设计思想，是尽量的静态化，使得**编译时就能确定模块的依赖关系**，以及输入和输出的变量，能够提供更好的**变量类型检查**。CommonJS和AMD模块，都只能在运行时确定这些东西。es6 module 在声明 import 时并不会执行对应模块文件里的代码，而是在使用到了该模块导出的值的时候，才会去执行。es6 模块是【**单例】**的，一个模块只会执行一次，第二次读取该模块导出的变量的时候，直接从内存中读取。

es6 模块和 CommonJS 模块主要的区别是引用，前者不会立即执行，但是必须写在文件顶部，用于静态引用关系分析，后者在引用的时候立即执行，可以在代码任何位置去 require

[参考链接](http://xieyufei.com/2017/02/19/JS-Standard.html)

