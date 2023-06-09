# 重构代码的 5 个技巧

> 原文：<https://levelup.gitconnected.com/5-tips-for-refactoring-code-96265a50f1de>

![](img/e1d37daffa15f72fc6302975ae4dc901.png)

需求改变，QA 发回构建，您继承旧代码，或者您的技术堆栈需要更新。无论哪种方式，在某种程度上，你都必须走上重构的道路。这个指南将帮助你避免一些常见的陷阱，节省你的时间和挫折。

# 1.制定行动计划

![](img/de04407fda5156bfae035f4b0c1c38fe.png)

在开始重构代码之前，创建一个行动计划。从需求开始，记下当前可用的和需要改变的列表。你应该能够回答下列问题。

1.  有什么新要求？
2.  当前代码中有多少能够解决新的需求？
3.  您的更改会对应用程序产生什么影响？
4.  你的改变会影响到其他开发者吗？
5.  何时以及如何集成代码？

# 2.与团队分享你的计划，不要在孤岛中发展

![](img/016ab31b0dc29f10bbbe53fcb96041f6.png)

重构代码是一项协作工作。尽管您可能负责编码，但与您的开发伙伴交流仍然是一个好主意。从未记录的细微差别、依赖性或集成见解中，其他开发人员可以获得丰富的知识。

## 请求反馈的方法

**在较小的团队中**

花点时间认真思考你的问题，并把它们写下来。尊重是很重要的，所以通过做好准备来尊重他们的时间。当你准备好的时候，简单地问“当你有机会的时候，我可以帮你做一些事情吗？”。

**测试驱动的开发团队**

与开发人员进行离线对话是很正常的，但是典型的拉请求是由单元测试发出的。这些测试然后由团队审查，他们可以对想法和结构给出反馈。

**每周同行代码评审**

一些团队每周进行代码评审，这给你一个机会通过评审彼此的代码来成长和学习。在这些评估过程中，重要的是你是一个积极的观察者。提出问题，指出你正在做的和其他人有重叠的地方。

# 3.编码前的单元测试

在重写一行代码之前，您应该有尽可能多的单元测试代码覆盖率。功能被破坏的可能性很高，如果没有原始功能的可靠基准，就很难知道缺少了什么。

多少才算足够的单元测试？

100%的代码覆盖率是一个很好的目标，然而，最重要的因素是工作流。至少，你的单元测试应该包括成功和错误的路径。如果有多个特性或方法，也应该进行测试。理想情况下，您希望限制供应的数量，并将测试作为成功的关键指标。

# 4.证明文件

很多时候，决策是在代码中做出的，而最初的开发人员不再解释。文档将保持知识在应用程序中流动。在原始开发人员仍然可用的情况下，文档允许知识的转移，而没有持续入职的开销。任何开发人员都可以阅读代码内文档，并了解做了什么以及如何使用它。

通过正确地记录您的代码，编辑器可以阅读文档并提供代码提示。一个很好的例子是使用@ depecrated 标签。Webstorm、Visual Studio、RIder 和其他现代 ide 将删除任何不推荐使用的函数或方法。这种智能感知是无价的，正如你在下面的图片中看到的，当使用错误或代码提示的类型使过程进行得更快时，会有即时反馈。

除了代码内文档，这里还有一个你应该考虑编写的其他文档的列表

# 5.受控的集成和发布策略

您的功能已经完成，现在可以开始集成过程了。你要做的第一件事是列出将受影响的区域。对于每个确定的区域，更新然后测试。这些测试可以是以下部分或全部。

**模拟或实时数据**

如果您无法访问实时数据，尽可能使用实时数据进行测试；精确模拟的数据将是下一个最好的东西。尽管随机化的文本生成器对于初始开发来说非常好，但是您希望确保您的数据是相同的单词和句子长度，以确保视觉保真度。

# 部署策略

有许多发布新代码的技术，每一种都有其优点和缺点。总的目标是让你的代码以一种可控制和可预测的方式呈现给最终用户。以下是可能的部署选项列表。

[嘲讽库机会](https://chancejs.com/)
关于单元测试你需要知道什么

# 结论

有了一个好的计划和良好的沟通，您可以使从需求到部署的代码重构过程尽可能地可预测和可靠。是时候把你学到的东西付诸实践了**让我们开始吧**

*原载于 2019 年 12 月 3 日*[*https://edithsonabelard.com*](https://edithsonabelard.com/5-tips-for-refactoring-code/)*。*