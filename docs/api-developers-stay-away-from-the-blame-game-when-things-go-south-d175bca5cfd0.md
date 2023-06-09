# API 开发者，当事情变糟时，远离指责游戏

> 原文：<https://levelup.gitconnected.com/api-developers-stay-away-from-the-blame-game-when-things-go-south-d175bca5cfd0>

## 设计 API 时的一些好的实践

当事情不像预期的那样运行时，正确地记录日志以保持冷静和自信

![](img/eef93b9b51ef840d488d94ea86a64fdf.png)

API 开发者和服务所有者，我们都遇到过这种情况。为了让我们的消费者满意，我们在开发时将血汗投入到代码中。

但是，当事情不奏效时，人们会感到害怕，并开始相互指责。如果我们能在发展我们的服务时采取一些措施，我们就能轻松地通过这些指责游戏，并能放松下来。

当错误已经发生时，日志记录是调试中非常重要的一个方面。

今天在这篇文章中，我将讨论一些记录日志的方法，特别是为了保持不被追究而记录什么。

# 追踪的重要性

当我们构建一个服务时，它基本上是某种数据源，依赖于其他服务或者拥有自己的数据库。

> 当我们依赖他人(他们的数据)并且我们无法控制他们的生命周期时，在需要的时候拥有证据总是一个好的做法，特别是当他们不合时宜并且试图将责任归咎于他人的时候。

# 分布式跟踪

分布式跟踪是一种我们可以在不同应用程序之间端到端跟踪数据流的方法。

