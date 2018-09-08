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

## 5 更有用的场景

## 6 总结与展望
