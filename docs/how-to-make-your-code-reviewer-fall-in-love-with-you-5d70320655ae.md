# 如何让你的代码评审员爱上你

> 原文：<https://levelup.gitconnected.com/how-to-make-your-code-reviewer-fall-in-love-with-you-5d70320655ae>

对于寻求评审的人和评审者来说，代码评审有时都是一项艰巨的任务。但也不尽然！

我有一些了不起的导师，他们让我坚持最高的代码质量标准，老实说，一开始是痛苦的——即使在第四次代码审查后，也没有做对。让一个高级开发人员或同行投资你的成长是非常有价值的事情——所以我们不想想当然地认为这是值得的。

最近，我花时间回顾了我为自己做的笔记，这些笔记是我参加的几次代码评审和我遇到的优秀代码质量指南的一部分。

# #1 规则:评论者的时间是黄金。

做你自己的代码评审员，尽早发现错误，这样你的评审员就可以专注于给你高质量的反馈，而不会因为缩进错误而失去理智。

在要求进行代码审查之前，我们可以检查以下内容:

# 清楚

*   对于新手来说，代码应该易于阅读。你应该一眼就明白每一行和每一个函数是做什么的。
*   **单一责任原则**要求“*一个类应该有且只有一个理由改变”*。每个函数都应该有一个简明的意图(这个目标是处理一个 API 请求，还是仅仅是一个日期时间实用函数，这取决于你所处的抽象层次)。
*   比起小的优化，更喜欢可读性。抵制将一段代码压缩成一行以使其看起来很酷的诱惑。让别人(和你未来的自己)的生活更轻松更酷:)
*   代码被注释掉了吗？很少有这样合适的情况。
*   将功能性和非功能性变更分开。如果您的更改涉及两行代码的更改，但是您格式化了代码文件以修改制表符/空格，并将其作为同一代码评审的一部分，那么对于您的评审人员来说，找出实际的更改将是一项令人沮丧的工作。

# 功能

*   代码中是否存在**逻辑缺陷**？
*   代码处理边缘情况吗？
*   这一变化是否完全满足了所有功能/问题的要求？需求是如何被解释的有任何模糊之处吗？
*   你添加的代码是线程安全的吗？线程安全性和并发性是在类或 API 级别记录的吗？

# 试验

