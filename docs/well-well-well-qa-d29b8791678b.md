# 嗯，嗯，嗯… QA

> 原文：<https://levelup.gitconnected.com/well-well-well-qa-d29b8791678b>

![](img/3f8ba4912eeb69f174b1b9574e6d27e6.png)

[Riccardo Pelati](https://unsplash.com/@craig000?utm_source=medium&utm_medium=referral) 在 [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral) 上拍摄的照片

你曾经做过一个项目，几个小时或几天后，你的系统崩溃了吗？这对于系统开发者和实际用户来说都是很平常的事情。当软件准备好了，它实际上还没有——软件永远不会结束。

让我们想象一下，你，或者一个团队，部门，等等，被报告你的项目有问题，他们很快开始修复，但是新的错误确实出现了。事实是，在投入生产之前，我们总是需要进行令人筋疲力尽的测试。不做测试是不负责任和鲁莽的。

因此，当`QA`出现时，`QA`或**质量保证**是防止产品错误或缺陷的方法(一般而言)，这可以应用于制造、医疗程序等。另一个关键组件`QA`是`QC` ( **质量控制**)，它实际上是在寻找缺陷。除了监控最终产品，QA 也存在于开发和测试过程中。`QA`包罗万象。

这同样适用于软件，它被称为`SQA`，其目标是，首先，参与到软件开发过程实现的每一个单独的部分，其次，确保软件在那里执行预期的任务(通过所有之前的测试用例等等)。软件是复杂的，因此不仅仅需要测试人员，测试人员是一个不同的角色。

`QA Engineers`有更多的战略功能，定义有效测试的需求，需要什么样的测试来实现特定的东西，并积极地监控列出的运行测试。相反，测试人员在那里执行并发现代码中的缺陷，在它的每一个方面，这被称为**测试用例**(将在后面解释)。

让我们简单回顾一下，我们有一个叫做`QA`的流程，它可以防止产品出现错误和缺陷。it 的`Software`版本，或 **SQA** ，帮助监控软件的开发过程(测试和实践)，以确保我们的产品中不会出现错误。质量保证关注过程

## 实施

`Software development`流程的最基本流程始于**创意**，将其转化为**功能**，然后开发、测试并部署到产品中。这个整个过程是非常庞大的，而且因为 QA 是(或者应该)存在于每一件事情中，这个工作实际上是一个很好的主角。

`QA`试图避免巨大的设计和技术挑战，为此，它参与每个过程，寻求功能开发和软件行为不断变化的解决方案，这实际上是由验收标准处理的，通常在规划阶段制定(稍后将介绍)。

所以，让我们把`acceptance criteria`看作是产品可以容忍的东西，任何可能的误差都有不确定性，对于 **QA** ，验收标准就像是经过认证的或者是生产的一种方式。一旦它被定义，它就被开发，然后被测试。QA 团队为该特性生成一个**测试用例**，并评估结果。

# 测试用例，终于来了！

测试用例是对重现的步骤的评估和预期结果的结合，就是这样。这就像是为了证明你所做的事情(作为一个开发人员)按照以前的验收标准工作的日志。如果测试用例中的某些东西失败了，或者如果产品没有按照预期的那样运行，那么它必须被修复。

无意中，软件错误在版本中出现，可悲的是，这导致了不愉快的用户和大量的支持票，这可能出现在软件的任何部分，也有缺陷，这是工作很好但在用户中产生抱怨的代码片段，缺陷也需要分类，并由 QA 仔细处理，不要将其与程序中的错误混合在一起。

**bug**需要上报，重新测试，直到大部分修复。记住一点，软件是无止境的，你开发，测试，发布，等待反馈，等等。

# 创建测试计划

这是整个 QA 流程中最重要的部分。计划是为系统的特定部分设计和创建的，例如:确认用户注册，从 CRUD 中删除一个项目，或者你的系统执行的任何事情。

计划本身不难定义，但是需要对文档需要什么进行大量的分析。根据 TPS 或测试程序规范，该计划应包含范围、时间表、测试可交付成果、发布标准以及风险和意外情况。

下面是每一个的解释。

1.**测试范围**说明了测试计划的目标，以及哪些工作可能超出了测试计划的范围

2. **Schedule** :这组测试将花费多长时间来估计执行时间(小时、天、月等)。

3.从测试计划中生成的**测试可交付成果**报告和数据，必须被收集用于测试结果、错误报告或应用程序日志。这是带有结果的测试列表。

4.**发布标准**:给测试人员一种客观的方式来面对发布某些东西的压力，这是发布一个产品所需要的条件，这将有助于确定发布这些东西是否是好的，或者是否有必要

5.**风险和突发事件**:测试不确定性的度量，一个完整的数据集将与新软件一起工作，或者通过反转代码版本来降低风险。

数据测试的数量对于采取详细的操作可能是必要的，一些客户通常可能在他们的操作中使用不同数量的详细信息(取决于他们的需求)。

这很好，但是之前完成并测试的代码呢？新的变化仍然通过了旧代码的先前测试用例吗？

# 回归

第一次测试一个可交付的代码是好的，但是旧的代码呢？在软件发布之前，我们需要确定软件的结果是否可行，我们应该测试旧的代码，并验证旧的测试用例是否完成或仍然通过。

这是通过做一些回归测试来完成的。

**回归测试**是为了运行旧的测试用例，我们在软件中“寻找回归”，如果之前通过的测试现在意外失败(现在是回归测试)，那么就需要**特性测试**。

一个**特性测试**是不言自明的，这是一个对软件中的新功能或者对我们来说是新的重大修改的测试。如果你有一个先前的特性被重写了两次以上，你也可以把它当作一个特性测试。

这是在**风险和意外事件**章节之后完成的。

## 其他测试

更多的测试也可以被添加到测试计划中。**配置测试**用于检查您的软件在某些系统配置、操作系统、浏览器、移动环境等中的工作情况。这种特殊类型的测试对于 **UI 测试**总体来说至关重要，对于测试**移动设备**和**布局**也是如此。您可以限制范围以支持特定类型的设备，并为特定支持的测试收集更多数据。像 **BrowserStack** 这样的工具可以很好的解决这个问题。

其他伟大的测试可能是**探索**和**自动化测试**。

**探索测试**通过尝试新事物或做非典型行为来发现潜在问题。这很有帮助，因为您可以预测用户认为这是一个正常过程会做什么。

另一方面，**自动化** **测试**本身来说，这些测试指导机器执行编程测试，这种委托可以让 QA 团队专注于其他一些测试。与之相对应的是，编码测试更多的是在准备中，而不是手动执行。为此检查**硒化 HQ** 工具。

这时我们可以有一个计划，我们知道不同类型的测试。然后，我们需要构建**测试用例**。

# 创建手动测试用例

这是 **QA 流程**的坚实基础。**测试用例**实际上为编写软件的人提供了有用的文档。

**测试用例**是被测软件中存在的每个代码片段或任何功能的特定场景。

这个包括一个作为标识符的**名称**，表示重现案例所需的**设置**部分，之后是**步骤**，它基本上列出了执行的动作和结果，最后是一个**拆卸**部分，它在执行测试之前清除数据。

根据 QA 团队收集的内容，这在某个时间会在一个广泛的文档中呈现。

所以，让我们稍微回顾一下，你必须为测试设置一个名称，步骤应该是非常原子的，然后，你需要对测试人员在合理的范围内将做什么做出假设，最后，添加清理数据的拆卸步骤(如果必要的话)

## 总是想着快乐的路

最后一个概念，不直接与 QA 过程同步，但当然可以用于执行某些类型的测试用例，这就是预期路径或**快乐路径**与可能性**测试用例**之间的区别

这个**快乐路径**基本上就是这个功能想要做的。想想这一点，开发人员在工作时，并不总是考虑或了解用户能做什么或不能做什么的一切，因此，自然地，他们在构建那个有问题的路径时工作，而不考虑其他潜在的情况或功能的变通办法。

就是这样。

那么，这篇引言能得出什么结论呢？。测试是必要的，不仅是在单元测试或代码中的 TDD 实践上，而且是在 QA 环境的实现中。软件总是可以变得更好，这是事实。有更多的测试和指南来改进测试计划、案例等等。

这是一个全新的世界，真的。这值得。在另一篇文章中，我将进一步阐述 QA 过程的实践。

如有必要，请随意扩展和更正。这只是我的经验之谈。向质量保证工程师致敬。

快乐编码:)