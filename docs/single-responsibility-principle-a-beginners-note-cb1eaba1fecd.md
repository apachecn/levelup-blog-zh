# 什么是单一责任原则？

> 原文：<https://levelup.gitconnected.com/single-responsibility-principle-a-beginners-note-cb1eaba1fecd>

## 编写伟大的代码是一门艺术

![](img/c76f1e0bb951dcefebf14102a51c2dac.png)

# 单一责任原则

单一责任原则是关键的软件工程原则，它决定了我们应该如何在面向对象编程中模块化代码。

省得你去网上查，它的定义是“一个类应该只有一个责任”，马丁进一步定义为“一个改变的理由。”

[Robert C. Martin](http://blog.cleancoder.com/) 将单一责任原则描述为:

> "一个类应该有**一个**，并且只有一个，改变的理由."

单一责任原则的论点相对简单:它使你的软件更容易实现，并防止未来变化的意外副作用。

假设你有一个类在你的程序中做几件事。我喜欢称这些为“最高阶层”。当您必须更新/更改代码时(您将会这样做)，过多的职责将会使隔离和修复问题或更新程序变得更加困难。

在软件开发过程中，需求不断变化是很常见的。每个需求变更都会修改至少一个类。你的类的职责越多，你就越需要经常改变它。

一旦你的类的一个职责发生变化，你就要改变它。如果它只有一个职责，这显然比您需要更改它的次数要多。

SRP 要求严格的模块化，反过来，它创造了将一个程序与不同的功能部分组合在一起的能力。

![](img/f286943b5e583afd0e75496cf1c19463.png)

这就像经典的俄罗斯方块游戏，一个沉重稳定的结构可以用几个定义好的小积木搭建起来。但是这里重要的一点是，这些块应该很小，定义良好，并且可以在任何地方重用。

SRP 初看起来似乎很容易，但它可能是实践中最难遵循的坚实原则。让我们看看为什么会这样。

遵循 SRP 是困难的，因为“变更的理由”只有在将来需求实际变更时才变得确定。在设计时，我们所能做的就是估计哪些需求是可能改变的，哪些是稳定的。

SRP 不可避免地涉及一定量的预言工作。

一些开发人员建议每个对象/类应该只做一件事。他们说的一件事是什么意思？当我查看一个类或一个方法时，我如何知道它是在做一件事还是不止一件事？

SRP 的这个定义甚至比最初的定义更模糊。

# 变化的影响

我们举个简单的例子。

这可能看起来像一个合理的类。我们有一本书，它可以提供书名，作者，还可以翻页。最后，它还能够在屏幕上打印当前页面。但是有一个小问题。

再看`printCurrentPage()`方法，打印页面的内容，这应该是`Book`类的责任吧？你可能会说:“为什么不呢？”但是想想这个。

如果有一项业务变更，规定页面内容应该在 HTML 页面和记事本文档中显示，该怎么办？

这一变化影响了`Book` 类，因为上面代码中的`Book`类也拥有打印的额外职责。这个额外的责任导致类由于与`Book`的行为无关的业务变化而变化。

这是一个更简洁的方法，因为`Book`类现在将返回当前页面的内容，而不是像以前那样自己打印。

现在当显示内容的要求改变时,`Book`不必改变。因此,“一个类，一个责任”的口号帮助我们创建定义良好的模块。

即使是这个非常基本的例子也显示了如何将表示从业务逻辑中分离出来，并尊重 SRP，从而为我们的设计灵活性带来巨大的优势。

# 变化的影响

这种变化可能看起来不像是一个大交易，但是把这个类看作是大软件的一部分。现在，我们对`Book`类所做的任何更改都会额外影响依赖于被更改的`Book`类的所有类或组件。

根据所做的更改，您可能需要更新依赖项或重新编译依赖类，即使它们不会直接受到您的更改的影响。

它们只使用由`Book`类实现的其他职责中的一个，但是您仍然需要更新它们。

最后，您需要更频繁地更改您的类，并且每次更改都更复杂，有更多的副作用，并且需要比它应该做的更多的工作。所以，最好通过确保每个类只有一个责任来避免这些问题。

我们再举一个例子。

通过看这个例子，我们意识到每个`Employee` 的算法可能是不同的，并且改变的请求可能来自不同的部门。

这是一个很好的例子。当我们将`Employee`类中的算法分解成独立的算法时，我们可能会避免在一个类中维护三个不同的算法(可能每个算法都容易改变)的麻烦。

问题是:“我们怎么知道我们需要这样做？我们怎么可能知道这是一件好事呢？”

因为我们在考虑领域。

# 软件设计需要对未来进行有根据的猜测

将软件设计等同于踢足球的中场是很好的。一个伟大的中场球员对周围环境非常敏感，经常会被安排在队友需要他们的位置，甚至在他们知道他们需要他们之前。

软件设计和架构是相似的。我们(通过抽象和接口)对我们预测的未来需要发生的事情做出最佳猜测，而没有投入所有的前期精力来实现我们不需要的东西的具体化( [YAGNI](https://martinfowler.com/bliki/Yagni.html) )。

了解你工作的领域。

如果我们不了解我们正在编写代码的领域，我们注定会犯昂贵的错误，因为软件需求肯定会随着时间而改变。

因此，我相信如果你了解领域，单一责任可以正确地完成。

# 最后的想法

你可以在你的问题中实现 SRP，在你做任何改变之前问一个简单的问题:“你的类/组件/微服务的职责是什么？”

如果你的答案包含“和”这个词，你很可能违反了单一责任原则。然后，最好退一步，重新思考你目前的方法。很可能有更好的方法来实现它。

SRP 有助于问题和任务的提炼。随着时间的推移，你学会了如何将巨大的问题分解成最小的公分母，并构建函数来解决更大的问题难题中的小问题。

不知不觉中，您已经解决了这个巨大的问题，并创建了一个优雅、高效、易于维护和改进的程序。

# *延伸阅读*

*   【https://stackify.com/solid-design-principles/ 

[](https://khalilstemmler.com/articles/solid-principles/single-responsibility/#Discussion) [## 领域知识&单一责任原则解释| SOLID Node.js +…

### 本文是 Solid Book——软件设计和架构手册 w/ TypeScript + Node.js 的一部分

khalilstemmler.com](https://khalilstemmler.com/articles/solid-principles/single-responsibility/#Discussion) 

*   [https://webolutiondesigns . com/single-respons ibility-principle-SRP](https://webolutiondesigns.com/single-responsibility-principle-srp/)

[](https://gitconnected.com/resume-builder) [## 软件工程师简历生成器和示例| gitconnected

### 免费打造不到 5 分钟的高质量软件工程简历。同步您的个人资料，我们会处理…

gitconnected.com](https://gitconnected.com/resume-builder)