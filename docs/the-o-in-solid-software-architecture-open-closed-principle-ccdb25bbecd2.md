# 固体软件架构中的“O”——开放封闭原则

> 原文：<https://levelup.gitconnected.com/the-o-in-solid-software-architecture-open-closed-principle-ccdb25bbecd2>

## “O”代表开放封闭原则，促进扩展而非修改。

Bertrand Meyer 在 1988 年首次提出了“开闭原则”,并写下了这句名言

> 软件实体(类、模块、函数等。)应该对扩展开放，但对修改关闭。

![](img/75b17768a46149f75e28f39ceb1d18d4.png)

如果我们可以用一个新镜头来扩展我们的相机，我们就不需要拧开它。(由卢卡斯[法夫尔](https://unsplash.com/@we_are_rising?utm_source=medium&utm_medium=referral)

这意味着，如果我们想要实现一个新的特性，应该很少需要修改现有的代码。起初，这似乎有点矛盾，因为软件一直在变化，它的代码也是如此，对吗？重构甚至修复 bug 呢？

让我们看一个具体的例子来理解这个原则试图推广什么。下面的例子是用 Typescript 编写的，但是很容易阅读——它是关于基本思想，而不是确切的代码。假设我们希望通过将应用程序中的事件发送到特定的通道来做出反应，在这种情况下，可以是*电子邮件*、*文本*或*推送通知*。

这段代码很难扩展，因为每次实现发送通知的新方法时，都需要进入`broadcast()`方法并添加另一个 if-block。这就是人们所说的“修改”。

当多人同时使用不同的广播方式时，这可能会导致合并冲突。同样，当一个项目“成长”时，通常会在基本模块之上添加更多的抽象。

在我们的示例中，这意味着其他模块可以依赖 NotificationHandler 将给定事件广播到正确的通道。所以当一个人在修改这个基本模块时犯了一点小错误，这个错误将潜在地影响到所有基于这个模块的代码。在这个例子中，这样的错误可能是在方法的末尾添加了一个新的 if 块。哎呦。我们可能忽略了`if(!user.phone) return`，当电话号码丢失时，它会阻止我们的新添加被执行。也许我们没有为我们的新功能编写一个测试来覆盖丢失的电话号码。

那么，我们如何保持开放来“扩展”我们的模块，而不是修改它呢？考虑一下这个:

我们在这里实现了[策略模式](https://sourcemaking.com/design_patterns/strategy)。我们不是在`NotificationHandler`中决定事件应该如何呈现给用户，而是将“如何”作为一个策略传递，在本例中是作为一个实现`Broadcaster`接口的类。然后，处理程序可以通过广播器发送消息，并处理所有通知之间的公共事务(例如错误处理)。

这些结构上的变化使我们能够

*   添加一种新的发送通知的方式，而不需要修改现有的代码——我们只需要添加一个实现`Broadcaster`的新类
*   开发多种方式同时发送通知而不发生冲突(意味着更高的开发速度和更大的灵活性)
*   开发新的`Broadcaster`而不必担心破坏任何现有的功能——我们也可以很容易地单独测试它们
*   遵循[单一责任原则](https://medium.com/@richartkeil/the-s-in-solid-5a6e0d778cbc)，确保我们的每个模块只有一个改变的理由

一般来说，当实现一个与现有特性同类的新特性时，应该考虑开闭原则。就像我们的例子中发送通知的新方式。

然后，通过将不同的特性提取到它们自己的模块中，并且只保留基本模块中的相似性，可以提高代码的质量。通过传入特性模块，基本模块不需要知道实际存在什么或者有多少特性——它只依赖于它们的接口。

正如 Robert C. Martin [指出的](https://blog.cleancoder.com/uncle-bob/2014/05/12/TheOpenClosedPrinciple.html)这种方法已经被允许定制插件的应用大量采用:

> “我听说 OCP 不适合有实际工作要做的真正的程序员。插件架构的兴起表明这些观点完全是胡说八道。[……]强大的插件架构可能是未来软件系统最重要的方面。"

当根据开放封闭原则构建软件时，应该牢记其初衷:在不破坏现有代码的情况下简化新功能的添加。盲目地将一行语句提取到自己的模块中是没有用的。

开闭原则通常被认为是软件架构最重要的设计模式之一。根据我的经验，它的实现通常会对新特性的实现速度产生直接和积极的影响。

如果你觉得这篇文章有帮助或者有任何反馈，请告诉我——我非常感激！

通过在我的博客上注册[，获得关于新帖子的电子邮件通知。](http://blog.richartkeil.com)