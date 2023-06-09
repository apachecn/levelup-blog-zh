# 用 Pistache 在 C++中构建 API

> 原文：<https://levelup.gitconnected.com/building-an-api-in-c-with-pistache-413247535fd3>

![](img/8ca576ef27435878f396b6c6ac853294.png)

Theo Crazzolara 在 [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral) 上的照片

根据 RapidAPI 的博客文章[的说法，用于构建 API 的最流行的语言/框架是 PHP、NodeJS 和 Python(相当多)。像 C++这样的语言并不经常用于这种目的，因为这超出了它们的范围。当我构建一个 web 前端来运行我之前构建的 C++模拟时，我自己就经历过这种情况，这是一个车轮交易算法的重新实现。在这种情况下，我使用 NodeJS 构建一个 API，可以从 web 前端调用该 API，然后 web 前端使用一个库通过终端调用来执行 C++代码。这是非常低效的，并且比用 C++处理所有事情更容易出错。正因为如此，我决定找出用 C++服务 API 端点需要什么，并发现](https://rapidapi.com/blog/programming-languages/)[pische . io](http://pistache.io/)是一种非常简单有效的方法。在这篇文章中，我将演示如何在 C++中建立一个 API，方法是用 Pistache 构造一个非常基本的 GET 请求和一个非常基本的 post 请求。

在我们开始之前，我将提到几个用例，因为如果你计划构建一个基于 web 的应用程序，最好坚持使用现代 web 技术(NodeJS、PHP、Python 等)。)为 API。我认为使用 C++/pische 的两个主要原因是:I)您已经有一个希望通过 web 前端运行的 C++应用程序，ii)您有一个希望通过 Docker 或其他容器化形式与其他应用程序混合的 c++应用程序。无论哪种情况，建立易于访问的 API 端点可能是最好的解决方案。

# 皮斯托切