[](https://opentracing.io/) [## OpenTracing 项目

### 本地启动 Jaeger $ docker run-d-p 6831:6831/UDP-p 16686:16686 Jaeger tracing/all-in-one:最新$ export…

opentracing.io](https://opentracing.io/) 

但是在所有应用程序中配置它们通常需要相当大的努力，并且该配置必须存在于所有应用程序中，以便所有中间应用程序将跟踪信息转发给下一个应用程序。

# 跟踪日志记录

如果我们没有时间和金钱在所有的应用程序堆栈中实现分布式跟踪，我们可以通过添加一个简单的跟踪日志来实现不负责任(当我们实际上是时)或快速知道问题(当我们实际上是错误的来源时)并采取行动。

我们将放置一个模式来记录相关数据，并且只记录搜索工具所需要的内容以**节省空间**和**索引时间**，搜索工具将扫描日志。

> ***这里的 Schema 基本上就是我们将日志记录在跟踪日志文件中的方式。这将是一个没有换行符和逗号分隔数据值的单行日志***

例如，如果模式如下所示:

```
TRACKING_ID, HOSTNAME, TIMESTAMP, RESPONSE_TIME, ACCOUNT_ID
```

一个真实的跟踪日志数据将会是这样的:

```
adef237-wkjh3j4h-218772, host-31a, 1638905687392, 300, 12891281928
```

我们希望它们是单行的。

> 一旦调用完成，我们将进行日志记录，因此对于对我们应用程序的调用，我们将在发送响应之前进行日志记录。对于来自我们服务的后端调用，我们将在获得后端响应后立即记录。

我们希望按照以下两种模式进行日志记录:

## 前端模式

这是日志的模式，当它到达我们的应用服务器时将记录调用。该日志模式日志将保存在**前端**日志文件中。

```
TRACKING_ID, REMOTE_IP, HOSTNAME, TIMESTAMP, VERSION, RESPONSE_TIME, ACCOUNT_ID,... all other data comma separated
```

***分析*** :

*   TRACKING_ID:这在所有调用中是唯一的，它可以由以前的应用程序转发(以便我们可以端到端地跟踪调用)。如果没有提供，我们将创建一个并发送给您
*   REMOTE_IP:调用方的 IP
*   主机名:我们的应用服务器的主机名
*   时间戳:呼叫的时间
*   版本:我们的应用程序的版本，以了解新部署的应用程序是否有问题
*   RESPONSE_TIME:调用在我们的服务器中花费的总时间
*   ACCOUNT_ID 或**主数据元素**:这应该是比呼叫中所有其他数据元素都重要的数据元素。例如，如果呼叫与帐户数据相关，则帐户是主要数据元素，如果呼叫需要地理定位，则纬度和经度是主要数据元素。

## 后端模式

这是从我们的服务器到我们所依赖的数据源的调用的跟踪日志的模式。该日志模式日志将保存在**后端**日志文件中。

```
TRACKING_ID, BACKEND_TRACKING_ID, TIMESTAMP, VERSION, ACCOUNT_ID, BACKEND_PRIMARY_DATA_ELEMENT, BACKEND_PRIMARY_RESPONSE_ELEMENT, BACKEND_RESPONSE_TIME, ... all other data
```

***分析*** :

*   TRACKING_ID:和以前一样，我们将把这个跟踪 ID 转发给我们从中获取数据的所有来源，并记录它。
*   BACKEND_TRACKING_ID:这将由我们的应用程序创建，对于我们调用的每个后端，我们将创建一个后端跟踪 ID。所以会有*多****back end _ TRACKING _ ID****每****TRACKING _ ID***
*   时间戳:呼叫的时间
*   版本:我们的应用程序的版本，以了解新部署的应用程序是否有问题
*   RESPONSE_TIME:调用在我们的服务器中花费的总时间
*   ACCOUNT_ID 或**主数据元**:同上
*   BACKEND_PRIMARY_DATA_ELEMENT:这是为了让后端调用知道向后端发送了什么，以便我们可以跟踪它。这可以通过一个以上的数据元素来实现
*   back end _ PRIMARY _ RESPONSE _ ELEMENT:同上，但这是我们从那个响应中得到的。我可以是一个或多个。
*   BACKEND_RESPONSE_TIME:服务或后端响应所花费的时间。

# 有用

现在我们已经正确设置了日志记录，让我们看看它是如何有用的:

## 手动调试

1.  一个调用来到我们的服务，我们处理它并调用一堆后端(db，api ),发送响应并记录在**前端**日志文件中。
2.  在调用后端时，我们也将每个调用记录在**后端**日志文件中。
3.  此时，对于**前端**日志的每一行，我们有多行**后端**日志行，它们通过 **TRACKING_ID** 相互关联。
4.  如果出现问题，涉众说我们的应用程序行为错误，发送了错误的数据，我们有适当的日志来支持。我们会询问呼叫的 **TRACKING_ID** 并跟踪我们的**前端**和**后端**日志文件中的所有日志，看看发生了什么以及我们返回了什么。
5.  如果他们没有 TRACKING_ID，我们会询问呼叫的主要数据元素，因为我们也记录了它，所以我们可以获得该呼叫的 TRACKING_ID，并以类似的方式进行跟踪。
6.  此外，当我们在跟踪日志的同时记录后端数据元素时，我们将了解后端是否返回了错误的数据。
7.  因为我们也记录了版本信息，我们也将了解一个问题是否源于我们的应用程序是因为新版本还是不是。

## 通过索引调试

1.  由于日志文件是单行的并且有索引，我们可以很容易地使用日志跟踪工具如 **Splunk** 和 **Elastic Search** 等对其进行索引(通过逗号分隔。)
2.  一旦建立索引，我们就可以根据数据得到很酷的图表，并对数据进行统计分析。
3.  我们甚至可以基于这些日志索引工具创建我们的应用程序仪表板，并将该仪表板发送给我们的利益相关者，以便他们也可以知道正在发生什么。
4.  基于版本的图表对于检查我们部署的影响非常有用。
5.  如果我们想推出基于地理位置的功能，我们可以基于这些日志和版本信息创建图表并进行分析。

# 结论

这些类型的跟踪日志有很多优点，因为它们精确、小、索引速度快，而且可以很容易地格式化，以满足不同的统计分析需求。

让我知道你对这种风格的跟踪日志的看法，会很有兴趣知道你的分析。

如果你喜欢这篇文章，请分享或评论这篇文章。非常感谢任何形式的互动。如果你想支持我并接触到媒体中所有伟大的事物，请加入并成为会员。这是我的推荐链接:

[](https://susamn.medium.com/membership) [## 加入 Medium，我的推荐链接- Supratim Samanta

### 作为一名中型会员，您的部分会员费将支付给您所阅读的作家，您可以完全接触到每个故事……

susamn.medium.com](https://susamn.medium.com/membership)