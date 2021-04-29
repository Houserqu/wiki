Web Worker为Web内容在后台线程中运行脚本提供了一种简单的方法。线程可以执行任务而不干扰用户界面。此外，他们可以使用XMLHttpRequest执行 I/O  (尽管responseXML和通道属性总是为空)。一旦创建， 一个worker 可以将消息发送到创建它的JavaScript代码, 通过将消息发布到该代码指定的事件处理程序 (反之亦然)。

api流程

1. 通过 worker = new Worker( url ) 加载一个JS文件来创建一个worker，同时返回一个worker实例。
2. 通过worker.postMessage( data ) 方法来向worker发送数据。
3. 绑定worker.onmessage方法来接收worker发送过来的数据。
4. 可以使用 worker.terminate() 来终止一个worker的执行。