根据他们的网站，pische ch 是“一个优雅的 C++ REST 框架”。该框架非常易于使用，提供了许多功能，包括多线程 HTTP 服务器、轻松向 C++函数发送请求的 HTTP 路由器以及请求 API 的异步 HTTP 客户端。这个库很容易安装在大多数系统上(我在我的服务器上运行的是[Debian 10](https://medium.com/swlh/building-an-affordable-home-server-with-old-server-hardware-600-4670f685ad45)和其他基于 Debian 的系统】,因为它有一个官方的 PPA。安装说明可以在他们的[快速入门指南](http://pistache.io/docs/)中找到。

尽管我发现这个框架很容易使用，但要开始使用还是需要一点努力。项目的文档很好，但是还有一些需要改进的地方。我发现阅读 GitHub 上示例的[代码非常有帮助，并为这篇简短的帖子提供了大部分见解，特别是](https://github.com/pistacheio/pistache/tree/master/examples) [*rest_server.cc* 示例](https://github.com/pistacheio/pistache/blob/master/examples/rest_server.cc)。安装 Pistache 后，可以通过 *-lpistache* 标志*将库包含在 *g++* 中。下面是一个基本的 Makefile，用名为 *main.cpp* 的文件中的代码为服务器构建可执行文件。*

这个 Makefile 说明了 Pistache 的一个潜在缺点，即需要 C++17。我认为在大多数情况下，这不应该是一个问题，因为该标准现在已经有 5 年的历史了，但它可能会成为你的一个障碍。

# 设置

安装并包含 Pistache 之后，需要在 C++项目中包含一些头文件来使用这个框架。

我还使用了 [RapidJSON](https://rapidjson.org/) 来解析 POST 请求的请求体，因此也需要包含它。[我之前写过关于在 C++中使用 RapidJSON 库处理 JSON 的文章](/parsing-json-in-c-with-rapidjson-6d6d3e505e12)，任何感兴趣的读者都应该看看这篇文章。

接下来，为了让事情变得简单一点，我们将使用 *Pistache* 名称空间。

最后，我们需要在用于运行服务器的主函数中定义一些变量。我没有详细描述它们，而是在代码中添加了一些解释性注释。

# 获取请求

## 没有参数

首先，我们将定义一个非常基本的 get 请求端点，它不接受任何参数并发回一些响应。我能想到的最简单的办法就是回应“世界！”在“你好”端点。回调函数看起来像这样

相当简单！注意，用 Pistache 构建的 REST API 的所有回调都有相同的签名，但函数名不同。现在，我们将此路由添加到路由器中。

上面，我已经将路由“/hello”添加到先前定义的路由器中。我在这里包含了整个 main 函数，以展示这一切是如何适应的，但是接下来我将包含更少的代码，以强调实际正在进行的更改(这样它们就不会在周围的代码中丢失)。现在通过上面的 Makefile 和*编译并运行它。/server* (如果使用 Linux 系统并像我一样制作)应该在

> http://本地主机:9900/hello

在 web 浏览器中导航到此 URL(或通过其他方式提交 GET 请求，例如通过邮递员)将返回以下响应

> 世界！

没有比这更简单的了。

## 带(可选)参数

接下来，我们将看看如何发出 GET 请求，但现在使用 URL 参数。GET 请求中的参数通过 URL 传递。在 Pistache 中，它们可以标记为可选或必需。为了进行演示，创建了一个端点，它接受一个(可选的)参数，并将其回显给用户，这个端点被称为“/echo_get”，参数被命名为“text”使端点“/echo_get/:text？”。请注意“？”参数名后面的(":text ")表示该参数是可选的。如果删除了该参数，则该参数必须是 URL 的一部分，否则将会出现错误，提示路由不存在。下面是“/echo_get”的回调

这条新路由需要添加到路由器中

提交此请求有两种方式，即带参数和不带参数。后者看起来像这样(确保您的服务器正在运行)

> [http://localhost:9900/echo _ get](http://localhost:9900/echo_get)

它返回响应

> 未提供参数。

不出所料。前者(带有参数)可能如下所示

> [http://localhost:9900/echo _ get/hello！](http://localhost:9900/echo_get/hello!)

它回显文本

> 你好！

多个参数可以以类似和直观的方式处理。

# 发布请求

如果您已经使用浏览器提交 GET 请求，那么转到 POST 请求将需要不同的方法。这是由于在请求中处理参数的方式使得处理敏感数据更加安全和理想。我使用 Postman 来测试我的端点，但是您可以使用任何其他允许您提交请求的软件(使用 *requests* 库在 Python 中测试端点也非常容易)。

开始回调的定义

这个回调将检查一个“文本”参数，如果它是可用的，就将它回显给用户。如果它不可用，将会有一条消息来说明这一点。注意这里我们使用 RapidJSON 来处理请求体(JSON 格式)，[我还有一篇关于使用这个 C++库来处理 JSON](/parsing-json-in-c-with-rapidjson-6d6d3e505e12) 的文章，如果你是这种处理的新手，这可能会有帮助。(对于那些想知道我为什么使用 RapidJSON 而不是 JsonCpp 的人，我在 2021 年初的一些合同工作中使用了两者，当解析大约 10 年的 OHLC 数据时，JsonCpp 用了大约 20 分钟，而 RapidJSON 只用了几秒钟，也就是说，两者各有利弊。)

现在需要将该路由添加到路由器中

随着服务器的运行，请求可以提交到 URL

> [http://localhost:9900/echo](http://localhost:9900/echo)

发送到服务器的 JSON 中有或没有“text”参数。下面是 Postman 的截图，展示了参数是如何提供的

![](img/e81d5e33102382e27e0d7b4efbdb73a7.png)

注意，我在我的服务器上提供这个 API，它的网络名称是 *navier，*如果在你的本地机器上运行，请求应该使用 *localhost* 而不是 *navier* 。

发送此请求将返回如下响应，如预期的那样，

> 你好世界！

同样，这个逻辑可以扩展到处理多个参数。我在这里的目标是展示实现自己的 API 时(或多或少)需要的大部分功能。

# 结论

在这篇文章中，我讨论了如何设置一些基本的 API 端点，并通过 Pistache 框架在 C++中为它们提供服务。该框架易于使用，许多 C++程序员应该通过使他们的应用程序更容易被观众访问的方式打开许多大门。下面是这个 API 的完整代码，你可以随意使用和修改。

# 完整代码