# 在生产中获取调试日志的 3 种方法

> 原文：<https://levelup.gitconnected.com/practical-solutions-for-your-debug-logs-db12f083f539>

![](img/0dc12ff242982d5ffd8d6061d9cf6ec3.png)

在生产中启用调试日志

调试日志…离不开，离不开。“生产中的调试”总是很棘手。始终在调试级别记录太冗长。对数噪声是无用的，它会占用太多的空间。完全不记录它们就失去了拥有它们的意义。那么快乐的媒介在哪里呢？

让我们首先理解调试日志是用于调试的——这意味着存在一些问题或错误。我们都同意我们有时需要日志，但不是一直需要。那么你能做什么呢？以下是我遇到的一些解决方案。我先说我最喜欢的。希望你的公司不会犯这些[常见的错误](https://medium.com/swlh/28418cab02b4)，并允许你这样做！

# 事件驱动的调试日志

我最喜欢的方法是基于触发器的日志转储。大多数现代语言和框架将允许您拥有多个日志处理程序。您可以添加一个处理程序来跟踪所有(包括调试)日志，但是只在内存中保存 N 个最近的日志。您需要捕获一个事件，比如一个异常或一个错误级别的日志，这将指示您的日志处理程序转储所有 N 个最近的日志。

✅ **优势**:在所有故障第一次发生时自动获取调试日志。不需要重复/等待 bug。没有日志基础设施的开销。添加“太多”调试日志是可以的！

**🛑不利方面**:你的“n”值可能捕捉到太多或太少。您的框架必须支持多个日志处理程序。

![](img/2f7facb8d4bf1f98af6a0e29b42ebd0a.png)

接收事件驱动的调试日志的日志处理程序之间的关系。

这里有一个用 python 编写的[概念证明](https://github.com/mikhail/recent_log_handler)。我在自己的项目中使用了非常相似的东西。其中一个聪明的应用是将您最近的日志直接发送到 PagerDuty，而不是发送到您的常规处理程序。小心不要包括任何 PII！

旁注—我对[logz . io](http://logz.io)自动日志模式检测印象深刻:

# 动态日志控制

一种常见的生产解决方案是“动态测井”控制。这允许您切换(无需重新部署)日志级别。然后，您等待错误再次发生。

✅ **好处**:控制可以非常灵活，每个服务，每个文件，如果你想保存你的日志基础设施，你甚至可以把一切都静音(坏主意)。自己实现相当简单，尤其是如果已经有了发布/订阅系统。

**🛑不利的一面**:在你再次发现这个错误之前，你可能会得到成千上万个你实际上并不需要的调试日志。或者，根据粒度的不同，您可能得不到您需要的东西！如果是罕见的 bug 就很难使用。

![](img/6be3f7adbffeec0479ef3fa3e794cc3a.png)

Apache Storm 的例子([https://Storm . Apache . org/releases/2 . 0 . 0/dynamic-log-level-settings . html](https://storm.apache.org/releases/2.0.0/dynamic-log-level-settings.html))

更好的配置是允许你指定一个采样百分比，这样你就可以在流量非常高的时候打开它。当然，如果您正在寻找一个特定的 bug，这有可能无法捕捉到您需要的东西，但是对于一般检查来说，这是一个有用的配置。

# 带调试的重放

另一个聪明的解决方案需要一个完全幂等的架构和一个无状态的系统。如果出现故障，您可以使用一个标志重复有效负载，该标志指示服务器应该启用调试。

✅ **优势**:按需获取调试日志。您只能获得您需要的调试日志。如果标志为“sticky”，这可能会传播到整个系统没有忘记撤销，因为它的需求。

**🛑不利方面**:架构需要考虑到这一点。如果至少有一个微服务不支持它或者不是幂等的——你就倒霉了。

如果您有复杂的体系结构，并且还没有为此做好准备，那么您可以采用这种方法的变体。建立一个完整的“调试环境”,然后在生产中记录并在这个新环境中重放。这是*而不是*并且很容易做到，因为环境中的任何状态变化都会使您的调试无效。一个很好的例子是在进行复杂计算的无状态可执行程序中。在那里你可以通过 [GDB](https://www.gnu.org/software/gdb/) 作为“记录和重放”功能进行调试；如果你需要低级调试，请查看 rr 项目。

你喜欢这篇文章吗？有没有其他很棒的方法？留言评论！