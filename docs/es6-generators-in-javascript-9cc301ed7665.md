# JavaScript 中的 ES6 生成器，一个真实的用例

> 原文：<https://levelup.gitconnected.com/es6-generators-in-javascript-9cc301ed7665>

## 开发人员很难理解何时使用生成器——通过理解这个真实世界的用例来学习如何集成它们。

![](img/848b0cbd12b6ccd1a3eaecdf90e4fd58.png)

照片由[乔恩·赛勒](https://unsplash.com/@eyefish73?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText)在 [Unsplash](https://unsplash.com/s/photos/generator?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText) 上拍摄

# 我对发电机的问题

我不介意承认，自从发电机问世以来，我很难理解它们能为我解决什么问题。虽然[文档](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Iterators_and_Generators)全面而有用，但我仍然对它们的应用感到有点不确定。

我最近偶然发现了一个我认为有效的用例，它可能对帮助其他人理解他们能做什么大有帮助。这绝不是对 JavaScript 中生成器的深入探究。然而，对于那些和我一样，仍然在寻找可以使用这个新特性的上下文的人来说，它可能是对文档的补充。

我保证没有涉及质数或斐波那契模式的例子。

# 发电机粗略指南

在我们看一些代码之前，我想我应该总结一下我对生成器的理解。

来自[文档](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Iterators_and_Generators):

> 生成器函数允许您通过编写一个不连续执行的函数来定义迭代算法

这里的区别是不连续的执行。当我们用 JavaScript 编写同步函数时，我们通常期望函数内部的代码会一直执行，直到我们到达一个返回语句、一个错误或函数块的末尾:

通过一个生成器函数，我们用关键字`yield`改变了期望值。当我们在函数中遇到`yield`时，我们表示希望暂停执行，允许我们在完成执行之前从函数*中获取一个值，或者将一个值放入函数*中:**

在这个公认的人为例子中，我们可以在到达返回语句之前从函数*中提取出 *shouty* 值。让我们看看如何向暂停的函数传递一个值:*

向由[迭代器协议](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Iteration_protocols#The_iterator_protocol)公开的`next()`方法传递一个值允许我们在恢复执行时使用它。

正是这些类型的例子让我想知道更多，并让我更多地考虑生成器的实际应用。

# 打字机的问题

在开发文本冒险游戏引擎时，我需要创建一种模拟字符串输入效果的方法。我想要一个实现，在这个实现中，我可以用一个字符串递归地调用一个函数，来检索这个字符串的新的类型化表示，直到它完成为止。

我的第一个方法是这样的:

这个解决方案在很大程度上满足了我的需求。但是，有一件事感觉不太对劲。由于函数的连续性，我*有*向它公开我的`print`函数。这是作为上面示例中的参数注入的，还是在封闭范围或上下文中公开的。

有了这个约束，我的输入函数不仅负责输入字符串，还负责打印它。这种隐式打印感觉有些不对劲，如果我想对字符串的类型化状态的每次迭代做些别的事情呢？

如果有一种方法可以在每次迭代中暂停函数的执行并提取值，我可以简单地将该值传递给负责打印的函数——或者其他任何相关的函数。

这听起来像是一个发电机能够解决的实际问题！值得注意的是，在没有生成器的情况下，实现我所需要的*当然是可能的。然而，在这种情况下，我发现生成器实现更简洁，也更容易推理:*

这里我们可以用一种更简单的非连续方式来表达我们的递归。我们的`type`函数现在对打印我们的值一无所知，也没有隐式处理打印的副作用。

为了完整起见，这里有一个完整问题的模拟实现，我们的关注点是分开的。根据您的浏览器的年龄，您应该能够将它直接复制并粘贴到您的控制台中，以查看它的运行情况:

这个例子的特点是模拟人类输入短语的`print`函数的异步实现。我们在字符串的每次迭代之间添加一个定义好的短暂停顿。现在我们的`print`函数可以处理*只是*打印，而我们的`type`函数可以处理*只是*打字。

# 进一步阅读

在我的实现中，有一点我没有提到，但我认为值得一提的是在事先不知道集合长度的情况下迭代集合的能力。当考虑性能和内存消耗时，在这种情况下暂停迭代执行的能力是至关重要的。

为了将它放在我的输入示例的上下文中，想想如果我们事先不知道这个短语，或者如果我们不确定这个短语是否包含无限数量的字符，我们将如何处理这个问题。我们可能想要暂停当前的迭代，以确保我们有足够的资源来处理下一个迭代*。*

# 结论

我希望这有助于那些和我一样，在规范第一次引入时感到有点困惑的人理解生成器。这个例子仅仅触及了生成器和迭代器的表面，所以我鼓励大家看看 [MDN 文档](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Iterators_and_Generators)，并开始思考它们在什么地方可以为现实世界的问题提供简洁。