*   是否有**单元测试**来充分测试代码，它们是否已经运行？
*   有没有一个代码覆盖工具可以自动运行在构建中？(例如[雅高](http://www.eclemma.org/jacoco/))

![](img/67338ee4b5fbc0d147a069772b2c6e09.png)

# 抽象

*   **不向客户透露实施情况**。虽然函数名应该反映它的效用，但它不应该透露调用者没有使用的实现细节。更重要的是，面向客户端的 API 文档不应该公开实现细节。想象一下，如果谷歌地图 API 文档告诉你他们从哪个数据库获取数据
*   数据库访问操作(DAO)被抽象成它们自己的类了吗？
*   当我们设计一个应用程序时，我们从高层次的设计开始，然后逐步深入到低层次的实现。同样，我们的代码也应该反映它。每个函数应该连接一个抽象层次，调用更低层次的函数。

# 风格

*   代码应该遵循该语言固有的**风格指南**。例如，camelCase 是 Java 中的命名约定，而 Python 建议使用 snake_case。
*   也就是说，代码应该符合模块中已经使用的样式(缩进、间距、命名约定等)。在某些情况下，风格指南提出建议，而不是声明需求。在这些情况下，需要判断新代码是否应该与建议或周围的代码一致。

# 证明文件

*   **每个功能的意图都清楚吗**或者描述期望的最小注释会有帮助吗？
*   公共方法和类是用 Javadoc (Java)还是 Doxygen (C/C++)记录的？
*   记录意图是最重要的记录形式。其他工程师在查看代码(甚至他们自己的代码)时最大的问题是，“为什么这些代码在这里？”，或者“他们(我)为什么要这样做？”，或者“这段代码解决了什么具体问题？”。
*   写一个清晰的变更描述——如果你正在使用一个工具来生成你的代码评审，把你的代码推到一个单独的分支，或者只是把你的代码变更以压缩的形式发送给他们(哎呀！)，你应该简单描述一下你的变化。你可以把它想象成一个高层次的设计图表——但是要使用文字。
*   如果您的变更是添加一个新功能或涉及对现有功能的重大修改，请考虑使用一个专用的设计文档来帮助人们轻松地使用它。高层次或低层次的图表是额外的奖励。

# 重用和重复的代码

*   **代码在包内是否重复**？如果在一个模块中有几行代码重复了不止一次，这就表明需要重构。
*   不要多此一举。有没有可以完全删除或用现有库替换的代码？没有代码就像没有代码一样！
*   尽可能使用注释来保持你的代码更容易阅读并且没有错误，同时在你的团队中建立一个通用的标准(例如 Lombok for Java)

# 配置和常数

*   代码中有没有分散的或者重复的**幻数或者字符串常量**？
*   代码是否有应该可配置的任意常量值？
*   尽可能用像 **final** (Java)或 **const** (JS) 这样的修饰符来定义变量。虽然像 **final** 这样的关键字确实提供了较小的性能优化，但它与人相关的重要方面是关于关键字的语义。这意味着变量在整个范围内保持不变，从而提高可读性和可维护性。

# 属国

*   避开**明星进口**。仅导入您需要的库依赖项。
*   是否引入了可能带来新的安全或运营风险的新的外部依赖？
*   是否有替代的轻量级依赖关系可以使用？
*   您是否每次都在创建依赖项，而不是注入或重用它们？**依赖倒置原则**声明依赖应该是松散耦合的。它要求代码单元(类、方法、模块)应该声明依赖关系，而不是创建依赖关系。

# 异常处理

*   代码对垃圾和空输入有弹性吗？
*   是否有清晰一致的异常处理策略？
*   您是否在 catch 块中记录了在函数中遇到的错误，然后抛出该错误供调用函数再次捕获？“记录并丢弃”是一种已知的反模式。可以参考这个优秀的栈溢出[回答](https://stackoverflow.com/questions/6639963/why-is-log-and-throw-considered-an-anti-pattern)。

# 表演

*   是否有迹象表明**过度设计或过早优化**？
*   是否有明显的性能或效率问题需要解决？

# 使用仪器

*   我们有没有**指标**来分析我们变革的影响？数字比“我们看到了巨大的进步”更有说服力。
*   从错误到调试的所有级别都有适当数量的日志记录吗？
*   每个日志消息是否包含足够的相关信息，以便人们仅通过阅读日志消息就能理解系统的行为？使用带有适当标识符的日志记录。

# 一般

1.  将大的代码评审分成小的。一个好的规则是在代码评审中不要有超过 150 行的新代码。变化越大，你的评审者在评审时需要记住更多的上下文，小错误可能会被忽略。
2.  尝试利用该语言的最新发展来编写代码，这可能会提高可读性或可伸缩性。例如，在 Java 中，更喜欢流而不是循环。在 JS 中，使用 ES6 语法。
3.  以建设性的方式接受批评。代码审查不是人身攻击，即使审查者的语气看起来像是指责。客观地看待它，就好像你们正在集体努力使代码变得更好。
4.  自动化枯燥的东西。Git 挂钩对于自动化各种东西来说非常酷。
5.  如果你的评论是错误的，要有耐心。抵制快速回复的诱惑，转而去思考你的代码是否缺乏清晰度，从而导致他们感到困惑。

幸运的是，我们可以遵循许多其他好的编码实践来改进我们的代码和代码审查。

[这是我最喜欢的一个](https://mtlynch.io/code-review-love/)(也是这篇文章名字的灵感来源)。

我希望你的评论家崇拜你！万事如意。