# Node.js特性以及原理

## Nodejs是什么
提到Javascript ,大家首先想到的是日常使用的浏览器,现代浏览器包含了各种组件,包括渲染引擎,Javascript引擎等,其中 Javascript 引擎负责解释执行网页中的 Javascript 代码。作为Web前端最重要的语言之一, Javascript 一直是前端工程师的专利。不过, Node.js 是一个后端的 Javascript 运行环境(支持的系统包括 *nux 、 Windows ),这意味着你可以编写系统级或者服务器端的 Javascript 代码,交给 Node.js 来解释执行。

Nodejs特性
* 事件驱动
* 异步编程
* 简易的网络编程
* 单进程,单线程

`事件驱动`当我们在浏览器编写Javascript代码写一个点击下拉菜单的代码的时候,就是给Dom元素注册一个监听click事件的回调函数。而在我们编写ajax收发api接口的时候,我们不知道服务器什么时候会返回数据,所以我们一遍会写出类似下方的回调函数,在客户端接收到服务器返回的json数据后,这种方式就是`异步编程`,同样的道理,对于每一个请求,服务器需要读取一个很大的文件,并返回这个文件,那么有两种方式读取
* 同步
* 异步

如果同步读取,那么对于服务器,每次请求,服务器开始读取文件,然后拒绝其他请求接入,等返回给客户端后再去接收下一个请求
如果是异步,那么对于服务器,每次请求,服务器开始读取文件,同时接收下一个请求,如果文件读取完成,回调读取文件的内容,并返回客户端文件内容


```js
$.ajax({
url:'/demo'
sucess:function(rtn){
    console.log(rtn);
    }
});
```

使用原生nodejs,创建一个简单的服务器,了解异步编程模型

helloworld.js
```js
// 加载http网络模块
var http = require('http');
// 创建http服务器
http.createServer(function (req, res) {

// 响应的状态码(status code) ,
res.writeHead(200, {'Content-Type': 'text/pla
in'});

//服务器返回Hello World   \n 是换行符
res.end('Hello World\n');
}).listen(80, "127.0.0.1");

```
运行helloworld.js
```js
node helloworld.js
```


## 单进程,单线程
Node.js 的性能不错。按照创始人 Ryan Dahl 的说法,性能是Node.js考虑的重要因素,选择 C++ 和 V8 而不是 Ruby 或者其他的虚拟机也是基于性能的目的。
Node.js 在设计上也是比较大胆,它以单进程、单线程 模式运行(很吃惊,对
吧?这和 Javascript 的运行方式一致),事件驱动机制是 Node.js 通过内部单线程高效率地维护事件循环队列来实现的,没有多线程的资源占用和上下文切换,这意味着面对大规模的 http 请求, Node.js 凭借事件驱动搞定一切,习惯了传统语言的网络服务开发人员可能对多线程并发和协作非常熟悉,但是面对Node.js ,我们需要接受和理解它的特点。
