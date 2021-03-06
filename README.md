# node-beginner

Node.js Web 开发入门

> Node.js tutorial for beginners <https://www.nodebeginner.org>
>
> 作者： [Manuel Kiessling](https://github.com/manuelkiessling/nodebeginner.org) 翻译： goddyzhao & GrayZhang & MondayChen

原文太啰嗦，我来简化下。

---

- [node-beginner](#node-beginner)
    - [1 绪论](#1-%E7%BB%AA%E8%AE%BA)
        - [1.1 读者对象](#11-%E8%AF%BB%E8%80%85%E5%AF%B9%E8%B1%A1)
        - [1.2 本书结构](#12-%E6%9C%AC%E4%B9%A6%E7%BB%93%E6%9E%84)
    - [2 JavaScript与Node.js](#2-javascript%E4%B8%8Enodejs)
        - [2.1 介绍](#21-%E4%BB%8B%E7%BB%8D)
        - [2.2 “Hello World”](#22-hello-world)
    - [3 一个完整的基于Node.js的web应用](#3-%E4%B8%80%E4%B8%AA%E5%AE%8C%E6%95%B4%E7%9A%84%E5%9F%BA%E4%BA%8Enodejs%E7%9A%84web%E5%BA%94%E7%94%A8)
        - [3.1 目标](#31-%E7%9B%AE%E6%A0%87)
        - [3.2 应用不同模块分析](#32-%E5%BA%94%E7%94%A8%E4%B8%8D%E5%90%8C%E6%A8%A1%E5%9D%97%E5%88%86%E6%9E%90)
    - [4 构建应用的模块](#4-%E6%9E%84%E5%BB%BA%E5%BA%94%E7%94%A8%E7%9A%84%E6%A8%A1%E5%9D%97)
        - [4.1 一个基础的HTTP服务器](#41-%E4%B8%80%E4%B8%AA%E5%9F%BA%E7%A1%80%E7%9A%84http%E6%9C%8D%E5%8A%A1%E5%99%A8)
        - [4.2 分析HTTP服务器](#42-%E5%88%86%E6%9E%90http%E6%9C%8D%E5%8A%A1%E5%99%A8)
        - [4.3 进行函数传递](#43-%E8%BF%9B%E8%A1%8C%E5%87%BD%E6%95%B0%E4%BC%A0%E9%80%92)
        - [4.4 函数传递是如何让HTTP服务器工作的](#44-%E5%87%BD%E6%95%B0%E4%BC%A0%E9%80%92%E6%98%AF%E5%A6%82%E4%BD%95%E8%AE%A9http%E6%9C%8D%E5%8A%A1%E5%99%A8%E5%B7%A5%E4%BD%9C%E7%9A%84)
        - [4.5 基于事件驱动的回调](#45-%E5%9F%BA%E4%BA%8E%E4%BA%8B%E4%BB%B6%E9%A9%B1%E5%8A%A8%E7%9A%84%E5%9B%9E%E8%B0%83)
        - [4.6 服务器是如何处理请求的](#46-%E6%9C%8D%E5%8A%A1%E5%99%A8%E6%98%AF%E5%A6%82%E4%BD%95%E5%A4%84%E7%90%86%E8%AF%B7%E6%B1%82%E7%9A%84)
        - [4.7 服务端的模块放在哪里](#47-%E6%9C%8D%E5%8A%A1%E7%AB%AF%E7%9A%84%E6%A8%A1%E5%9D%97%E6%94%BE%E5%9C%A8%E5%93%AA%E9%87%8C)
        - [4.8 如何来进行请求的“路由”](#48-%E5%A6%82%E4%BD%95%E6%9D%A5%E8%BF%9B%E8%A1%8C%E8%AF%B7%E6%B1%82%E7%9A%84%E8%B7%AF%E7%94%B1)
        - [4.9 行为驱动执行](#49-%E8%A1%8C%E4%B8%BA%E9%A9%B1%E5%8A%A8%E6%89%A7%E8%A1%8C)
        - [4.10 路由给真正的请求处理程序](#410-%E8%B7%AF%E7%94%B1%E7%BB%99%E7%9C%9F%E6%AD%A3%E7%9A%84%E8%AF%B7%E6%B1%82%E5%A4%84%E7%90%86%E7%A8%8B%E5%BA%8F)
        - [4.11 让请求处理程序作出响应](#411-%E8%AE%A9%E8%AF%B7%E6%B1%82%E5%A4%84%E7%90%86%E7%A8%8B%E5%BA%8F%E4%BD%9C%E5%87%BA%E5%93%8D%E5%BA%94)
        - [4.12 不好的实现方式](#412-%E4%B8%8D%E5%A5%BD%E7%9A%84%E5%AE%9E%E7%8E%B0%E6%96%B9%E5%BC%8F)
        - [4.13 阻塞与非阻塞](#413-%E9%98%BB%E5%A1%9E%E4%B8%8E%E9%9D%9E%E9%98%BB%E5%A1%9E)
        - [4.14 错误的使用非阻塞操作](#414-%E9%94%99%E8%AF%AF%E7%9A%84%E4%BD%BF%E7%94%A8%E9%9D%9E%E9%98%BB%E5%A1%9E%E6%93%8D%E4%BD%9C)
        - [4.15 以非阻塞操作进行请求响应](#415-%E4%BB%A5%E9%9D%9E%E9%98%BB%E5%A1%9E%E6%93%8D%E4%BD%9C%E8%BF%9B%E8%A1%8C%E8%AF%B7%E6%B1%82%E5%93%8D%E5%BA%94)
    - [5 更有用的场景](#5-%E6%9B%B4%E6%9C%89%E7%94%A8%E7%9A%84%E5%9C%BA%E6%99%AF)
        - [5.1 处理POST请求](#51-%E5%A4%84%E7%90%86post%E8%AF%B7%E6%B1%82)
        - [5.2 处理文件上传](#52-%E5%A4%84%E7%90%86%E6%96%87%E4%BB%B6%E4%B8%8A%E4%BC%A0)
    - [6 总结与展望](#6-%E6%80%BB%E7%BB%93%E4%B8%8E%E5%B1%95%E6%9C%9B)

---

## 1 绪论

本书是一本“从初级入门到高级入门”的书，将教你如何用Node.js来开发Web应用，和所需的JavaScript知识。

### 1.1 读者对象

至少对一门诸如Python、Ruby、PHP或者Java这样面向对象的语言有一定的经验；对JavaScript处于初学阶段，并且完全是一个Node.js的新手。

本书不会对诸如数据类型、变量、控制结构等基础概念作介绍，但还是会对JavaScript中的函数和对象作详细介绍，因为它们与其他同类编程语言中的有很大的不同。

### 1.2 本书结构

读完本书之后，你将完成一个完整的web应用，该应用允许用户浏览页面以及上传文件。

相比为了实现该功能书写的代码本身，我们更关注的是如何创建一个框架来对我们应用的不同模块进行干净地剥离。

本书先介绍JavaScript和Node.js，实现最基础的Node.js应用“Hello World”。

然后，讨论如何设计一个“真正”完整的应用，分析应用需要实现的不同模块，及如何实现这些模块。

该应用所有的源代码都可以通过 [本书Github代码仓库](https://github.com/manuelkiessling/nodebeginner.org/tree/master/code/application)。

## 2 JavaScript与Node.js

### 2.1 介绍

JavaScript最早是运行在浏览器中，为web页面添加交互，属于前端技术。

后来，Node.js出现，它允许在后端（脱离浏览器环境）运行JavaScript代码。

要实现在后台运行JavaScript代码，就需要解释器来被解释和执行代码。Node.js使用了Google的V8虚拟机（Google的Chrome浏览器使用的JavaScript执行环境），来解释和执行JavaScript代码。

Node.js生态系统包括众多第三方模块，大大简化开发过程。

要使用Node.js,首先需要进行安装。关于如何安装Node.js，可以直接参考官方的[安装指南](https://nodejs.org/zh-cn/)。

### 2.2 “Hello World”

开始我们的第一个Node.js应用：“Hello World”。

打开你最喜欢的编辑器，创建一个helloworld.js文件。我们要做就是向STDOUT输出“Hello World”，代码如下：

```js
console.log('Hello World');
```

保存该文件，并通过Node.js来执行：

```sh
node helloworld.js
```

正确的话，终端输出Hello World 。

## 3 一个完整的基于Node.js的web应用

### 3.1 目标

我们来把目标设定得简单实际点：

- 用户可以通过浏览器使用我们的应用
- 当用户请求<http://domain/start>时，可以看到一个欢迎页面，页面上有一个文件上传的表单
- 用户可以选择一个图片并提交表单，随后文件将被上传到<http://domain/upload>，该页面完成上传后会把图片显示在页面上

在完成这一目标的过程中，我们不仅需要基础的代码，还要对此进行抽象，来寻找一种适合构建更为复杂的Node.js应用的方式。

### 3.2 应用不同模块分析

我们来分解一下这个应用，为了实现上面的目标，我们需要实现哪些部分呢？

- 我们需要提供Web页面，因此需要一个HTTP服务器
- 对于不同的请求，根据请求的URL，我们的服务器需要给予不同的响应，因此我们需要一个路由，用于把请求对应到请求处理程序（request handler）
- 当请求被服务器接收并通过路由传递之后，需要可以对其进行处理，因此我们需要最终的请求处理程序
- 路由还应该能处理POST数据，并且把数据封装成更友好的格式传递给请求处理入程序，因此需要请求数据处理功能
- 我们不仅仅要处理URL对应的请求，还要把内容显示出来，这意味着我们需要一些视图逻辑供请求处理程序使用，以便将内容发送给用户的浏览器
- 最后，用户需要上传图片，所以我们需要上传处理功能来处理这方面的细节

使用Node.js时，我们不仅在实现一个应用，同时还实现了HTTP服务器。事实上，我们的Web应用以及对应的Web服务器基本上是一样的。

听起来很多，但对Node.js来说不难。

现在我们就先从第一个部分 —— HTTP服务器着手。

## 4 构建应用的模块

### 4.1 一个基础的HTTP服务器

让我们先从服务器模块开始。在你的项目的根目录下创建一个叫server.js的文件，并写入以下代码：

```js
var http = require("http");

http.createServer(function(request, response) {
  response.writeHead(200, {"Content-Type": "text/plain"});
  response.write("Hello World");
  response.end();
}).listen(8888);
```

搞定！你刚刚完成了一个可以运行的HTTP服务器。我们来运行并且测试这段代码。首先，用Node.js执行你的脚本：

```sh
node server.js
```

接下来，打开浏览器访问<http://localhost:8888/>，你会看到一个写着“Hello World”的网页。

### 4.2 分析HTTP服务器

让我们分析一下这个HTTP服务器的构成。

第一行请求（require）Node.js自带的 http 模块，并且把它赋值给 http 变量。

接下来我们调用http模块提供的函数： `createServer` 。这个函数会返回一个对象，这个对象有一个叫做 listen 的方法，这个方法有一个数值参数，指定服务器监听的端口号。

先不管 http.createServer 的括号里的那个函数定义，我们可以用下面的代码来启动服务器并侦听8888端口：

```js
var http = require("http");

var server = http.createServer();
server.listen(8888);
```

这段代码只会启动一个侦听8888端口的服务器，它不做任何别的事情，甚至连请求都不会应答。

最有趣的部分是 createServer() 的第一个参数，一个函数定义。在JavaScript中，函数和其他变量一样都是可以被传递的。

### 4.3 进行函数传递

举例来说，你可以这样做：

```js
function say(word) {
  console.log(word);
}

function execute(someFunction, value) {
  someFunction(value);
}

execute(say, "Hello");
```

请仔细阅读这段代码！在这里，我们把 say 函数作为execute函数的第一个变量进行了传递。这里传递的**不是 say 的返回值**，而是 say 本身！

这样一来， say 就变成了execute 中的本地变量 someFunction ，execute可以通过调用 someFunction() （带括号的形式）来使用 say 函数。

当然，因为 say 有一个变量， execute 在调用 someFunction 时可以传递这样一个变量。

我们可以，用函数名，把一个函数作为变量传递。但是我们不一定要绕这个“先定义，再传递”的圈子，我们可以直接在另一个函数的括号中定义和传递这个函数：

```js
function execute(someFunction, value) {
  someFunction(value);
}

execute(function(word){ console.log(word) }, "Hello");
```

我们在 execute 接受第一个参数的地方直接定义了我们准备传递给 execute 的函数。

用这种方式，我们甚至不用给这个函数起名字，这也是为什么它被叫做 **匿名函数** 。

在JavaScript中，我们可以先定义一个函数，然后传递，也可以在传递参数的地方直接定义函数。

### 4.4 函数传递是如何让HTTP服务器工作的

带着这些知识，我们再来看看我们简约而不简单的HTTP服务器：

```js
var http = require("http");

http.createServer(function(request, response) {
  response.writeHead(200, {"Content-Type": "text/plain"});
  response.write("Hello World");
  response.end();
}).listen(8888);
```

现在它看上去应该清晰了很多：我们向 createServer 函数传递了一个匿名函数。

用这样的代码也可以达到同样的目的：

```js
var http = require("http");

function onRequest(request, response) {
  response.writeHead(200, {"Content-Type": "text/plain"});
  response.write("Hello World");
  response.end();
}

http.createServer(onRequest).listen(8888);
```

也许现在我们该问这个问题了：我们为什么要用这种方式呢？

### 4.5 基于事件驱动的回调

在我们的Node.js程序中，当一个新的请求到达8888端口的时候，我们怎么控制流程呢？

这就是Node.js/JavaScript的事件驱动设计的作用了。

我们创建了服务器，并向创建它的方法传递了一个函数。无论何时我们的服务器收到一个请求，这个函数就会被调用。

我们不知道这件事情什么时候会发生，但是我们现在有了一个处理请求的地方：它就是我们传递过去的那个函数。至于它是被预先定义的函数还是匿名函数，就无关紧要了。

这就是 回调 。我们给某个方法传递了一个函数，这个方法在相应事件发生时调用这个函数来进行 回调 。

我们再添加两条输出，在 onRequest（我们的回调函数）触发的地方，和HTTP服务器开始工作之后，用 console.log 输出文本。代码如下：

```js
var http = require("http");

function onRequest(request, response) {
  console.log("Request received.");
  response.writeHead(200, {"Content-Type": "text/plain"});
  response.write("Hello World");
  response.end();
}

http.createServer(onRequest).listen(8888);

console.log("Server has started.");
```

运行`node server.js`时，命令行上输出“Server has started.”。

当我们向服务器发出请求（在浏览器访问<http://localhost:8888/>），“Request received.”这条消息就会在命令行中出现。

这就是事件驱动的异步服务器端JavaScript和它的回调啦！

> 注意，当我们在服务器访问网页时，我们的服务器可能会输出两次“Request received.”。那是因为大部分浏览器都会在你访问 <http://localhost:8888/> 时尝试读取 <http://localhost:8888/favicon.ico>

### 4.6 服务器是如何处理请求的

接下来我们简单分析回调函数 onRequest() 的主体部分。

当回调启动，我们的 onRequest() 函数被触发的时候，有两个参数被传入： request 和 response 。

它们是对象，你可以使用它们的方法来处理HTTP请求的细节，并且响应请求（比如向发出请求的浏览器发回一些东西）。

所以我们的代码就是：当收到请求时，使用 response.writeHead() 函数发送一个HTTP状态200和HTTP头的内容类型（content-type），使用 response.write() 函数在HTTP相应主体中发送文本“Hello World"。

最后，我们调用 response.end() 完成响应。

目前，我们对请求的细节并不在意，所以我们没有使用 request 对象。

### 4.7 服务端的模块放在哪里

可以把所有代码放在一个文件里吗？

实际上，为了便于维护，保持代码的可读性，我们把不同功能的代码放入不同的模块中，保持代码分离。
这种方法允许你拥有一个简洁的主文件，你可以用Node.js执行它；同时你可以拥有简洁的模块，它们可以被主文件和其他的模块调用。

通常我们会有一个叫 index.js 的文件去调用其他模块来引导和启动应用。

怎么把server.js变成一个真正的Node.js模块，使它可以被index.js 主文件使用。

也许你已经注意到，我们已经在代码中使用了模块了。像这样：

```js
var http = require("http");
...
http.createServer(...);
```

Node.js中自带了一个叫做“http”的模块，我们在我们的代码中请求它并把返回值赋给一个本地变量。

这把我们的本地变量变成了一个拥有所有 http 模块所提供的公共方法的对象。

我们怎么创建自己的模块，又怎么使用它呢？

把某段代码变成模块意味着我们需要把我们希望提供其功能的部分 导出 到请求这个模块的脚本。

目前，我们的HTTP服务器需要导出的功能非常简单，因为请求服务器模块的脚本仅仅是需要启动服务器而已。

我们把服务器脚本放到一个叫做 start 的函数里，然后会导出这个函数。

```js
var http = require("http");

function start() {
  function onRequest(request, response) {
    console.log("Request received.");
    response.writeHead(200, {"Content-Type": "text/plain"});
    response.write("Hello World");
    response.end();
  }

  http.createServer(onRequest).listen(8888);
  console.log("Server has started.");
}

exports.start = start;
```

这样，我们现在就可以创建我们的主文件 index.js 并在其中启动我们的HTTP了，虽然服务器的代码还在 server.js 中。

创建 index.js 文件并写入以下内容：

```js
var server = require("./server");

server.start();
```

我们可以像使用其他内置模块一样使用server模块：require这个文件并把它指向一个变量，我们就可以使用模块中已导出的函数了。

现在，我们可以这样启动应用了：

```sh
node index.js
```

我们现在可以把应用的不同部分放入不同的文件里，并且通过生成模块的方式把它们连接到一起了。

我们实现了应用的最初部分：接收HTTP请求。但是对于不同的URL请求，服务器应该有不同的反应。处理不同的HTTP请求，就需要做“路由选择”。我们接下来就创造一个叫做 路由 的模块吧。

### 4.8 如何来进行请求的“路由”

我们需要查看HTTP请求，从中提取出请求的URL以及GET/POST参数。

我们需要的所有数据都会包含在request对象中，该对象作为onRequest()回调函数的第一个参数传递。但是为了解析这些数据，我们需要额外的Node.JS模块，它们分别是url和querystring模块。

```js
                                 url.parse(string).query
                                           |
            url.parse(string).pathname     |
                       |                   |
                       |                   |
                      ----- -------------------
http://localhost:8888/start?foo=bar&hello=world
                            ------  -----------
                                |        |
                                |        |
            querystring(string)["foo"]   |
                                         |
                    querystring(string)["hello"]
```

现在我们来给onRequest()函数加上一些逻辑，用来找出浏览器请求的URL路径：

```js
var http = require("http");
var url = require("url");

function start() {
  function onRequest(request, response) {
    var pathname = url.parse(request.url).pathname;
    console.log("Request for " + pathname + " received.");
    response.writeHead(200, {"Content-Type": "text/plain"});
    response.write("Hello World");
    response.end();
  }

  http.createServer(onRequest).listen(8888);
  console.log("Server has started.");
}

exports.start = start;
```

好了，我们的应用现在可以通过请求的URL路径来区别不同请求了--这使我们得以使用路由（还未完成）来将请求以URL路径为基准映射到处理程序上。

在我们所要构建的应用中，这意味着来自/start和/upload的请求可以使用不同的代码来处理。稍后我们将看到这些内容是如何整合到一起的。

现在我们可以来编写路由了，建立一个名为router.js的文件，添加以下内容：

```js
function route(pathname) {
  console.log("About to route a request for " + pathname);
}

exports.route = route;
```

如你所见，这段代码什么也没干，不过对于现在来说这是应该的。在添加更多的逻辑以前，我们先来看看如何把路由和服务器整合起来。

我们的服务器应当知道路由的存在并加以有效利用。我们当然可以通过硬编码的方式将这一依赖项绑定到服务器上，但是其它语言的编程经验告诉我们这会是一件非常痛苦的事，因此我们将使用依赖注入的方式较松散地添加路由模块（你可以读读Martin Fowlers关于依赖注入的大作来作为背景知识）。

首先，我们来扩展一下服务器的start()函数，以便将路由函数作为参数传递过去：

```js
var http = require("http");
var url = require("url");

function start(route) {
  function onRequest(request, response) {
    var pathname = url.parse(request.url).pathname;
    console.log("Request for " + pathname + " received.");

    route(pathname);

    response.writeHead(200, {"Content-Type": "text/plain"});
    response.write("Hello World");
    response.end();
  }

  http.createServer(onRequest).listen(8888);
  console.log("Server has started.");
}

exports.start = start;
```

同时，我们会相应扩展index.js，使得路由函数可以被注入到服务器中：

```js
var server = require("./server");
var router = require("./router");

server.start(router.route);
```

在这里，我们传递的函数依旧什么也没做。

如果现在启动应用（node index.js，始终记得这个命令行），随后请求一个URL，你将会看到应用输出相应的信息，这表明我们的HTTP服务器已经在使用路由模块了，并会将请求的路径传递给路由。

### 4.9 行为驱动执行

请允许我再次脱离主题，在这里谈一谈函数式编程。

将函数作为参数传递并不仅仅出于技术上的考量。对软件设计来说，这其实是个哲学问题。想想这样的场景：在index文件中，我们可以将router对象传递进去，服务器随后可以调用这个对象的route函数。

就像这样，我们传递一个东西，然后服务器利用这个东西来完成一些事。嗨那个叫路由的东西，能帮我把这个路由一下吗？

但是服务器其实不需要这样的东西。它只需要把事情做完就行，其实为了把事情做完，你根本不需要东西，你需要的是动作，动作就是函数方法。

### 4.10 路由给真正的请求处理程序

路由，是指我们要针对不同的URL有不同的处理方式。例如处理/start的“业务逻辑”就应该和处理/upload的不同。

路由模块并不是真正针对请求“采取行动”的模块，否则当我们的应用程序变得更为复杂时，将无法很好地扩展。

我们暂时把作为路由目标的函数称为请求处理程序。我们来创建一个叫做requestHandlers的模块，并对于每一个请求处理程序，添加一个占位用函数，随后将这些函数作为模块的方法导出：

```js
// requestHandlers.js
function start() {
  console.log("Request handler 'start' was called.");
}

function upload() {
  console.log("Request handler 'upload' was called.");
}

exports.start = start;
exports.upload = upload;
```

这样我们就可以把请求处理程序和路由模块连接起来，让路由“有路可寻”。

那么我们要怎么传递这些请求处理程序呢？别看现在我们只有2个处理程序，在一个真实的应用中，请求处理程序的数量会不断增加，我们当然不想每次有一个新的URL或请求处理程序时，都要为了在路由里完成请求到处理程序的映射而反复折腾。除此之外，在路由里有一大堆if request == x then call handler y也使得系统丑陋不堪。

在JavaScript中，对象就是一个键/值对的集合 -- 你可以把JavaScript的对象想象成一个键为字符串类型的字典。JavaScript的对象的值可以是字符串、数字或者……函数！

现在我们已经确定将一系列请求处理程序通过一个对象来传递，并且需要使用松耦合的方式将这个对象注入到route()函数中。

我们先将这个对象引入到主文件index.js中：

```js
var server = require("./server");
var router = require("./router");
var requestHandlers = require("./requestHandlers");

var handle = {}
handle["/"] = requestHandlers.start;
handle["/start"] = requestHandlers.start;
handle["/upload"] = requestHandlers.upload;

server.start(router.route, handle);
```

正如所见，将不同的URL映射到相同的请求处理程序上是很容易的：只要在对象中添加一个键为"/"的属性，对应requestHandlers.start即可，这样我们就可以干净简洁地配置/start和/的请求都交由start这一处理程序处理。

在完成了对象的定义后，我们把它作为额外的参数传递给服务器，为此将server.js修改如下：

```js
var http = require("http");
var url = require("url");

function start(route, handle) {
  function onRequest(request, response) {
    var pathname = url.parse(request.url).pathname;
    console.log("Request for " + pathname + " received.");

    route(handle, pathname);

    response.writeHead(200, {"Content-Type": "text/plain"});
    response.write("Hello World");
    response.end();
  }

  http.createServer(onRequest).listen(8888);
  console.log("Server has started.");
}

exports.start = start;
```

这样我们就在start()函数里添加了handle参数，并且把handle对象作为第一个参数传递给了route()回调函数。

然后我们相应地在route.js文件中修改route()函数：

```js
function route(handle, pathname) {
  console.log("About to route a request for " + pathname);
  if (typeof handle[pathname] === 'function') {
    handle[pathname]();
  } else {
    console.log("No request handler found for " + pathname);
  }
}

exports.route = route;
```

我们首先检查，给定路径 对应的请求处理程序 是否存在，如果存在的话直接调用相应的函数。我们可以用从关联数组中获取元素一样的方式从传递的对象中获取请求处理函数，因此就有了简洁流畅的形如`handle[pathname]();`的表达式，这个就像前面提到的那样：“嗨，请帮我处理了这个路径”。

有了这些，我们就把服务器、路由和请求处理程序结合在一起了。现在我们启动应用程序并在浏览器中访问<http://localhost:8888/start>，以下日志可以说明系统调用了正确的请求处理程序:

```sh
Server has started.
Request for /start received.
About to route a request for /start
Request handler 'start' was called.
```

并且在浏览器中打开<http://localhost:8888/>可以看到这个请求同样被start请求处理程序处理了：

```js
Request for / received.
About to route a request for /
Request handler 'start' was called.
```

### 4.11 让请求处理程序作出响应

很好。不过要是请求处理程序能够向浏览器返回一些有意义的信息而并非全是“Hello World”，那就更好了。

这里要记住的是，浏览器发出请求后获得并显示的“Hello World”信息仍是来自于我们server.js文件中的onRequest函数。

其实“处理请求”说白了就是“对请求作出响应”，因此，我们需要让请求处理程序能够像onRequest函数那样可以和浏览器进行“对话”

### 4.12 不好的实现方式

直截了当的实现方式是：让请求处理程序通过onRequest函数直接 return 返回他们要展示给用户的信息。

我们先这样去实现，然后再来看为什么这不是一种好的实现方式。

让我们从让请求处理程序返回信息开始。我们将requestHandler.js修改为：

```js
function start() {
  console.log("Request handler 'start' was called.");
  return "Hello Start";
}

function upload() {
  console.log("Request handler 'upload' was called.");
  return "Hello Upload";
}

exports.start = start;
exports.upload = upload;
```

同样，请求路由需要将请求处理程序返回给它的信息返回给服务器。因此，我们将router.js修改为：

```js
function route(handle, pathname) {
  console.log("About to route a request for " + pathname);
  if (typeof handle[pathname] === 'function') {
    return handle[pathname]();
  } else {
    console.log("No request handler found for " + pathname);
    return "404 Not found";
  }
}

exports.route = route;
```

正如上述代码所示，当请求无法路由的时候，我们返回相关的错误信息。

最后，我们需要对server.js进行重构，以使得它能够将请求处理程序通过请求路由返回的内容响应给浏览器，如下所示：

```js
var http = require("http");
var url = require("url");

function start(route, handle) {
  function onRequest(request, response) {
    var pathname = url.parse(request.url).pathname;
    console.log("Request for " + pathname + " received.");
    response.writeHead(200, {"Content-Type": "text/plain"});
    var content = route(handle, pathname)
    response.write(content);
    response.end();
  }

  http.createServer(onRequest).listen(8888);
  console.log("Server has started.");
}

exports.start = start;
```

运行重构后的应用，一切正常：

- 请求<http://localhost:8888/start> 浏览器会输出“Hello Start”
- 请求<http://localhost:8888/upload> 会输出“Hello Upload”
- 请求<http://localhost:8888/foo> 会输出“404 Not found”

那么问题在哪里呢？

简单的说就是：当请求处理程序需要进行非阻塞的操作的时候，我们的应用就“挂”了。下面就来详细解释下。

### 4.13 阻塞与非阻塞

我不想去解释“阻塞”和“非阻塞”的具体含义，我们直接来看，当在请求处理程序中加入阻塞操作时会发生什么。

这里，我们来修改下start请求处理程序，我们让它等待10秒以后再返回“Hello Start”。因为，JavaScript中没有类似sleep()这样的操作，所以这里只能来模拟实现。

让我们将requestHandlers.js修改成如下：

```js
function start() {
  console.log("Request handler 'start' was called.");

  function sleep(milliSeconds) {
    var startTime = new Date().getTime();
    while (new Date().getTime() < startTime + milliSeconds);
  }

  sleep(10000);
  return "Hello Start";
}

function upload() {
  console.log("Request handler 'upload' was called.");
  return "Hello Upload";
}

exports.start = start;
exports.upload = upload;
```

上述代码中，当函数start()被调用的时候，Node.js会先等待10秒，之后才会返回“Hello Start”。当调用upload()的时候，会和此前一样立即返回。

（当然了，这里只是模拟休眠10秒，实际场景中，这样的阻塞操作有很多，比方说一些长时间的计算操作等。）

接下来就让我们来看看，我们的改动带来了哪些变化。

当我们同时打开 <http://localhost:8888/start> 和 <http://localhost:8888/upload>时，注意，发生了什么： /start URL加载花了10秒，这和我们预期的一样。但是，/upload URL居然也花了10秒，而它在对应的请求处理程序中并没有类似于sleep()这样的操作！

这到底是为什么呢？原因就是start()包含了阻塞操作。形象的说就是“它阻塞了所有其他的处理工作”。

这显然是个问题，因为Node一向是这样来标榜自己的：“在node中除了代码，所有一切都是并行执行的”。

这句话的意思是说，Node.js可以在不增加其它线程的情况下，依然可以对任务进行并行处理 —— Node.js是单线程的。它通过事件轮询（event loop）来实现并行操作，对此，我们应该要充分利用这一点 —— 尽可能的避免阻塞操作，取而代之，多使用非阻塞操作。

然而，要用非阻塞操作，我们需要使用回调，通过将函数作为参数传递给其他需要花时间做处理的函数（比方说，休眠10秒，或者查询数据库，又或者是进行大量的计算）。

对于Node.js来说，它是这样处理的：“嘿，耗时操作Function()，你继续处理你的事情，我（Node.js线程）先不等你了，我继续去处理你后面的代码，请你提供一个callbackFunction()，等你处理完之后我会去调用该回调函数的，谢谢！”

### 4.14 错误的使用非阻塞操作

我们介绍一种错误的使用非阻塞操作的方式，将start请求处理程序修改成如下：

```js
var exec = require("child_process").exec;

function start() {
  console.log("Request handler 'start' was called.");
  var content = "empty";

  exec("ls -l", function (error, stdout, stderr) {
    content = stdout;
  });

  return content;
}

function upload() {
  console.log("Request handler 'upload' was called.");
  return "Hello Upload";
}

exports.start = start;
exports.upload = upload;
```

上述代码中，我们引入了`child_process`模块，为了实现一个既简单又实用的非阻塞操作：exec()。exec()让Node.js来执行一个shell命令，获取当前目录下所有的文件（“ls -l”）,然后，当/startURL请求的时候将文件信息输出到浏览器中。

我们启动服务器，访问<http://localhost:8888/start>，页面内容为“empty”。怎么回事？

虽然为了进行非阻塞操作，exec()使用了回调函数，但我们的主体代码是同步执行的，在调用exec()之后，Node.js会立即执行`return content`；这时，content仍然是“empty”，因为传递给exec()的回调函数还未执行到——因为exec()的操作是异步的。

那我们要如何才能实现将当前目录下的文件列表显示给用户呢？

### 4.15 以非阻塞操作进行请求响应

实现要点就是：函数传递。

之前，应用各种之间都是通过传递值的方式（请求处理程序 -> 请求路由 -> 服务器），将结果传递给HTTP服务器。

现在，我们采用传递response对象的方式：将服务器的回调函数onRequest()中的response对象，通过请求路由传递给请求处理程序。 随后，处理程序调用response的方法直接对请求作出响应。

让我们来一步步实现，先从server.js开始：

```js
var http = require("http");
var url = require("url");

function start(route, handle) {
  function onRequest(request, response) {
    var pathname = url.parse(request.url).pathname;
    console.log("Request for " + pathname + " received.");

    route(handle, pathname, response);
  }

  http.createServer(onRequest).listen(8888);
  console.log("Server has started.");
}

exports.start = start;
```

之前，我们从route()函数获取返回值，现在我们将response对象作为第三个参数传递给route()函数，并且，我们将所有response的函数调都移除，因为我们希望让route()函数来完成。

下面就来看看我们的router.js:

```js
function route(handle, pathname, response) {
  console.log("About to route a request for " + pathname);
  if (typeof handle[pathname] === 'function') {
    handle[pathname](response);
  } else {
    console.log("No request handler found for " + pathname);
    response.writeHead(404, {"Content-Type": "text/plain"});
    response.write("404 Not found");
    response.end();
  }
}

exports.route = route;
```

同样，相对之前从请求处理程序中获取返回值，这次的是直接传递response对象。

最后，我们将requestHandler.js修改为如下形式：

```js
var exec = require("child_process").exec;

function start(response) {
  console.log("Request handler 'start' was called.");

  exec("ls -lah", function (error, stdout, stderr) {
    response.writeHead(200, {"Content-Type": "text/plain"});
    response.write(stdout);
    response.end();
  });
}

function upload(response) {
  console.log("Request handler 'upload' was called.");
  response.writeHead(200, {"Content-Type": "text/plain"});
  response.write("Hello Upload");
  response.end();
}

exports.start = start;
exports.upload = upload;
```

为了对请求作出直接的响应，处理函数需要接收`response`参数。

start处理程序在exec()的匿名回调函数中做请求响应的操作，而upload处理程序仍然是简单的回复“Hello World”，只是这次是使用response对象而已。

再次我们启动应用（node index.js），一切正常。

如果想要证明/start处理程序中耗时的操作不会阻塞对/upload请求作出立即响应的话，可以将requestHandlers.js修改为如下形式：

```js
var exec = require("child_process").exec;

function start(response) {
  console.log("Request handler 'start' was called.");

  exec("find /",
    { timeout: 10000, maxBuffer: 20000*1024 },
    function (error, stdout, stderr) {
      response.writeHead(200, {"Content-Type": "text/plain"});
      response.write(stdout);
      response.end();
    });
}

function upload(response) {
  console.log("Request handler 'upload' was called.");
  response.writeHead(200, {"Content-Type": "text/plain"});
  response.write("Hello Upload");
  response.end();
}

exports.start = start;
exports.upload = upload;
```

这样，当请求<http://localhost:8888/start>时，10秒后才载入，而请求<http://localhost:8888/upload>会立即响应，虽然这时/start响应还在处理中。

## 5 更有用的场景

下面让我们给网站添加交互：用户选择一个文件，上传该文件，然后在浏览器中看到上传的文件。我们假设用户只会上传图片，然后我们应用将该图片显示到浏览器中。

要实现该功能，分为两步：首先，让我们来看看如何处理POST请求（非文件上传），之后，我们使用Node.js的一个用于文件上传的外部模块。之所以采用这种实现方式有两个理由。

- 第一，Node.js处理基础的POST请求虽然简单，但在这过程中能学到很多
- 第二，用Node.js来处理文件上传（multipart POST请求）是比较复杂的，它不在本书的范畴，但，如何使用外部模块却是在本书涉猎内容之内。

### 5.1 处理POST请求

考虑这样一个简单的例子：我们显示一个文本区（textarea）供用户输入内容，然后通过POST请求提交给服务器。最后，服务器接受到请求，通过处理程序将输入的内容展示到浏览器中。

/start生成带文本区的表单，我们将requestHandlers.js修改为如下形式：

```js
function start(response) {
  console.log("Request handler 'start' was called.");

  var body = '<html><head><meta http-equiv="Content-Type" content="text/html; '+
    'charset=UTF-8" />'+
    '</head><body>'+
    '<form action="/upload" method="post">'+
    '<textarea name="text" rows="20" cols="60"></textarea>'+
    '<input type="submit" value="Submit text" />'+
    '</form>'+
    '</body></html>';

    response.writeHead(200, {"Content-Type": "text/html"});
    response.write(body);
    response.end();
}

function upload(response) {
  console.log("Request handler 'upload' was called.");
  response.writeHead(200, {"Content-Type": "text/plain"});
  response.write("Hello Upload");
  response.end();
}

exports.start = start;
exports.upload = upload;
```

好了，现在浏览器中访问<http://localhost:8888/start>就可以看到简单的表单了，记得重启服务器哦！

你可能会说：这种直接将视觉元素放在请求处理程序中的方式太丑陋了。说的没错，但是，我并不想在本书中介绍诸如MVC之类的模式，因为这对于你了解JavaScript或者Node.js环境来说没多大关系。

我们来探讨一个更有趣的问题：当用户提交表单时，触发/upload处理POST请求的问题。

现在，我们已经是新手中的专家了，很自然会想到采用异步回调来实现非阻塞地处理POST请求的数据。

这里采用非阻塞方式处理是明智的，因为POST请求一般都比较“重” —— 用户可能会输入大量的内容。用阻塞的方式处理大数据量的请求必然会导致用户操作的阻塞。

为了使整个过程非阻塞，Node.js会将POST数据拆分成很多小的数据块，然后通过触发特定的事件，将这些小数据块传递给回调函数。这里的特定的事件有data事件（表示新的小数据块到达了）以及end事件（表示所有的数据都已经接收完毕）。

我们需要告诉Node.js当这些事件触发的时候，回调哪些函数。怎么告诉呢？ 我们通过在request对象上注册监听器（listener） 来实现。这里的request对象是每次接收到HTTP请求时候，都会把该对象传递给onRequest回调函数。

如下所示：

```js
request.addListener("data", function(chunk) {
  // called when a new chunk of data was received
});

request.addListener("end", function() {
  // called when all chunks of data have been received
});
```

问题来了，这部分逻辑写在哪里呢？ 我们现在只是在服务器中获取到了request对象 —— 我们并没有像之前response对象那样，把 request 对象传递给请求路由和请求处理程序。

在我看来，获取来自请求的数据，然后将这些数据给应用层处理，应该是HTTP服务器要做的事情。因此，我建议，我们直接在服务器中处理POST数据，然后将最终的数据传递给请求路由和请求处理器，让他们来进行进一步的处理。

因此，实现思路就是： 将data和end事件的回调函数直接放在服务器中，在data事件回调中收集所有的POST数据，当接收到所有数据，触发end事件后，其回调函数调用请求路由，并将数据传递给它，然后，请求路由再将该数据传递给请求处理程序。

马上来实现，先从server.js开始：

```js
var http = require("http");
var url = require("url");

function start(route, handle) {
  function onRequest(request, response) {
    var postData = "";
    var pathname = url.parse(request.url).pathname;
    console.log("Request for " + pathname + " received.");

    request.setEncoding("utf8");

    request.addListener("data", function(postDataChunk) {
      postData += postDataChunk;
      console.log("Received POST data chunk '"+
      postDataChunk + "'.");
    });

    request.addListener("end", function() {
      route(handle, pathname, response, postData);
    });

  }

  http.createServer(onRequest).listen(8888);
  console.log("Server has started.");
}

exports.start = start;
```

上述代码做了三件事情：首先，我们设置了接收数据的编码格式为UTF-8，然后注册了“data”事件的监听器，用于收集每次接收到的新数据块，并将其赋值给postData变量，最后，我们将请求路由的调用移到end事件处理程序中，以确保它只会当所有数据接收完毕后才触发，并且只触发一次。我们同时还把POST数据传递给请求路由，因为这些数据，请求处理程序会用到。

上述代码在每个数据块到达的时候输出了日志，这对于最终生产环境来说，是很不好的（数据量可能会很大），但是，在开发阶段是很有用的，有助于让我们看到发生了什么。

我建议可以尝试下，尝试着去输入一小段文本，以及大段内容，当大段内容的时候，就会发现data事件会触发多次。

再来点酷的。我们接下来在/upload页面，展示用户输入的内容。要实现该功能，我们需要将postData传递给请求处理程序，修改router.js为如下形式：

```js
function route(handle, pathname, response, postData) {
  console.log("About to route a request for " + pathname);
  if (typeof handle[pathname] === 'function') {
    handle[pathname](response, postData);
  } else {
    console.log("No request handler found for " + pathname);
    response.writeHead(404, {"Content-Type": "text/plain"});
    response.write("404 Not found");
    response.end();
  }
}

exports.route = route;
```

然后，在requestHandlers.js中，我们将数据包含在对upload请求的响应中：

```js
function start(response, postData) {
  console.log("Request handler 'start' was called.");

  var body = '<html>'+
    '<head>'+
    '<meta http-equiv="Content-Type" content="text/html; '+
    'charset=UTF-8" />'+
    '</head>'+
    '<body>'+
    '<form action="/upload" method="post">'+
    '<textarea name="text" rows="20" cols="60"></textarea>'+
    '<input type="submit" value="Submit text" />'+
    '</form>'+
    '</body>'+
    '</html>';

    response.writeHead(200, {"Content-Type": "text/html"});
    response.write(body);
    response.end();
}

function upload(response, postData) {
  console.log("Request handler 'upload' was called.");
  response.writeHead(200, {"Content-Type": "text/plain"});
  response.write("You've sent: " + postData);
  response.end();
}

exports.start = start;
exports.upload = upload;
```

好了，我们现在可以接收POST数据并在请求处理程序中处理该数据了。

我们最后要做的是：当前我们是把请求的整个消息体传递给了请求路由和请求处理程序。我们应该只把POST数据中，我们感兴趣的部分传递给请求路由和请求处理程序。在我们这个例子中，我们感兴趣的其实只是text字段。

我们可以使用此前介绍过的querystring模块来实现：

```js
var querystring = require("querystring");

function start(response, postData) {
  console.log("Request handler 'start' was called.");

  var body = '<html>'+
    '<head>'+
    '<meta http-equiv="Content-Type" content="text/html; '+
    'charset=UTF-8" />'+
    '</head>'+
    '<body>'+
    '<form action="/upload" method="post">'+
    '<textarea name="text" rows="20" cols="60"></textarea>'+
    '<input type="submit" value="Submit text" />'+
    '</form>'+
    '</body>'+
    '</html>';

    response.writeHead(200, {"Content-Type": "text/html"});
    response.write(body);
    response.end();
}

function upload(response, postData) {
  console.log("Request handler 'upload' was called.");
  response.writeHead(200, {"Content-Type": "text/plain"});
  response.write("You've sent the text: "+
  querystring.parse(postData).text);
  response.end();
}

exports.start = start;
exports.upload = upload;
```

好了，以上就是关于处理POST数据的全部内容。

### 5.2 处理文件上传

最后，我们来实现我们最终的目标：允许用户上传图片，并将该图片在浏览器中显示出来。我们通过它能学到如何安装和使用外部Node.js模块。

这里我们要用到的外部模块是node-formidable模块。它对解析上传的文件数据做了很好的抽象。其实说白了，处理文件上传“就是”处理POST数据 —— 但是，麻烦的是在具体的处理细节，所以，这里采用现成的方案更合适点。

使用该模块，首先需要安装该模块。Node.js有它自己的包管理器，叫NPM。它可以让安装Node.js的外部模块变得非常方便。通过如下一条命令就可以完成该模块的安装：

```js
npm install formidable
```

现在我们就可以用formidable模块了——使用外部模块与内部模块类似，用require语句将其引入即可

```js
var formidable = require("formidable");
```

这里该模块做的就是将通过HTTP POST请求提交的表单，在Node.js中可以被解析。我们要做的就是创建一个新的IncomingForm，它是对提交表单的抽象表示，之后，就可以用它解析request对象，获取表单中需要的数据字段。

node-formidable官方的例子展示了这两部分是如何融合在一起工作的：

```js
var formidable = require('formidable'),
    http = require('http'),
    util = require('util');

http.createServer(function(req, res) {
  if (req.url == '/upload' && req.method.toLowerCase() == 'post') {
    // parse a file upload
    var form = new formidable.IncomingForm();
    form.parse(req, function(err, fields, files) {
      res.writeHead(200, {'content-type': 'text/plain'});
      res.write('received upload:\n\n');
      res.end(util.inspect({fields: fields, files: files}));
    });
    return;
  }

  // show a file upload form
  res.writeHead(200, {'content-type': 'text/html'});
  res.end(
    '<form action="/upload" enctype="multipart/form-data" '+
    'method="post">'+
    '<input type="text" name="title"><br>'+
    '<input type="file" name="upload" multiple="multiple"><br>'+
    '<input type="submit" value="Upload">'+
    '</form>'
  );
}).listen(8888);
```

如果我们将上述代码，保存到一个文件中，并通过node来执行，就可以进行简单的表单提交了，包括文件上传。然后，可以看到通过调用form.parse传递给回调函数的files对象的内容，如下所示：

```js
received upload:

{ fields: { title: 'Hello World' },
  files:
   { upload:
      { size: 1558,
        path: '/tmp/1c747974a27a6292743669e91f29350b',
        name: 'us-flag.png',
        type: 'image/png',
        lastModifiedDate: Tue, 21 Jun 2011 07:02:41 GMT,
        _writeStream: [Object],
        length: [Getter],
        filename: [Getter],
        mime: [Getter] } } }
```

为了实现我们的功能，我们需要将上述代码应用到我们的应用中，另外，我们还要考虑如何将上传文件的内容（保存在/tmp目录中）显示到浏览器中。

我们先来解决后面那个问题：对于保存在本地硬盘中的文件，如何才能在浏览器中看到呢？

显然，我们需要将该文件读取到我们的服务器中，使用一个叫fs的模块。

我们来添加/showURL的请求处理程序，该处理程序直接硬编码将文件/tmp/test.png内容展示到浏览器中。当然了，首先需要将该图片保存到这个位置才行。

将requestHandlers.js修改为如下形式：

```js
var querystring = require("querystring"),
    fs = require("fs");

function start(response, postData) {
  console.log("Request handler 'start' was called.");

  var body = '<html>'+
    '<head>'+
    '<meta http-equiv="Content-Type" '+
    'content="text/html; charset=UTF-8" />'+
    '</head>'+
    '<body>'+
    '<form action="/upload" method="post">'+
    '<textarea name="text" rows="20" cols="60"></textarea>'+
    '<input type="submit" value="Submit text" />'+
    '</form>'+
    '</body>'+
    '</html>';

    response.writeHead(200, {"Content-Type": "text/html"});
    response.write(body);
    response.end();
}

function upload(response, postData) {
  console.log("Request handler 'upload' was called.");
  response.writeHead(200, {"Content-Type": "text/plain"});
  response.write("You've sent the text: "+
  querystring.parse(postData).text);
  response.end();
}

function show(response, postData) {
  console.log("Request handler 'show' was called.");
  fs.readFile("/tmp/test.png", "binary", function(error, file) {
    if(error) {
      response.writeHead(500, {"Content-Type": "text/plain"});
      response.write(error + "\n");
      response.end();
    } else {
      response.writeHead(200, {"Content-Type": "image/png"});
      response.write(file, "binary");
      response.end();
    }
  });
}

exports.start = start;
exports.upload = upload;
exports.show = show;
```

我们还需要将这新的请求处理程序，添加到index.js中的路由映射表中：

```js
var server = require("./server");
var router = require("./router");
var requestHandlers = require("./requestHandlers");

var handle = {}
handle["/"] = requestHandlers.start;
handle["/start"] = requestHandlers.start;
handle["/upload"] = requestHandlers.upload;
handle["/show"] = requestHandlers.show;

server.start(router.route, handle);
```

重启服务器之后，通过访问<http://localhost:8888/show>，就可以看到保存在/tmp/test.png的图片了。

好，最后我们要的就是：

- 在/start表单中添加一个文件上传元素
- 将node-formidable整合到我们的upload请求处理程序中，用于将上传的图片保存到/tmp/test.png
- 将上传的图片内嵌到/uploadURL输出的HTML中

第一项很简单。只需要在HTML表单中，添加一个multipart/form-data的编码类型，移除此前的文本区，添加一个文件上传组件，并将提交按钮的文案改为“Upload file”即可。 如下requestHandler.js所示：

```js
var querystring = require("querystring"),
    fs = require("fs");

function start(response, postData) {
  console.log("Request handler 'start' was called.");

  var body = '<html>'+
    '<head>'+
    '<meta http-equiv="Content-Type" '+
    'content="text/html; charset=UTF-8" />'+
    '</head>'+
    '<body>'+
    '<form action="/upload" enctype="multipart/form-data" '+
    'method="post">'+
    '<input type="file" name="upload">'+
    '<input type="submit" value="Upload file" />'+
    '</form>'+
    '</body>'+
    '</html>';

    response.writeHead(200, {"Content-Type": "text/html"});
    response.write(body);
    response.end();
}

function upload(response, postData) {
  console.log("Request handler 'upload' was called.");
  response.writeHead(200, {"Content-Type": "text/plain"});
  response.write("You've sent the text: "+
  querystring.parse(postData).text);
  response.end();
}

function show(response, postData) {
  console.log("Request handler 'show' was called.");
  fs.readFile("/tmp/test.png", "binary", function(error, file) {
    if(error) {
      response.writeHead(500, {"Content-Type": "text/plain"});
      response.write(error + "\n");
      response.end();
    } else {
      response.writeHead(200, {"Content-Type": "image/png"});
      response.write(file, "binary");
      response.end();
    }
  });
}

exports.start = start;
exports.upload = upload;
exports.show = show;
```

很好。下一步相对比较复杂。这里有这样一个问题： 我们需要在upload处理程序中对上传的文件进行处理，这样的话，我们就需要将request对象传递给node-formidable的form.parse函数。

但是，我们有的只是response对象和postData数组。看样子，我们只能不得不将request对象从服务器开始一路通过请求路由，再传递给请求处理程序。 或许还有更好的方案，但是，不管怎么说，目前这样做可以满足我们的需求。

到这里，我们可以将postData从服务器以及请求处理程序中移除了 —— 一方面，对于我们处理文件上传来说已经不需要了，另外一方面，它甚至可能会引发这样一个问题： 我们已经“消耗”了request对象中的数据，这意味着，对于form.parse来说，当它想要获取数据的时候就什么也获取不到了。（因为Node.js不会对数据做缓存）

我们从server.js开始 —— 移除对postData的处理以及request.setEncoding （这部分node-formidable自身会处理），转而采用将request对象传递给请求路由的方式：

```js
var http = require("http");
var url = require("url");

function start(route, handle) {
  function onRequest(request, response) {
    var pathname = url.parse(request.url).pathname;
    console.log("Request for " + pathname + " received.");
    route(handle, pathname, response, request);
  }

  http.createServer(onRequest).listen(8888);
  console.log("Server has started.");
}

exports.start = start;
```

接下来是 router.js —— 我们不再需要传递postData了，这次要传递request对象：

```js
function route(handle, pathname, response, request) {
  console.log("About to route a request for " + pathname);
  if (typeof handle[pathname] === 'function') {
    handle[pathname](response, request);
  } else {
    console.log("No request handler found for " + pathname);
    response.writeHead(404, {"Content-Type": "text/html"});
    response.write("404 Not found");
    response.end();
  }
}

exports.route = route;
```

现在，request对象就可以在我们的upload请求处理程序中使用了。node-formidable会处理将上传的文件保存到本地/tmp目录中，而我们需要做的是确保该文件保存成/tmp/test.png。没错，我们保持简单，并假设只允许上传PNG图片。

这里采用fs.renameSync(path1,path2)来实现。要注意的是，正如其名，该方法是同步执行的，也就是说，如果该重命名的操作很耗时的话会阻塞。这块我们先不考虑。

接下来，我们把处理文件上传以及重命名的操作放到一起，如下requestHandlers.js所示：

```js
var querystring = require("querystring"),
    fs = require("fs"),
    formidable = require("formidable");

function start(response) {
  console.log("Request handler 'start' was called.");

  var body = '<html>'+
    '<head>'+
    '<meta http-equiv="Content-Type" content="text/html; '+
    'charset=UTF-8" />'+
    '</head>'+
    '<body>'+
    '<form action="/upload" enctype="multipart/form-data" '+
    'method="post">'+
    '<input type="file" name="upload" multiple="multiple">'+
    '<input type="submit" value="Upload file" />'+
    '</form>'+
    '</body>'+
    '</html>';

    response.writeHead(200, {"Content-Type": "text/html"});
    response.write(body);
    response.end();
}

function upload(response, request) {
  console.log("Request handler 'upload' was called.");

  var form = new formidable.IncomingForm();
  console.log("about to parse");
  form.parse(request, function(error, fields, files) {
    console.log("parsing done");
    fs.renameSync(files.upload.path, "/tmp/test.png");
    response.writeHead(200, {"Content-Type": "text/html"});
    response.write("received image:<br/>");
    response.write("<img src='/show' />");
    response.end();
  });
}

function show(response) {
  console.log("Request handler 'show' was called.");
  fs.readFile("/tmp/test.png", "binary", function(error, file) {
    if(error) {
      response.writeHead(500, {"Content-Type": "text/plain"});
      response.write(error + "\n");
      response.end();
    } else {
      response.writeHead(200, {"Content-Type": "image/png"});
      response.write(file, "binary");
      response.end();
    }
  });
}

exports.start = start;
exports.upload = upload;
exports.show = show;
```

好了，重启服务器，我们应用所有的功能就可以用了。选择一张本地图片，将其上传到服务器，然后浏览器就会显示该图片。

## 6 总结与展望

恭喜，我们的任务已经完成了！我们开发完了一个Node.js的web应用，应用虽小，但却“五脏俱全”。 期间，我们介绍了很多技术点：服务端JavaScript、函数式编程、阻塞与非阻塞、回调、事件、内部和外部模块等等。

当然了，还有许多本书没有介绍到的：如何操作数据库、如何进行单元测试、如何开发Node.js的外部模块以及一些简单的诸如如何获取GET请求之类的方法。

但本书毕竟只是一本给初学者的教程 —— 不可能覆盖到所有的内容。

幸运的是，Node.js社区非常活跃，这意味着，有许多关于Node.js的资源，有什么问题都可以向社区寻求解答。