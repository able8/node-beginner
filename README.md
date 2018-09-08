# node-beginner

Node.js Web 开发入门

> Node.js tutorial for beginners <https://www.nodebeginner.org>
>
> 作者： [Manuel Kiessling](https://github.com/manuelkiessling/nodebeginner.org) 翻译： goddyzhao & GrayZhang & MondayChen

---

- [Node 入门](#node-beginner)
    - [1 绪论](#1-%E7%BB%AA%E8%AE%BA)
        - [1.1 读者对象](#11-%E8%AF%BB%E8%80%85%E5%AF%B9%E8%B1%A1)
        - [1.2 本书结构](#12-%E6%9C%AC%E4%B9%A6%E7%BB%93%E6%9E%84)
    - [2 JavaScript与Node.js](#2-javascript%E4%B8%8Enodejs)
        - [2.1 介绍](#21-%E4%BB%8B%E7%BB%8D)
        - [2.2 “Hello World”](#22-hello-world)

---

## 1 绪论

本书是一本“从初级入门到高级入门”的书，将教你如何用Node.js来开发Web应用，和所需的JavaScript知识。

### 1.1 读者对象

至少对一门诸如Python、Ruby、PHP或者Java这样面向对象的语言有一定的经验；对JavaScript处于初学阶段，并且完全是一个Node.js的新手。

本书不会对诸如数据类型、变量、控制结构等等之类非常基础的概念作介绍。

本书还是会对JavaScript中的函数和对象作详细介绍，因为它们与其他同类编程语言中的函数和对象有很大的不同。

### 1.2 本书结构

读完本书之后，你将完成一个完整的web应用，该应用允许用户浏览页面以及上传文件。

相比为了实现该功能书写的代码本身，我们更关注的是如何创建一个框架来对我们应用的不同模块进行干净地剥离。

本书先从介绍在Node.js环境中进行JavaScript开发和在浏览器环境中进行JavaScript开发的差异开始。

紧接着，会带领大家完成一个最传统的“Hello World”应用，这也是最基础的Node.js应用。

最后，会和大家讨论如何设计一个“真正”完整的应用，剖析要完成该应用需要实现的不同模块，并一步一步介绍如何来实现这些模块。

过程中，大家会学到JavaScript中一些高级的概念、如何使用它们以及为什么使用这些概念就可以实现而其他编程语言中同类的概念就无法实现。

该应用所有的源代码都可以通过 [本书Github代码仓库](https://github.com/manuelkiessling/nodebeginner.org/tree/master/code/application)。

## 2 JavaScript与Node.js

### 2.1 介绍

JavaScript最早是运行在浏览器中，为web页面添加交互，属于前端技术。

后来，Node.js出现，它允许在后端（脱离浏览器环境）运行JavaScript代码。

要实现在后台运行JavaScript代码，就需要解释器来被解释和执行代码。Node.js使用了Google的V8虚拟机（Google的Chrome浏览器使用的JavaScript执行环境），来解释和执行JavaScript代码。

Node.js生态系统包括众多第三方模块，大大简化开发过程。

要使用Node.js,首先需要进行安装。关于如何安装Node.js，可以直接参考官方的[安装指南](https://nodejs.org/zh-cn/)。

### 2.2 “Hello World”

马上开始我们第一个Node.js应用：“Hello World”。

打开你最喜欢的编辑器，创建一个helloworld.js文件。我们要做就是向STDOUT输出“Hello World”，如下是实现该功能的代码：

```js
console.log('Hello World');
```

保存该文件，并通过Node.js来执行：

```js
node helloworld.js
```

正常的话，就会在终端输出Hello World 。

好吧，我承认这个应用是有点无趣，那么下面我们就来点“干货”。

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

听起来好像有一大堆活要做，但对Node.js来说这并不是什么麻烦的事。

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

搞定！你刚刚完成了一个可以工作的HTTP服务器。为了证明这一点，我们来运行并且测试这段代码。首先，用Node.js执行你的脚本：

```js
node server.js
```

接下来，打开浏览器访问<http://localhost:8888/>，你会看到一个写着“Hello World”的网页。

这很有趣，不是吗？让我们先来谈谈HTTP服务器的问题。

### 4.2 分析HTTP服务器

让我们分析一下这个HTTP服务器的构成。

第一行请求（require）Node.js自带的 http 模块，并且把它赋值给 http 变量。

接下来我们调用http模块提供的函数： createServer 。这个函数会返回一个对象，这个对象有一个叫做 listen 的方法，这个方法有一个数值参数，指定这个HTTP服务器监听的端口号。

咱们暂时先不管 http.createServer 的括号里的那个函数定义。

我们本来可以用这样的代码来启动服务器并侦听8888端口：

```js
var http = require("http");

var server = http.createServer();
server.listen(8888);
```

这段代码只会启动一个侦听8888端口的服务器，它不做任何别的事情，甚至连请求都不会应答。

最有趣的部分是 createServer() 的第一个参数，一个函数定义。

实际上，这个函数定义是 createServer() 的第一个也是唯一一个参数。因为在JavaScript中，函数和其他变量一样都是可以被传递的。

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

请仔细阅读这段代码！在这里，我们把 say 函数作为execute函数的第一个变量进行了传递。这里传递的不是 say 的返回值，而是 say 本身！

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

用这种方式，我们甚至不用给这个函数起名字，这也是为什么它被叫做 匿名函数 。

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

这就是Node.js/JavaScript的事件驱动设计能够真正帮上忙的地方了。

我们创建了服务器，并向创建它的方法传递了一个函数。无论何时我们的服务器收到一个请求，这个函数就会被调用。

我们不知道这件事情什么时候会发生，但是我们现在有了一个处理请求的地方：它就是我们传递过去的那个函数。至于它是被预先定义的函数还是匿名函数，就无关紧要了。

这个就是传说中的 回调 。我们给某个方法传递了一个函数，这个方法在有相应事件发生时调用这个函数来进行 回调 。

让我们再来琢磨琢磨这个新概念。我们怎么证明，在创建完服务器之后，即使没有HTTP请求进来、我们的回调函数也没有被调用的情况下，我们的代码还继续有效呢？我们试试这个：

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

> 注意：在 onRequest（我们的回调函数）触发的地方，我用 console.log 输出了一段文本。在HTTP服务器开始工作之后，也输出一段文本。

运行node server.js时，命令行上输出“Server has started.”。当我们向服务器发出请求（在浏览器访问<http://localhost:8888/ >），“Request received.”这条消息就会在命令行中出现。

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

怎么组织代码，我们应该把所有东西都放进一个文件里吗？

实际上，为了便于维护，保持代码的可读性，我们把不同功能的代码放入不同的模块中，保持代码分离。

这种方法允许你拥有一个干净的主文件（main file），你可以用Node.js执行它；同时你可以拥有干净的模块，它们可以被主文件和其他的模块调用。

通常我们会有一个叫 index.js 的文件去调用应用的其他模块（比如 server.js 中的HTTP服务器模块）来引导和启动应用。

我们现在就来谈谈怎么把server.js变成一个真正的Node.js模块，使它可以被我们（还没动工）的 index.js 主文件使用。

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

我们把我们的服务器脚本放到一个叫做 start 的函数里，然后我们会导出这个函数。


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

我们可以像使用任何其他的内置模块一样使用server模块：请求这个文件并把它指向一个变量，其中已导出的函数就可以被我们使用了。

好了。我们现在就可以从我们的主要脚本启动我们的的应用了，而它还是老样子：

```js
node index.js
```

我们现在可以把我们的应用的不同部分放入不同的文件里，并且通过生成模块的方式把它们连接到一起了。

我们仍然只拥有整个应用的最初部分：我们可以接收HTTP请求。但是我们得做点什么——对于不同的URL请求，服务器应该有不同的反应。

对于一个非常简单的应用来说，你可以直接在回调函数 onRequest() 中做这件事情。不过就像我说过的，我们应该加入一些抽象的元素，让我们的例子变得更有趣一点儿。

处理不同的HTTP请求在我们的代码中是一个不同的部分，叫做“路由选择”——那么，我们接下来就创造一个叫做 路由 的模块吧。

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

J在JavaScript中，对象就是一个键/值对的集合 -- 你可以把JavaScript的对象想象成一个键为字符串类型的字典。avaScript的对象的值可以是字符串、数字或者……函数！

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

通过以上代码，我们首先检查给定的路径对应的请求处理程序是否存在，如果存在的话直接调用相应的函数。我们可以用从关联数组中获取元素一样的方式从传递的对象中获取请求处理函数，因此就有了简洁流畅的形如handle[pathname]();的表达式，这个感觉就像在前方中提到的那样：“嗨，请帮我处理了这个路径”。

有了这些，我们就把服务器、路由和请求处理程序在一起了。现在我们启动应用程序并在浏览器中访问http://localhost:8888/start，以下日志可以说明系统调用了正确的请求处理程序

Server has started.
Request for /start received.
About to route a request for /start
Request handler 'start' was called.
并且在浏览器中打开http://localhost:8888/可以看到这个请求同样被start请求处理程序处理了：

Request for / received.
About to route a request for /
Request handler 'start' was called.


### 4.11 让请求处理程序作出响应

很好。不过现在要是请求处理程序能够向浏览器返回一些有意义的信息而并非全是“Hello World”，那就更好了。

这里要记住的是，浏览器发出请求后获得并显示的“Hello World”信息仍是来自于我们server.js文件中的onRequest函数。

其实“处理请求”说白了就是“对请求作出响应”，因此，我们需要让请求处理程序能够像onRequest函数那样可以和浏览器进行“对话”

## 5 更有用的场景

处理POST请求
处理文件上传


## 6 总结与展望
