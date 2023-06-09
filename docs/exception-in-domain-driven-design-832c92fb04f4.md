# 领域驱动设计中的异常

> 原文：<https://levelup.gitconnected.com/exception-in-domain-driven-design-832c92fb04f4>

引入了异常来处理函数级的错误。目的是避免返回错误代码，并消除返回类型的不确定性。异常的威力来自于它们向下传播堆栈的能力。您没有义务直接处理异常。它允许您将正常的代码流与错误处理分开。

![](img/2729ff9ae18dc2111623161bd90ab857.png)

当函数关于参数的假设被打破或者函数不能实现它的承诺时，应该抛出一个异常。最简单的例子就是除以零。我们必须向打电话的人发出信号，表示我们无法提供答案。例外构成功能合同的一部分。在语言学中，这有时被称为预设失败。考虑一下如果法国国王是秃头的问题。法国没有国王，所以我们不能用“是”或“不是”来回答。任何这些答案都是误导性的。

# 作为领域语言一部分的异常

将异常视为领域语言本身的一部分是很方便的。这是一种很好的交流方式。像 OrderLimitExceeded 这样的业务异常非常重要，而且信息丰富。通过浏览例外列表，你可以获得关于业务期望的重要信息。有必要建立一致的域异常层次结构。例如，如果您的 Order aggregate 可能会引发许多不同的异常，作为其 API 的一部分，所有这些异常都应该扩展一个类似 OrderException 的异常。这样更容易处理。事实是，控制异常流不是一件容易的事情，它需要大量的训练。否则迟早会失控。

# 异常的问题

不幸的是，例外并不理想。它们破坏了代码的自然控制流。这是乔装打扮的 GOTO。使用异常也增加了接口的复杂性，增强了耦合性。抛出一个异常会破坏引用的透明性，所以我们的方法并不纯粹。我们的函数没有单一的返回点，这极大地阻碍了推理。

例外还有另一个大问题。异常可能导致模型的不一致状态。如果某些操作无法完成，模型应该保持与以前相同的状态。开发人员并不总是注意这一点。在计算过程中，当模型状态仅被部分改变且不一致时，通常会引发异常。你的 IDE 和编译器都不会帮助你解决这个问题。

最近的一项研究表明，分布式系统中 90%的故障都与错误处理有关。

# 功能方法

使用类似 monad 的容器类型，比如 Option、or Result，可读性更好，也更优雅。这些是面向函数的语言中众所周知的结构。我们可以在设计 API 时考虑单一的返回类型，不要扭曲控制流。

```
Order.addItem(Item $item): Either[Order, Error]
```

添加项目可能会导致新订单(包含该项目)或错误。指定我们可能从该方法中获得的错误类型(OrderItemsNumberExceed，CanNotAddItemToFinishedOrder)是必不可少的。这个 API 优雅而完整。返回类型明确地告诉我们，对于任何参数，我们可能都没有有效的答案。我们可以使用联合类型或泛型 OrderError，并在方法文档中描述错误，但依赖类型级安全总是更好。

必须能够在语言层面上轻松地对多个调用进行排序，而无需担心错误处理。当情况如此时，它是极好的。
Option，要么，Result——保留单子特征的类型很容易组合。这不会破坏正常的控制流或引用透明性。但是如果没有语言层面的语法支持，结果可能会很麻烦。否则，例外可能是更有吸引力的选择。

# 放弃

这篇文章只涉及业务领域环境，可能不适用于底层或基础设施环境。

# 分级编码

感谢您成为我们社区的一员！更多内容请参见[升级编码出版物](https://levelup.gitconnected.com/)。
跟随: [Twitter](https://twitter.com/gitconnected) ， [LinkedIn](https://www.linkedin.com/company/gitconnected) ，[迅](https://newsletter.levelup.dev/)
**升一级正在改造理工大招聘➡️** [**加入我们的人才集体**](https://jobs.levelup.dev/talent/welcome?referral=true)