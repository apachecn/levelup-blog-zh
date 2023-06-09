# 成功部署应用程序的经过验证和测试的策略

> 原文：<https://levelup.gitconnected.com/proven-tested-strategies-for-successful-application-deployment-d59dd786020d>

![](img/d9eca0dbcbb890084d497bc1fcaffc6a.png)

这是我们的应用程序架构系列的最后一集，其中我们将讨论应用程序部署的方法。如果你想了解更多关于单片和微服务的知识，当然也可以看看第一章[和第二章](https://medium.com/codex/monoliths-or-microservices-the-critical-differences-between-approaches-to-application-architecture-adb6a8e93aa)[和第三章](/6-tradeoffs-between-monolithic-and-microservices-architecture-you-need-to-keep-in-mind-f7dd5c5cda4)。

无论选择哪种架构，都可以使用一组优秀的开发实践来优化发布和维护阶段的应用程序生命周期。采用这些原则可以提高健壮性，减少恢复时间，并使服务如何处理传入请求变得清晰。

**健康检查、度量、日志、跟踪和资源使用都是这些过程的一部分。**

**健康检查**
健康检查用于显示应用程序的执行情况。这些测试确定应用程序是否启动并运行，以及在处理传入流量时是否如预期那样运行。健康检查通常由 HTTP 端点表示，如/health 或/status。这些端点产生一个 HTTP 响应，指示应用程序是否健康。

**指标**
需要指标来量化应用程序的性能。为了正确理解服务如何工作，有必要收集关于服务如何处理请求的数据。例如，活动用户、处理的请求和登录的数量。此外，程序正常运行所使用的资源数据也很关键:CPU、ram 和网络吞吐量的数量。通常，度量的集合是通过 HTTP 端点(如/metrics)交付的，它包含内部数据，如活动用户数、消耗的 CPU、网络吞吐量等。

**日志**
日志聚合提供了关于服务在任何给定时间如何运行的有用信息。任何故障排除和调试过程都围绕着它。例如，跟踪用户是否成功注册了某项服务，或者在付款时遇到了问题，这一点至关重要。
被动日志记录技术通常用于从 STDOUT(标准输出)和 STDERR(标准错误)收集日志。这意味着应用程序的输出和错误被传递给 shell。然后，使用 Fluentd 或 Splunk 等日志记录解决方案收集这些信息并保存在后端存储中。
另一方面，应用程序可以将日志直接传输到后端存储。在这种情况下，使用主动日志记录，因为日志传输由程序直接处理，不需要日志记录工具。

一个操作可以有多个日志记录级别。应用最广泛的有:
DEBUG——记录应用程序进程的细粒度事件。

信息—提供有关操作的粗粒度信息。

警告—记录服务的潜在问题。

错误—通知遇到错误，但是应用程序仍在运行。

致命—表示应用程序无法运行时的危急情况。

此外，标准做法是为每个日志行提供一个时间戳，这将精确地记录操作的执行时间。

**跟踪**
跟踪可以提供几个服务如何被用来完成一个请求的完整视图。跟踪通常在应用层使用一个库来实现，该库允许开发人员跟踪某个服务何时被调用。单个服务记录被组织成范围。重新创建请求的完整生命周期的跟踪是由一组跨度定义的。跟踪被定义为重新创建请求的完整生命周期的跨度的集合。

**资源消耗**
术语“资源消耗”是指程序正常运行所需的资源。这通常是指程序运行时消耗的 CPU 和内存量。此外，对网络吞吐量或一个应用程序可以并发处理多少请求进行基准测试也是有益的。为了保持应用程序一周 7 天、一天 24 小时不间断运行，了解资源限制是至关重要的。

**维护**
产品发布后，无论是单片还是基于微服务的程序都进入维护阶段。在此期间，应用程序的结构和功能可能会发生变化，这是可以预见的！应用程序的架构是不断变化的，不是静态的。这是由消费者的投入和新技术驱动的产品有机增长的结果。
在添加新功能或采用新技术时，如果我们从服务水平的角度考虑，最好将可扩展性置于灵活性之上。一般来说，使用定义良好的基本功能来管理大量服务(如微服务的情况)比添加更多的抽象层来容纳新服务(如 monoliths 的情况)更有效。但这并不意味着您应该忽略灵活性缺陷。所以，这两个因素在不同的情况下都有意义。最终，主要目标是始终为用户和客户带来价值。
至于架构变更，有必要理解为什么为一个应用程序选择一个特定的架构，以及有一个结构良好的维护阶段所涉及的权衡。以下是维护期间最常执行的一些操作:

拆分操作—当服务功能过多且难以管理时相关。在这种情况下，更小、更易管理的部分是更可取的。

合并操作—用于合并粒度过细或执行紧密互连功能的单元的操作。例如，将两个不同的日志输出和日志格式服务组合成一个服务。

替换操作—当找到一个更有效的服务实现时相关。例如，在 Go 中重写一个 Java 服务，以减少总的执行时间。

陈旧操作—与对公司不再有用的服务相关，应该归档或废弃。例如，用于执行一次性迁移的服务。

这些活动中的任何一项都将有助于项目持续更长时间并保持在正轨上。总的来说，目标是保证应用程序为消费者增加价值，同时也便于技术团队管理。除此之外，您可以看到项目的结构不是静态的。它是无定形的，并且会根据客户的新需求和输入而变化。

寻求更多信息。
[Artyom](https://www.linkedin.com/in/artyom-koshko-87629985/) ，高级软件工程师

参考资料:
-[www.udacity.com](https://www.udacity.com/course/cloud-native-application-architecture-nanodegree--nd064) -[docs.microsoft.com](https://docs.microsoft.com/en-us/azure/architecture/microservices/migrate-monolith)
[-YT—1500 微服务中的现代银行](https://www.youtube.com/watch?v=t7iVCIYQbgk)